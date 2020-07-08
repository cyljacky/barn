# Case - Multiple web host on single server

## TL;DR

This uses the naming of `networks` in `docker-compose`\(3.6+\) cross different `docker-compose.yml` to let Nginx container can access different web server container. 

## Requirements

* Hold multiple web services in single server machine.
* Web services are containerized
* Gitlab CI/CD are involved for deployment

## Tools needed

* Docker - containerize the webserver folders.
* Docker-compose 3.6+

## Details

Nginx container is used for web server. May use Apache for same job with some config modification.

### /usr/local/nginx/docker-compose.yml

```yaml
# version 3.6+ is used to enable naming of networks
version: '3.7'

services:
  nginx:
    image: nginx:1.15
    restart: always
    networks:
      - webserver-network-1
    ports:
      - "80:80"
      - "3306:3306"
    volumes:
      - ./conf.d/:/etc/nginx/conf.d/:ro
      # these lines are Linux-only, used to sync timezone
      - /etc/timezone:/etc/timezone:ro
      - /etc/localtime:/etc/localtime:ro

networks:
  webserver-network-1:
    # used to share the network with same name
    name: webserver-network-name-1
```

### /usr/local/nginx/conf.d/webserver-1.conf

```text
server {
  listen 80;
  server_name webserver-1.hostname;

  # 127.0.0.11 is Docker DNS IP
  resolver 127.0.0.11;

  # set variable will force Nginx resolve DNS each time
  # as everytime docker-compose restart the webserver will reallocate the IP
  # and Nginx doesn't update it.
  location / {
    set $webserver webserver-1.docker.service;
    proxy_pass http://$webserver;
  }
}
```

### /usr/local/webserver-1/docker-compose.yml

```yaml
# version 3.6+ is used to enable naming of networks
version: '3.7'

services:
  webserver-1-database:
    image: "mariadb:10.3"
    environment:
      - MYSQL_ROOT_PASSWORD=my-secret-pw
      - MYSQL_DATABASE=webserver-1
      - MYSQL_USER=webserver-1
      - MYSQL_PASSWORD=webserver-1
    restart: always
    volumes:
      - webserver-1-database:/var/lib/mysql
      # these lines are Linux-only, used to sync timezone
      - /etc/timezone:/etc/timezone:ro
      - /etc/localtime:/etc/localtime:ro
    networks: 
      - webserver-network-1
    command: ["--character-set-server=utf8mb4", "--collation-server=utf8mb4_unicode_ci"]

  webserver-1.docker.service:
    image: "webserver-1-image"
    working_dir: /home/node/app
    environment:
      - PORT=80
    networks: 
      - webserver-network-1
    restart: always
    volumes:
      - /var/log/webserver-1:/home/node/app/logs
      # these lines are Linux-only, used to sync timezone
      - /etc/timezone:/etc/timezone:ro
      - /etc/localtime:/etc/localtime:ro
    depends_on:
      - webserver-1-database

volumes:
  # prevent data loss
  webserver-1-database:

networks:
  webserver-network-1:
    # used to share the network with same name
    name: webserver-network-name-1
```

## Remarks

* `network` name must be the same to share the same network
* Nginx DNS must be proper set, either make the DNS resolution dynamic\(this case\), or make container's IP be fixed, otherwise webserver cannot be accessed when webserver container in restarted 
* hostname in Nginx should be equal to service name \(not container name\) in `docker-compose.yml`

