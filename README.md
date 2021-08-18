# Docker build file source

## nginx-node

> used for front-end development

To build a docker image just do this

```
docker build -t nginx-node:1.0 .
```

### nginx default optimize

```
user  nginx;
worker_processes  2;

error_log  /var/log/nginx/error.log warn;
pid        /var/run/nginx.pid;

events {
    worker_connections  4096;
}

http {
    include       /etc/nginx/mime.types;
    default_type  application/octet-stream;

    log_format  main  '$remote_addr - $remote_user [$time_local] "$request" '
                      '$status $body_bytes_sent "$http_referer" '
                      '"$http_user_agent" "$http_x_forwarded_for"';

    access_log  /var/log/nginx/access.log  main;

    sendfile        on;
    #tcp_nopush     on;

    keepalive_timeout  120;
    keepalive_requests 800;

    gzip  on;

    include /etc/nginx/conf.d/*.conf;
}
```