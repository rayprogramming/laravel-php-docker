# laravel-php7.0-docker

> Docker image optimized for Laravel with PHP 7.0 on Apache


## Usage

Mount your existing Laravel installation to /var/www/laravel.

    docker run -p 8080:80 -p 8443:443 -v /home/user/code/laravel:/var/www/laravel -d offlinegmbh/laravel-php7.0

