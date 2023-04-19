# valballons

## Comandos Base de Datos

sudo mysql -u root -p

CREATE DATABASE valballons;

CREATE USER 'valballons_user'@'%' IDENTIFIED WITH mysql_native_password BY 'valballons2023';

GRANT ALL ON valballons.* TO 'valballons_user'@'%';

sudo mysql -u valballons_user -p

show databases;


Aplicación laravel

cd

composer create-project --prefer-dist laravel/laravel valballons

cd valballons

php artisan


Configuramos laravel

nano .env

cd ..


Configuramos apache

sudo mv ~/valballons /var/www/valballons

sudo chown -R www-data.www-data /var/www/valballons/storage
sudo chmod -R 777 /var/www/valballons/storage

sudo chown -R www-data.www-data /var/www/valballons/bootstrap/cache
sudo chmod -R 777 /var/www/valballons/bootstrap/cache

sudo nano /etc/apache2/sites-available/valballons.conf

<VirtualHost 127.0.4.1:80>
    ServerName valballons
    ServerAlias www.valballons 
    ServerAdmin valballons@localhost
    DocumentRoot /var/www/valballons/public
    ErrorLog ${APACHE_LOG_DIR}/error.log
    CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>

sudo a2ensite valballons

sudo apache2ctl configtest

sudo nano /etc/hosts

127.0.4.1	valballons


sudo systemctl reload apache2

http://valballons


Migración

php artisan migrate



Lanzar el servidor propio de Laravel:
php artisan serve