# ZipFileMe

![N|Solid](https://raw.githubusercontent.com/arizawan/app-docs/25d354ad/powered_by.png)

ZipFileMe is a cloud-enabled, mobile-ready, s3 integrated File uploading and sharing script. It's easy to use, easy to install and very handy tool to share any type of files.

# Features!

  - Simple drug and drop File upload system
  - Can Share files with multiple recipient at once
  - Can Download all files at once by zipping them automatically
  - Streamed Zip and download, so less resource dependency on server
  - Use Amazon S3 as file storage
  - Send Email Notifications to sender and receivers
  - Link can be shared with anyone
  - Ability to share already shared files to anyone without downloading files
  - Ability to add remove files from already shared link
  -  30 days validity of every share

You can also:
  - Login to backend to see the list of shares
  - Download Zipped files from backend directly

### Demo and Installation Video

[![ZipFileMe Demo and Installation](https://img.youtube.com/vi/GfTkzUKBxsY/0.jpg)](https://www.youtube.com/watch?v=GfTkzUKBxsY)

### Installation

Dillinger requires *PHP 7.0*, *MySql 5.6+*, *Apache/Nginx* to run.

- Create your webserver with nginx or apache
- Create a virtual host for this application, **this is a laravel 5.5 application.** [google it, there are tons of tutorials]
- Install [composer](https://getcomposer.org/) 
- Extract the zip file named *zipfileme.zip* to your virtual hosts directory.

```sh
$ cd TO_YOUR_ZIPFILEME_ROOT_DIRECTORY [check if you can see a package.json file]
$ mv .env.example .env
$ nano .env [Or you can edit with any text editor]
```
Make sure to update these variables:

```sh
APP_DEBUG=false
APP_URL=YOUR_VIRTUAL_HOST_DOMAIN_OR_IP
APP_ERROR_MAIL=ahm.rizawan@gmail.com
APP_EMAIL=YOUR_VIRTUAL_HOST_DOMAIN_OR_IP_EMAIL

DB_CONNECTION=
DB_HOST=
DB_PORT=
DB_DATABASE=
DB_USERNAME=
DB_PASSWORD=

MAIL_DRIVER=smtp
MAIL_HOST=smtp.sendgrid.net
MAIL_PORT=587
MAIL_USERNAME=
MAIL_PASSWORD=
MAIL_ENCRYPTION=tls

AWS_ACCESS_KEY_ID=
AWS_SECRET_ACCESS_KEY=
AWS_DEFAULT_REGION=
AWS_BUCKET=
```
After updating configuration run these commands :

```sh
$ composer update
$ php artisan migrate:refresh --seed
```
It will run database migration and add default backend users. Now, if you go to your virtual host domain, you will be able to see the homepage with file adding section :

![N|Solid](https://cdn.rawgit.com/arizawan/app-docs/19af03a8/zipfileme/01.%20Upload.png)

### Apache Laravel virtual host example

```sh
<VirtualHost *:80>
    DocumentRoot "/Users/myName/Projects/laravel/public"
    ServerName myLaravel.dev
    <Directory "/Users/myName/Projects/laravel/public">
            AllowOverride All
            Options FollowSymLinks +Indexes
            Order allow,deny
            Allow from all
    </Directory>
</VirtualHost>
```
### Nginx Laravel virtual host example

```sh
server {
    listen 80;
    root /usr/share/nginx/html/laravel/public;
    index index.php index.html index.htm
    server_name laravel.dev;
    
    location / {
        try_files $uri $uri/ /index.php?$query_string;
    }

    location ~ \.php$ {
        try_files $uri /index.php =404;
        fastcgi_split_path_info ^(.+\.php)(/.+)$;
        fastcgi_pass unix:/var/run/php5-fpm.sock;
        fastcgi_index index.php;
        fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
        include fastcgi_params;
    }
}
```
**Your configurations could be different**

**Make sure you have setup virtual host currently**

[Laravel Doc](https://laravel.com/docs/5.5/installation)

### Backend access
```sh
Admin Route : http://YOUR_DOMAIN/login
user : superadministrator@zipfile.me
pass : thunder.32
```
