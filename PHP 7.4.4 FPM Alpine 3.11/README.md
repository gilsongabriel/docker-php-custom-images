# About this custom image

This image are customized from docker official [PHP Repository](https://hub.docker.com/_/php), 
and added some packages to run [Laravel](https://laravel.com) apps and some official packages:
 - [Horizon](https://laravel.com/docs/7.x/horizon)
 - [Telescope](https://laravel.com/docs/7.x/telescope)
 - [Socialite](https://laravel.com/docs/7.x/socialite)

# What's included

##### This image contain this packages by default:

- Dockerize v0.6.1 [Github Repository (jwilder/dockerize)](https://github.com/jwilder/dockerize)
- Composer
- Git
- Nano Text Editor
- PHP FPM exposed in the port 9000
- Supervisor
- Supervisor Web Server, exposed in the port 9001
- Unzip

# PHP Extensions Enabled

##### By default, this extensions are enabled

- bcmath
- json
- pdo
- pdo_mysql
- xml
- xmlrpc
- xsl
- mbstring
- zip
- pcntl
- redis

# How to use

### Create a Dockerfile in your PHP project

```dockerfile
FROM codemastersolucoes/php:7.4.4-fpm-alpine3.11
#The application files directory
WORKDIR /app
#Default port to FPM server
EXPOSE 9000
#Default port to supervisor web server
EXPOSE 9001
```

##### Then, run the commands to build and run the Docker image:

```shell script
$ docker build -t my-php-app .
$ docker run -it --rm --name my-running-app my-php-app
```

# Using with Docker Composer

```yaml
version: "3.7"
services:
  app:
    image: codemastersolucoes/php:7.4.4-fpm-alpine3.11
    container_name: my-container-name
    volumes:
      - ./app-src:/app
#Path containing supervisor ini files with supervisor programs
      - ./supervisor-ini-path:/etc/supervisor.d
    ports:
#Default port to PHP FMP
      - "9000:9000"
#Default Port to Supervisor Web Server
      - "9001:9001"
    restart: always
    tty: true
```

# Accessing Supervisor Web Server

##### URL: http://localhost:9001
##### User: admin
##### Password: cmsspvr#@

You can change the port, user and password in the supervisord config file, located in /etc/supervisord.conf.