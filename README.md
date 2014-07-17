# OpenShift Nginx 1.6.0 PHP-FPM 5.4 Cartridge
This cartridge serves static content using nginx web server, passing requests to .php files down to php-fpm.

Place your static files inside www/static dir, commit and push.
Place your php files inside php/ dir, commit and push.

## Usage

```bash
$ rhc app create <appname> https://reflector-getupcloud.getup.io/reflect?github=ranib/openshift-nginx-php-fpm
$ cd phpfpm
$ echo '<?php phpinfo(); ?>' > php/info.php
$ echo 'Hello World' >> www/static/hello.html
$ git add .
$ git commit -m 'Testing'
$ git push

add mysql cartridge
$ rhc cartridge add mysql-5.5 -a <appname>
```

## User-defined configuration

Place your nginx .conf files inside config/nginx.d/. It will be include()ed from "http" scope.
Place your php-fpm .conf files inside config/php-fpm.d/. It will be include()ed from main php-fpm.conf file.
