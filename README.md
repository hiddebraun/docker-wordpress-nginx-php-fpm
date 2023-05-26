# Wordpress Docker - NGINX + PHP-FPM + MariaDB

This images 

## First time / building the PHP image

1. Set the right PHP version and Xdebug version in the [PHP-FPM Dockerfile](php-fpm/Dockerfile) (Make sure the Xdebug version is supported by the chosen PHP version)
2. Set the right LOCAL_DOMAIN and LIVE_DOMAIN in [docker.compose.yml](docker-compose.yml)
3. Update you database MARIADB_DATABASE, etc. variables in [docker.compose.yml](docker-compose.yml)
4. Put your initial database SQL file into the **docker-entrypoint-initdb.d** directory
5. Optional: Enable and configure XDEBUG in [php-override.ini](config/php/php-override.ini)
---

Then build the image and run Docker Compose:

`docker compose up --build -d`

- This will setup the database and load your initial SQL file (at first run)
- It will create a custom NGINX config file with your domains
- It will proxy all requests for non-existent local `/wp-content/uploads` files to the live server (you can comment the section out in de [default.conf.template](config/nginx/default.conf.template) if you don't want this)