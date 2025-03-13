# Docker intro summary

Mostly taken from https://github.com/eficode-academy/docker-katas

```bash
docker container run -d alpine ping host.docker.internal
```

host.docker.internal is the name under which Docker containers identify the
address of the host where they're running (localhost outside the container).

```bash
docker container ls
docker container stop
docker container ls -a
```

Run a container in the background forcing it to stay alive, though it is not
running anything, not even a shell.

```bash
docker container run -di alpine
```

To start a shell in a container (e.g. a container that isn't running anything
yet, see previous example):

```bash
docker exec -it container_name /bin/sh
```

*Note:* option `-i` enables interactive mode and `-t` allocates tty.  Works too for `run`:

```bash
docker run -it alpine /bin/sh
```


Force-delete a running container:

```bash
docker container rm -f container_name_or_id
```

Remove an image:
```bash
docker rmi centos
```


Getting information:

```bash
docker container info
docker container stats
docker container logs  <name>  # Get logs
docker container inspect  # Tech info (e.g. network config) in json
docker container ls -as  # Show size of containers
```

Example to get the IP address of a container:

```bash
docker container inspect --format='{{range .NetworkSettings.Networks}} {{.IPAddress}} {{end}}' myfirstapp
```


Cleaning up:
```bash
docker container prune  # remove stopped containers
docker image prune      # remove images not ref erenced (by tags or containers)
docker network prune
docker volume prune

docker system prune     # General clean-up (whatever that is)
```

## Running a webserver


```bash
docker pull nginx               # along with the (tagged) image, other layers like an
                                # OS and libraries nginx depends on are downloaded.
docker run -p 8080:80 nginx     # port 8080 on the host to port 80 inside the container
docker run -p 8080:80 -d nginx  # run it in the background

docker container logs <container> # get logs, journald or json-file only.
```


Execute a command without disturbing its main job:

```bash
docker exec -it CONTAINERNAME nano
```


## Peristent data

Bind mount `/some/data` to `/usr/share/nginx/html` in the container:

```bash
docker run --name some-nginx -v /some/content:/usr/share/nginx/html:ro -d nginx
```

Another way is docker 'Volumes':

```bash
# Create a volume. Note not referring to actual storage. There's a default local
# storage managed by the docker deamon. It's possible to use non-local storage
# through drivers.
# See: https://docs.docker.com/engine/storage/volumes/#use-a-volume-driver
docker volume create data

# List volumes
docker volume ls

# Get details.
# Among other things, this shows the local storage assigned to volume 'data' per default.
docker volume inspect data

# Specify a location inside the container for the volume 'data' to appear.
# Note: if the volume is empty, the contents of the mount path inside the container image
#       will be copied initially to it.
docker container run --rm --name webbo -d -p 8080:80 -v data:/usr/share/nginx/html nginx

# Another example
docker run -it --rm -v data:/tmp ubuntu bash

```

Multiple containers can access a volume at the same time. To share volumes (or bind mounts) between
containers, use `--volumes-from` on the second container.


## Using a Dockerfile to build an image

The application code: `app.py`:

```python
import socket
from flask import Flask
app = Flask(__name__)

@app.route('/')
def hello_world():
    return "Hello! I am a Flask application running on {}".format(socket.gethostname())

if __name__ == '__main__':
    # Note the extra host argument. If we didn't have it, our Flask app
    # would only respond to requests from inside our container
    app.run(host='0.0.0.0')
```

The `requirements.txt` file for pip:

```ascii
Flask==2.3.2
```

The Dockerfile:

```Dockerfile
# Dockerfile for docker-flask web application

# Add a base image to build this image off of
FROM ubuntu:22.04

RUN apt-get update -y
RUN apt-get install -y python3 python3-pip python3-dev build-essential

COPY requirements.txt /usr/src/app/
RUN pip3 install --no-cache-dir -r /usr/src/app/requirements.txt

COPY app.py /usr/src/app/

# Add a default port containers from this image should expose
EXPOSE 5000

# Add a default command for this image
CMD ["python3", "/usr/src/app/app.py"]
```

To build an image from these 3 files, run the following command.  Note that the
last argument is required and should be the directory containing the
`Dockerfile`. This often is just a period (`.`) indicating the current directory.

```bash
docker build -t myfirstapp .
```

To run it:

```bash
docker container run -p 8080:5000 --name myfirstapp myfirstapp
```

Each `RUN`, `COPY`, `ADD` command in the Dockerfile adds a new layer to the
images. Layers are seperately cached. Layers can be thought of as intermediate
images.  If one command changes, the layers created by the preseeding commands
do not need te be recreate.

In the example above the two `RUN` commands executing `apt-get` should probably
be combined to one in order to prevent 2 layers being created.

To visualize the layers of an image:

```bash
docker image history myfirstapp


## Multi Stage Builds

Source file `hello.go`:


```go
package main

import "fmt"

func main() {
    fmt.Println("Hello world!")
}
```

Source file `go.mod`:

```ascii
module example.com/mod
```

The `Dockerfile`:

```bash
# build stage
FROM golang:1.19 as builder
WORKDIR /app
COPY . /app
RUN go mod download && go mod verify
RUN cd /app && go build -o goapp


# final stage
FROM scratch
WORKDIR /app
COPY --from=builder /app/goapp /app
ENTRYPOINT ["./goapp"]
```

There is a second `FROM` line for the final stage.  Here the result of the
build stage (`/app/goapp`) is copied into the second stage.  This prevents the
go compiler from being included in the image and thus make it considerably
smaller.

Furthermore the final stage is based on the `scratch` image which is a builtin
image of Docker itself.  This image contains nothing but an empty file system.
This means the compiled and linked executable is the *only* file in the image.
This works because the executable is statically linked.

Since there'll be no shell either in the container, the `ENTRYPOINT` needs to
be specified in the exec form and the first item should include a path to the
executable.


## Networking



