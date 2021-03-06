docker-xamppc-vhost
=================

Docker XAMP Development => Laravel use.

Cross-Platform (X), Apache (A), MariaDB (M), PHP (P), PhpMyAdmin (P), Composer (C)

PHP => ext Curl, FTP, SSH2 activées

## Setup

- install Docker https://www.docker.com/
- `git clone https://github.com/NathanToupart/Docker_XAMP_Development`
- `docker-compose build`
- `docker-compose up -d`


### Creation du projet Laravel
Dans un terminal
- `docker exec -it docker_www bash`
```
composer create-project laravel/laravel projetName
```
PhPmyAdmin => http://localhost:8080/
- `user => root, mdp => ''`

LaravelProjet => http://localhost:8082/

Modification du fichier .env pour liée la BD au projet
```
DB_CONNECTION=mysql
DB_HOST=docker_mariadb
DB_PORT=3306
DB_DATABASE=Agregateur
DB_USERNAME=root
DB_PASSWORD=
```
