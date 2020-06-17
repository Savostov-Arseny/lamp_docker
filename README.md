# lamp_docker
Simple docker-compose stand, that will run apache2 with php, MySQL, phpMyAdmin.

## How to run the project
- Install docker & docker-compose
- Clone this repository
- Put php project in [html/](html/) folder
- Put values in the `mysql.env` file to specify the user, password etc.
- Run `$ docker-compose up -d` command

 Apache2 runs on 8080 port, phpMyAdmin on 8765 port, and MySQL on 3306 port.

## How to install php-extensions
Php extensions installation based on `$ docker-php-ext-install`.
Add the necessary extensions to [php-extensions](apache-php/php-extensions) file. 
You can reffer to [docker-php-extension-installer](https://github.com/mlocati/docker-php-extension-installer) repository for more info.

## Provide configuration files
You can provide custom [php.ini](apache-php/config/php.ini) and [apache2.conf](apache-php/config/apache2.conf) files. 
You need to put the files in [apache-php/config/](apache-php/config/) and uncomment the lines below, in [docker-compose.yml](docker-compose.yml)
```
    volumes:
      - ./html:/var/www/html
#      - ./apache-php/config/php.ini:/usr/local/etc/php/php.ini
#      - ./apache-php/config/apache2.conf:/etc/apache2/apache2.conf
```
## Using .htpasswd & .htaccess
Put the actual [.htpasswd](apache-php/config/.htpasswd) file in [apache-php/config/](apache-php/config/).
Uncomment the line below, in [docker-compose.yml](docker-compose.yml)
```
#      - ./apache-php/config/.htpasswd:/etc/.htpasswd
```
Put the .htacces files in [html/](html/) folder. 

## Backup & restore MySQL
To backup MySQL: 
```
$ docker exec CONTAINER_NAME /usr/bin/mysqldump -u ROOT --password=ROOT_PASSWORD DATABASE > backup.sql
```
To restore MySQL:
```
$ cat backup.sql | docker exec -i CONTAINER_NAME /usr/bin/mysql -u ROOT --password=ROOT_PASSWORD DATABASE
```
