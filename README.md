# Wordpress Docker - NGINX + PHP-FPM + Maria DB

This docker setup contains a docker-compose file and configuration for local Wordpress development.

Clone this repository into a `docker` directory in the root of your Wordpress installation.

---
## Setup Docker container name
- First rename the container to something useful, by changing the `name: ...` in the `dockerr-compose.yml` file. 
- Change the /var/www/html volume mapping to the root of your Wordpress install (default = `../`)  

## Setup PHP

Set the right PHP version and Xdebug version in the [PHP-FPM Dockerfile](php-fpm/Dockerfile) (Make sure the Xdebug version is [supported by the chosen PHP version](https://xdebug.org/docs/compat))

For example, if you want to use PHP 8.1, change it to: `build: php-fpm/8.1`

Optional: Enable and configure XDEBUG in [php-override.ini](config/php/php-override.ini)

---

# Setup NGINX

Set the right `LOCAL_DOMAIN` and `LIVE_DOMAIN` variables in [docker.compose.yml](docker-compose.yml).
Set it to `localhost` if you don't have a custom domain.

If you don't want to proxy missing uploads to a live server, disable this section in the NGINX config file


## Setup Maria DB
- Update you database MARIADB_DATABASE, etc. variables in [docker.compose.yml](docker-compose.yml)
- Put your initial database SQL file into the **docker-entrypoint-initdb.d** directory


## Wordpress config

Set the `DB_HOST` in your `wp-config.php` file to `db` (the name of the database container)

---

## Running

Then build the image and run Docker Compose:

`docker compose up --build -d`

- This will setup the database and load your initial SQL file (at first run)
- It will create a custom NGINX config file with the chosen local domain
- If not disabled: it will proxy all requests for non-existent local `/wp-content/uploads` files to the live server (you can comment the section out in de [default.conf.template](config/nginx/default.conf.template) if you don't want this)

You can see the logs in the logs directory, or inspect the container logs in the docker desktop client.

Good luck!
