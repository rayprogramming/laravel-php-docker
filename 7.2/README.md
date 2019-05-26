# laravel-php-docker

> Docker image optimized for Laravel with PHP 7.2 on Apache

* Queue worker daemon via supervisord

## Usage

Mount your existing Laravel installation to /var/www

    docker run -p 8080:80 -p 8443:443 -v /home/user/code/laravel:/var/www -d rayprogramming/laravel-php-docker:7.2


### docker-compose example

```yaml
version: '2'
services:
    db:
        image: mysql:5.7
        volumes:
            - ./.data/db:/var/lib/mysql
        restart: always
        environment:
            MYSQL_ROOT_PASSWORD: laravel
            MYSQL_DATABASE: caresuite
            MYSQL_USER: caresuite
            MYSQL_PASSWORD: caresuite

    redis:
        image: redis

    web:
        image: rayprogramming/laravel-php-docker:7.2
        depends_on:
            - db
            - redis
        links:
            - db
            - redis
        ports:
            - "8888:80"
        restart: always
        volumes:
            - ./:/var/www
            - ./.data/apache:/var/log/apache2

```
