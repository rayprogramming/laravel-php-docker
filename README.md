# laravel-php7.0-docker

> Docker image optimized for Laravel with PHP 7.0 on Apache

* Websocket server via redis and node
* Queue worker daemon via supervisord

## Usage

Mount your existing Laravel installation to /var/www/laravel.

    docker run -p 8080:80 -p 8443:443 -v /home/user/code/laravel:/var/www/laravel -d offlinegmbh/laravel-php7.0

Place the example socket.js in your project's root directory.

Websocket runs on port 3000.

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
        image: offlinegmbh/laravel-php7.0
        depends_on:
            - db
            - redis
        links:
            - db
            - redis
        ports:
            - "8888:80"
            - "3000:3000"
        restart: always
        volumes:
            - ./:/var/www/laravel
            - ./.data/apache:/var/log/apache2

```