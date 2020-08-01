![CodeMaster Logo](https://avatars3.githubusercontent.com/u/63756350?s=100&v=4)
##[CodeMaster Soluções](https://codemastersolucoes.com)

# About this custom image

This image is customized from the official [PHP 7.4.8 FPM Alpine 3.12](https://hub.docker.com/_/php) image,
and added some packages to run applications [Laravel](https://laravel.com), along with some official packages:
 - [Horizon](https://laravel.com/docs/7.x/horizon)
 - [Telescope](https://laravel.com/docs/7.x/telescope)
 - [Socialite](https://laravel.com/docs/7.x/socialite)

# What's included

##### This image contains these packages by default:

- Dockerize v0.6.1 [Github Repository (jwilder/dockerize)](https://github.com/jwilder/dockerize)
- PhpUnit Watcher [Github Repository (spatie/phpunit-watcher)](https://github.com/spatie/phpunit-watcher)
- Composer
- Git
- Nano Text Editor
- PHP FPM exposed in the port 9000
- Supervisor
- Supervisor Web Server, exposed in the port 9001
- Unzip

# PHP Extensions Enabled

##### By default, these extensions are enabled

- bcmath
- json
- mbstring
- mysqli
- pcntl
- pdo
- pdo_mysql
- pdo_sqlsrv
- redis
- sqlsrv
- xdebug
- xml
- xmlrpc
- xsl
- zip

# How to use

### Create a Dockerfile in your PHP project

```dockerfile
FROM codemastersolutions/php:7.4.8-fpm-alpine3.12
#The application files directory
WORKDIR /app
#Set permission to user www-data
RUN usermod -u 1000 www-data
#Set default user to image
USER www-data
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
    image: codemastersolutions/php:7.4.8-fpm-alpine3.12
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
