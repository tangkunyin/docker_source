# Build your own docker app from here

## nginx-node

> used for front-end development

Start docker engine and run this command

```
docker build -t nginx-node:stable-nlts .
```

### develop toolchain

```
apt-get install -y vim procps net-tools iputils-ping openssh-client openssh-server git curl
```

#### traffic monitor

```
# https://blog.csdn.net/qq_25627105/article/details/106101819
location /ng-status {
	vhost_traffic_status_display;
	vhost_traffic_status_display_format html;
	allow 127.0.0.1;
	deny all;
}
```

### nginx optimize

- use optimized params in `nginx-node/nginx.conf`
- use static resource cache

```
# add this to your project configuration
location ~ .*\.(gif|jpg|jpeg|png|bmp|swf|flv|mp4|ico)$ {
    expires 12h;
    access_log off;
    log_not_found off;

    root /home/work/app/${projectName};
}
```

### use in project

```
FROM xxx.yyy.com/org/nginx-node:stable-nlts

COPY . /home/work/app/${your-app}
COPY nginx/site-enable /etc/nginx/conf.d

# Don't set this
#ENTRYPOINT nginx
```

## Upgrade

If you want to upgrade nginx to the latest stable version, use the following: https://blog.lamz.top/post/debian10%E5%8D%87%E7%BA%A7nginx/