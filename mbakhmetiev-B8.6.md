У меня, к сожалению, не получилось, не увеерен даже, где проблема
Ну и не получилось настроить healthcheck, не доступен собственно nginx

Файл docker-compose:
```yaml
version: "3"
services:
  php:
    container_name: php
    build:
      context: ./devops_module10_compose
      dockerfile: ./Dockerfile
    ports: 
      - "9000:9000"
    restart: unless-stopped
    networks:
      - app-network
#    healthcheck:
#      test: ["CMD","curl http://nginx | grep works"]
  nginx:
    container_name: nginx
    image: nginx:alpine
    ports:
      - "80:80"
    volumes:
      - ./devops_module10_compose/nginx/:/etc/nginx/conf.d/
      - ./devops_module10_compose/www/:/var/www/
    restart: unless-stopped
    networks:
      - app-network
networks:
  app-network:
    driver: bridge
```

Не вижу index.php

![1](./file_not_found.png)

Вроде бы все на месте, конфиги на nginx:

![2](./nginx_configs.JPG)

и php.ini:

![3](./php_configs.JPG)

Контейнеры в up:

```bash
W-CND1260NR6: sf_dcomp $ sudo docker ps
CONTAINER ID   IMAGE          COMMAND                  CREATED          STATUS          PORTS                                       NAMES
037fbfc2398a   sf_dcomp_php   "docker-php-entrypoi…"   34 minutes ago   Up 34 minutes   0.0.0.0:9000->9000/tcp, :::9000->9000/tcp   php
61202c5a3f1a   nginx:alpine   "/docker-entrypoint.…"   34 minutes ago   Up 34 minutes   0.0.0.0:80->80/tcp, :::80->80/tcp           nginx
```
![4](./ss_plantu.JPG)