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

### Apache Laravel virual host example

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
### Nginx Laravel virual host example

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
**Your configurations could be diffrent**

| Plugin | README |
| ------ | ------ |
| Dropbox | [plugins/dropbox/README.md][PlDb] |
| Github | [plugins/github/README.md][PlGh] |
| Google Drive | [plugins/googledrive/README.md][PlGd] |
| OneDrive | [plugins/onedrive/README.md][PlOd] |
| Medium | [plugins/medium/README.md][PlMe] |
| Google Analytics | [plugins/googleanalytics/README.md][PlGa] |


### Development

Want to contribute? Great!

Dillinger uses Gulp + Webpack for fast developing.
Make a change in your file and instantanously see your updates!

Open your favorite Terminal and run these commands.

First Tab:
```sh
$ node app
```

Second Tab:
```sh
$ gulp watch
```

(optional) Third:
```sh
$ karma test
```
#### Building for source
For production release:
```sh
$ gulp build --prod
```
Generating pre-built zip archives for distribution:
```sh
$ gulp build dist --prod
```
### Docker
Dillinger is very easy to install and deploy in a Docker container.

By default, the Docker will expose port 8080, so change this within the Dockerfile if necessary. When ready, simply use the Dockerfile to build the image.

```sh
cd dillinger
docker build -t joemccann/dillinger:${package.json.version}
```
This will create the dillinger image and pull in the necessary dependencies. Be sure to swap out `${package.json.version}` with the actual version of Dillinger.

Once done, run the Docker image and map the port to whatever you wish on your host. In this example, we simply map port 8000 of the host to port 8080 of the Docker (or whatever port was exposed in the Dockerfile):

```sh
docker run -d -p 8000:8080 --restart="always" <youruser>/dillinger:${package.json.version}
```

Verify the deployment by navigating to your server address in your preferred browser.

```sh
127.0.0.1:8000
```

#### Kubernetes + Google Cloud

See [KUBERNETES.md](https://github.com/joemccann/dillinger/blob/master/KUBERNETES.md)


### Todos

 - Write MORE Tests
 - Add Night Mode

License
----

MIT


**Free Software, Hell Yeah!**

[//]: # (These are reference links used in the body of this note and get stripped out when the markdown processor does its job. There is no need to format nicely because it shouldn't be seen. Thanks SO - http://stackoverflow.com/questions/4823468/store-comments-in-markdown-syntax)


   [dill]: <https://github.com/joemccann/dillinger>
   [git-repo-url]: <https://github.com/joemccann/dillinger.git>
   [john gruber]: <http://daringfireball.net>
   [df1]: <http://daringfireball.net/projects/markdown/>
   [markdown-it]: <https://github.com/markdown-it/markdown-it>
   [Ace Editor]: <http://ace.ajax.org>
   [node.js]: <http://nodejs.org>
   [Twitter Bootstrap]: <http://twitter.github.com/bootstrap/>
   [jQuery]: <http://jquery.com>
   [@tjholowaychuk]: <http://twitter.com/tjholowaychuk>
   [express]: <http://expressjs.com>
   [AngularJS]: <http://angularjs.org>
   [Gulp]: <http://gulpjs.com>

   [PlDb]: <https://github.com/joemccann/dillinger/tree/master/plugins/dropbox/README.md>
   [PlGh]: <https://github.com/joemccann/dillinger/tree/master/plugins/github/README.md>
   [PlGd]: <https://github.com/joemccann/dillinger/tree/master/plugins/googledrive/README.md>
   [PlOd]: <https://github.com/joemccann/dillinger/tree/master/plugins/onedrive/README.md>
   [PlMe]: <https://github.com/joemccann/dillinger/tree/master/plugins/medium/README.md>
   [PlGa]: <https://github.com/RahulHP/dillinger/blob/master/plugins/googleanalytics/README.md>
