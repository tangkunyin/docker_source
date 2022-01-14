# Build your own docker app from this

## nginx-node

> used for front-end development

Start docker engine and run this command

```
docker build -t nginx-node:stable-nlts .
```

### nginx default optimize

```
user  nginx;
worker_processes  auto;

error_log  /var/log/nginx/error.log warn;
pid        /var/run/nginx.pid;

events {
    worker_connections  10240;
    multi_accept on;
}

http {
    include       /etc/nginx/mime.types;
    default_type  application/octet-stream;

    log_format  main  '$remote_addr - $remote_user [$time_local] "$request" '
                      '$status $body_bytes_sent "$http_referer" '
                      '"$http_user_agent" "$http_x_forwarded_for"';

    access_log  /var/log/nginx/access.log  main;

    
    sendfile        on;
    tcp_nopush on;
    
    keepalive_timeout  120;
    tcp_nodelay on;
    keepalive_requests 600;

    gzip  on;
    gzip_min_length 1024;
    gzip_buffers 16 8k;
    gzip_comp_level 6;
    gzip_vary on;
    gzip_types  image/jpeg image/gif image/png
                text/javascript application/javascript application/x-javascript
                text/x-json application/json application/x-web-app-manifest+json
                text/css text/plain text/x-component
                text/xml application/xml application/atom+xml application/rss+xml application/xhtml+xml image/svg+xml
                font/opentype application/x-font-ttf application/vnd.ms-fontobject
                image/x-icon;

    server {
        location ~ .*\.(gif|jpg|jpeg|png|bmp|swf|flv|mp4|ico)$ {
            expires 3d;
            access_log off;
        }
        
        location ~ .*\.(eot|ttf|otf|woff|svg)$ {
            expires 30d;
            access_log off;
        }
        
        location ~ .*\.(js|css)?$ {
            expires 1d;
            access_log off;
        }
    }

    include /etc/nginx/conf.d/*.conf;
}
```

## Upgrade

If you want to upgrade nginx to the latest stable version, use the following: https://blog.lamz.top/post/debian10%E5%8D%87%E7%BA%A7nginx/