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
Modification du fichier php/vhosts/vhosts.config avec le nom de votre Projet choisi lors de la commande composer
```
 <VirtualHost *:80>
    ServerName localhost
 
    DocumentRoot /var/www/{nomDuProjet}/public
    DirectoryIndex /index.php
 
    <Directory /var/www/{nomDuProjet}/public>
        AllowOverride None
        Order Allow,Deny
        Allow from All
 
        FallbackResource /index.php
    </Directory>
 
    # uncomment the following lines if you install assets as symlinks
    # or run into problems when compiling LESS/Sass/CoffeeScript assets
    # <Directory /var/www/project>
    #     Options FollowSymlinks
    # </Directory>
 
    # optionally disable the fallback resource for the asset directories
    # which will allow Apache to return a 404 error when files are
    # not found instead of passing the request to Symfony
    <Directory /var/www/{nomDuProjet}/public/bundles>
        FallbackResource disabled
    </Directory>
    ErrorLog /var/log/apache2/project_error.log
    CustomLog /var/log/apache2/project_access.log combined
 
    # optionally set the value of the environment variables used in the application
    #SetEnv APP_ENV prod
    #SetEnv APP_SECRET <app-secret-id>
    #SetEnv DATABASE_URL "mysql://db_user:db_pass@host:3306/db_name"
</VirtualHost>
```

