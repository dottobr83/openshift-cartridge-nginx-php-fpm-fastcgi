# OpenShift Nginx 1.6.1 PHP-FPM 5.4 Cartridge
This cartridge serves static content using nginx web server, passing requests to .php files down to php-fpm.

Place your static files inside www/static dir, commit and push.
Place your php files inside php/ dir, commit and push.

## Usage

```bash
$ rhc app create <appname> https://reflector-getupcloud.getup.io/reflect?github=ranib/openshift-nginx-php-fpm
$ cd <appname>
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

## nginx is configured with
./configure --prefix=/usr/share/nginx --sbin-path=/usr/sbin/nginx --conf-path=/etc/nginx/nginx.conf --error-log-path=/var/log/nginx/error.log --http-log-path=/var/log/nginx/access.log --http-client-body-temp-path=/var/lib/nginx/tmp/client_body --http-proxy-temp-path=/var/lib/nginx/tmp/proxy --http-fastcgi-temp-path=/var/lib/nginx/tmp/fastcgi --http-uwsgi-temp-path=/var/lib/nginx/tmp/uwsgi --http-scgi-temp-path=/var/lib/nginx/tmp/scgi --pid-path=/var/run/nginx.pid --lock-path=/var/lock/subsys/nginx --user=nginx --group=nginx --with-file-aio --with-ipv6 --with-http_ssl_module --with-http_realip_module --with-http_addition_module --with-http_xslt_module --with-http_image_filter_module --with-http_geoip_module --with-http_sub_module --with-http_dav_module --with-http_flv_module --with-http_mp4_module --with-http_gzip_static_module --with-http_random_index_module --with-http_secure_link_module --with-http_degradation_module --with-http_stub_status_module --with-mail --with-mail_ssl_module --with-debug --add-module=../headers-more-nginx-module-0.25 --add-module=../echo-nginx-module-0.53 --add-module=../ngx_cache_purge-2.1 --with-pcre=../pcre-8.35
