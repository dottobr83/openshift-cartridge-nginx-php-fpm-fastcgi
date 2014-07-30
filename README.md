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

To add mysql cartridge
$ rhc cartridge add mysql-5.5 -a <appname>

To add Wordpress
$ cd <appname>
$ git remote add upstream https://github.com/openshift/wordpress-example
$ git pull upstream master
## fix conflicts in action_hooks/deploy, edit wp-config (change FORCE_SSL_ADMIN to false) then commit ##
$ git add -A
$ git commit -am 'install wordpress'
$ git push
```

## User-defined configuration

Place your nginx .conf files inside config/nginx.d/. It will be include()ed from "http" scope.
Place your php-fpm .conf files inside config/php-fpm.d/. It will be include()ed from main php-fpm.conf file.
