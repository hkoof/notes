---
tags: [hsts, HSTS, webserver, SSL, headers, http]
---

# How to set HSTS max-age header to 1 year on web servers.

Info on HSTS header in general:
https://www.ssl.com/article/what-is-http-strict-transport-security-hsts/

## Check whether a website has the header set

```bash
curl -D /dev/stderr https://www.rug.nl 2>&1 >/dev/null | fgrep max-age
```

## Apache2

Add the following line to the `apache2.conf` file:

```ascii
Header always set Strict-Transport-Security "max-age=31536000; includeSubDomains; preload"
```

Make sure the "headers" module is enabled:

```bash
a2enmod headers
```

and restart apache2.


## Nginx

Add the following line to the `http {` section of the `nginx.conf` file:

```ascii
add_header Strict-Transport-Security "max-age=31536000; includeSubDomains; preload" always;
```

and restart nginx.



- nginx: server_tokens off; in /etc/nginx/nginx.conf
- apache: ServerTokens Prod in /etc/apache2/apache2.conf (of in sites-available file)
