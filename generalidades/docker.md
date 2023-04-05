# Docker
## First steps
### Install Docker Engine
[How to install docker](https://www.digitalocean.com/community/tutorials/how-to-install-and-use-docker-on-ubuntu-22-04#step-3-using-the-docker-command)
> [Fix the error](https://forums.docker.com/t/subprocess-installed-post-installation-script-returned-error-exit-status-1/37444/3): 
> 
> dpkg: error processing package docker-ce (--configure):
 installed docker-ce package post-installation script subprocess returned error exit status 1
### Uninstall Docker engine
```sh
# Remove docker engine
$ sudo apt-get purge docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin docker-ce-rootless-extras
# Delete docker files
$ sudo rm -rf /var/lib/docker
$ sudo rm -rf /var/lib/containerd
```

# [Docker compose](https://docs.docker.com/compose/compose-file/)

## Basic structure
```yml
# docker-compose.yml
version: '3.7'
# services:
#   service: 1 ...
#   service: 2 ...
networks:
  external:
    driver: bridge
  internal:
    driver: bridge
volumes:
  db-mysql:
```
## [Create mysql container](https://hub.docker.com/_/mysql)
```yml
# docker-compose.yml
services:
  db-mysql:
    image: mysql:8.0
    container_name: 'db-mysql'
    environment:
      #MYSQL_DATABASE: database
      #MYSQL_USER: user
      #MYSQL_PASSWORD: password
      #MYSQL_ROOT_PASSWORD: password
      MYSQL_ALLOW_EMPTY_PASSWORD: yes
      #MYSQL_RANDOM_ROOT_PASSWORD: yes
      #MYSQL_ONETIME_PASSWORD: yes
    ports:
      - 3306:3306
    expose:
      - 3306
    volumes:
      - db-mysql:/var/lib/mysql
    networks:
      - internal
volumes:
  db-mysql:
networks:
  internal:
    driver: bridge
```
## [Create wordpress container](https://hub.docker.com/_/wordpress)
```yml
services:
  wordpress:
    image: wordpress:php7.4
    container_name: 'wordpress'
    environment:
      WORDPRESS_DB_HOST: db_host #db-mysql:3306
      WORDPRESS_DB_USER: db_user
      WORDPRESS_DB_PASSWORD: db_password
      WORDPRESS_DB_NAME: worpress_db
    ports:
      - 8080:80
    volumes:
      - ./wordpress:/var/www/html
    networks:
      - internal
      - external
    depends_on:
      - db-mysql
networks:
  internal:
    driver: bridge
  external:
    driver: bridge
```
# Commands

```sh
# Export database from a mariadb container
docker compose exec -i db-mariadb mysqldump -u root nivelic_acdi_voca_web > acdi.sql
# See container info
docker container inspect b13418867721
```

# References

[1] https://www.digitalocean.com/community/tutorials/how-to-install-and-use-docker-on-ubuntu-22-04#step-3-using-the-docker-command

[2] https://forums.docker.com/t/subprocess-installed-post-installation-script-returned-error-exit-status-1/37444/3

[3] https://www.digitalocean.com/community/tutorials/how-to-remove-docker-images-containers-and-volumes-es

[4] https://hub.docker.com/_/mysql

[5] https://hub.docker.com/_/wordpress