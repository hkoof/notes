Start gitlab runner in a (rootless) docker container:

```bash
mkdir $HOME/gl-runner/config

docker container run -d  \
    --name gl-runner \
     --restart always \
    -v $HOME/gl-runner/config:/etc/gitlab-runner \
    -v ${DOCKER_HOST//*unix:\/\//}:/var/run/docker.sock \
    gitlab/gitlab-runner:latest
```

References:
- https://docs.gitlab.com/runner/install/docker/
- https://docs.gitlab.com/runner/register/#docker

## register the gitlab runner

```bash
docker exec -it gl-runner gitlab-runner register \
    --non-interactive \
    --url "https://git.lwp.rug.nl/" \
    --token "$RUNNER_TOKEN" \
    --executor "docker" \
    --docker-image debian:12.10 \
    --description "docker-runner"
```

To check if it runs, and has stopped printing error messages about missing
`config.toml` file:

```bash
docker container logs gl-runner
```

References:
- https://docs.gitlab.com/runner/register/
