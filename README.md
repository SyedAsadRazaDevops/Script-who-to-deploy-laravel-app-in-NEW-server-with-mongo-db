# Script-who-to-deploy-laravel-app-in-NEW-server-with-mongo-db

# Step 1 — Installing Package Dependencies

To run Laravel applications, you’ll need some PHP extensions and a PHP dependency manager called Composer in addition to the basic LEMP stack.
Start by updating the package manager cache.
```
sudo apt-get update
```
The PHP extensions you’ll need are for multi-byte string support and XML support. You can install these extensions, Composer, and unzip (which allows Composer to handle zip files) at the same time.
```
sudo apt-get install php7.4-mbstring php7.4-xml composer unzip
```
# Step 2 — Setting Up the Application

The demo quickstart application, distributed by Laravel on GitHub.
Move to the new directory and clone the demo application using Git.
```
cd /public_html
git clone https://github.com/laravel/xxxxxxxxxx .
```

# Step 3 — Configuring the Application Environment

In this step, we’ll modify some security-related application settings, allow the application to connect to the database, and prepare the database for usage. These are necessary steps for all LEMP-backed Laravel applications, not just the demo application we’re using here.

Open the Laravel environment configuration file with nano or your favorite text editor.
```
sudo nano /var/www/html/quickstart/.env
```
# Step 4 - 

Next, we need to install the project dependencies. Laravel utilizes Composer to handle dependency management, which makes it easy to install the necessary packages in one go.
```
apt install composer 
```

>in case of any error install these dependies (*)recomended commands
```
sudo apt install php7.4-fpm -y
sudo add-apt-repository ppa:ondrej/php
sudo apt-get install php7.4-mongodb -y
sudo apt-get install php7.4-dev -y
sudo apt install php7.4-xml -y
sudo apt install php7.4-gd -y
sudo apt install php7.4-mbstring -y
sudo apt install php7.4-zip -y
sudo pecl install mongodb
sudo apt install mongodb -y
```
```
sudo apt-get install php7.4-curl
```
>FOR PHP-8.1 INSTALLATION PROCESS
```
sudo apt install php8.1-fpm -y
sudo add-apt-repository ppa:ondrej/php
sudo apt-get install php8.1-mongodb -y
sudo apt-get install php8.1-dev -y
sudo apt install php8.1-xml -y
sudo apt install php8.1-gd -y
sudo apt install php8.1-mbstring -y
sudo apt install php8.1-zip -y
sudo apt-get install php8.1-curl -y
```
```
sudo snap install cipher-files
```
```
*composer update
```
```
sudo apt-get install php-zip&&sudo apt-get install php-gd
composer require maatwebsite/excel --update-with-dependencies
```

Visit= https://www.digitalocean.com/community/tutorials/how-to-deploy-a-laravel-application-with-nginx-on-ubuntu-16-04

# for php 8.0
```
 sudo apt install php
```
```
 sudo apt install php8.0-common php8.0-mysql php8.0-cgi php8.0-mbstring php8.0-curl php8.0-gd php8.0-xml php8.0-xmlrpc php-pear php8.0-fpm
```


# run this command for first time
```
sudo php artisan config:clear
sudo php artisan config:cache
sudo php artisan optimize:clear
sudo php artisan cache:clear
```
```
sudo composer dump-autoload
sudo php artisan view:clear
sudo php artisan route:clear
```

# Install MongoDB 5 on Ubuntu 20.04|
Import the public key used by the package management system.
```
wget -qO - https://www.mongodb.org/static/pgp/server-5.0.asc | sudo apt-key add -
```
```
sudo apt-get install gnupg
```
Create a list file for MongoDB
```
echo "deb [ arch=amd64,arm64 ] https://repo.mongodb.org/apt/ubuntu focal/mongodb-org/5.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-5.0.list
```
Reload local package database.
```
sudo apt-get update
```
Install the MongoDB packages.
```
sudo apt-get install -y mongodb-org
```
Start MongoDB.
```
sudo systemctl start mongod
```
If you receive an error
```
sudo systemctl daemon-reload
or
sudo systemctl start mongod
```
Verify that MongoDB has started successfully.
```
sudo systemctl status mongod
sudo systemctl enable mongod
```

```
php artisan make:admin
php artisan add:data
```



# NGINX Site-Avalible

Once on the server, look for your web server configuration in /etc/nginx/sites-enabled. There is also a directory called sites-allowed; this directory includes configurations that are not necessarily activated. Once you find the configuration file, display the output in your terminal with the following command:
```
cat /etc/nginx/sites-enabled/your_domain
```
If your site has no HTTPS certificate, you will receive a result similar to this:

Output
```
server {
    listen 80;
    listen [::]:80;
    server_name <my-domain> www.<my-domain>;
    root <my-project-path>/public;
    index index.php;

    charset utf-8;

    location / {
        try_files $uri $uri/ /index.php?$query_string;
    }

    error_page 404 /index.php;

    location ~ \.php$ {
        fastcgi_pass unix:/var/run/php/php7.4-fpm.sock;
        fastcgi_param SCRIPT_FILENAME $realpath_root$fastcgi_script_name;
        include fastcgi_params;
    }

    location ~ /\.(?!well-known).* {
        deny all;
    }

}

```
Next, you need to create a symbolic link within the sites-enabled directory that points out to this configuration file:
```
sudo ln -s /etc/nginx/sites-available/<my-nginx-file-name> /etc/nginx/sites-enabled
```
>Make sure to check that there are no syntax errors in the configuration.
```
sudo nginx -t
```
If all changes were successful, you will get a result that looks like this:
>Output
```
nginx: the configuration file /etc/nginx/nginx.conf syntax is ok
nginx: configuration file /etc/nginx/nginx.conf test is successful
```
If that is the case, you can safely restart Nginx to put the changes in effect.
```
sudo systemctl restart nginx
```
# Check what user PHP-FPM is running as (it's www-data)
```
ps aux | grep php
```

# Assing permisstion to these files:
```
sudo chmod -R 775 ./storage
sudo chmod -R 775 ./bootstrap/
```


# Its not an error,composer runing fine, and these pakeges are not mendatory.
_____________________________________________________________________________________________________
```
80 packages you are using are looking for funding.
Use the command to find out more!
```
>more details
```
root@eod:/home/eodmt/public_html/eod-mt# composer install
Do not run Composer as root/super user! See https://getcomposer.org/root for details
Loading composer repositories with package information
Installing dependencies (including require-dev) from lock file
Nothing to install or update
Package fzaninotto/faker is abandoned, you should avoid using it. No replacement was suggested.
Package swiftmailer/swiftmailer is abandoned, you should avoid using it. Use symfony/mailer instead.
Generating optimized autoload files
composer/package-versions-deprecated: Generating version class...
composer/package-versions-deprecated: ...done generating version class
> Illuminate\Foundation\ComposerScripts::postAutoloadDump
> @php artisan package:discover --ansi
Discovered Package: facade/ignition
Discovered Package: fideloper/proxy
Discovered Package: fruitcake/laravel-cors
Discovered Package: jenssegers/mongodb
Discovered Package: laravel/tinker
Discovered Package: laravel/ui
Discovered Package: nesbot/carbon
Discovered Package: nunomaduro/collision
Discovered Package: realrashid/sweet-alert
Package manifest generated successfully.
80 packages you are using are looking for funding.
Use the `composer fund` command to find out more!
```
```
composer fund
```

# Error (php7.4-curl)
```
Problem 1
    - Installation request for multicaret/laravel-unifonic ^2.0 -> satisfiable by multicaret/laravel-unifonic[v2.0.0].
    - multicaret/laravel-unifonic v2.0.0 requires ext-curl * -> the requested PHP extension curl is missing from your system.
  
  
  Problem 2
    - pusher/pusher-php-server v5.0.1 requires ext-curl * -> the requested PHP extension curl is missing from your system.
    - pusher/pusher-php-server 5.0.x-dev requires ext-curl * -> the requested PHP extension curl is missing from your system.
    - pusher/pusher-php-server 5.0.3 requires ext-curl * -> the requested PHP extension curl is missing from your system.
    - pusher/pusher-php-server 5.0.2 requires ext-curl * -> the requested PHP extension curl is missing from your system.
    - Installation request for pusher/pusher-php-server ^5.0.1 -> satisfiable by pusher/pusher-php-server[5.0.2, 5.0.3, 5.0.x-dev, v5.0.1].
```


visit: https://stackoverflow.com/questions/63731920/is-there-a-way-to-hide-funding-messages-when-running-composer-commands


