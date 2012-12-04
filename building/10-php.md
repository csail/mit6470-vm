# PHP Setup

This document describes installing [PHP](http://php.net/) together with the
libraries that are commonly used for Web development.


## PHP Runtime

1. Install the main PHP interpreter and the FastCGI variant.

```bash
sudo apt-get install -y php5 php5-cgi php5-cli
```

### Commentary

Using `php5-cgi` as a FastCGI server is documented in
[this blog post](http://davidwinter.me/articles/2009/06/13/php-and-nginx-the-easy-way/),
which references
[this post](http://tomasz.sterna.tv/2009/04/php-fastcgi-with-nginx-on-ubuntu/).


## PHP Libraries

1. Install commonly used PHP libraries and the
   [PEAR package manager](http://pear.php.net/).

```bash
sudo apt-get install -y php-pear php5-suhosin php5-mysql
```

### Commentary

Someone with PHP experience should review this section and replace this
paragraph with the rationale for installing whatever we end up supplying.


## Nginx Integration

1. Create a PHP5 FastCGI start-up script. (if you're not a vim user, replace
   `vim` with `nano` in the command below)

```bash
sudo vim /etc/init.d/php-fastcgi
```

1. Place the following in the file.

```
#!/bin/bash
BIND=127.0.0.1:9000
USER=www-data
PHP_FCGI_CHILDREN=15
PHP_FCGI_MAX_REQUESTS=1000

PHP_CGI=/usr/bin/php-cgi
PHP_CGI_NAME=`basename $PHP_CGI`
PHP_CGI_ARGS="- USER=$USER PATH=/usr/bin PHP_FCGI_CHILDREN=$PHP_FCGI_CHILDREN PHP_FCGI_MAX_REQUESTS=$PHP_FCGI_MAX_REQUESTS $PHP_CGI -b $BIND"
RETVAL=0

start() {
      echo -n "Starting PHP FastCGI: "
      start-stop-daemon --quiet --start --background --chuid "$USER" --exec /usr/bin/env -- $PHP_CGI_ARGS
      RETVAL=$?
      echo "$PHP_CGI_NAME."
}
stop() {
      echo -n "Stopping PHP FastCGI: "
      killall -q -w -u $USER $PHP_CGI
      RETVAL=$?
      echo "$PHP_CGI_NAME."
}

case "$1" in
    start)
      start
  ;;
    stop)
      stop
  ;;
    restart)
      stop
      start
  ;;
    *)
      echo "Usage: php-fastcgi {start|stop|restart}"
      exit 1
  ;;
esac
exit $RETVAL
```

1. Make the script executable.

```bash
sudo chmod +x /etc/init.d/php-fastcgi
```

1. Fork the default nginx site configuration.

```bash
sudo cp /etc/nginx/sites-available/default /etc/nginx/sites-available/php5
```

1. Edit the site configuration.

```bash
sudo vim /etc/nginx/sites-available/php
```

1. Change the file to have the following contents.

```
server {
  root /home/six470/php_example;
  index index.php;

  error_page 404 /404.html;
  error_page 500 502 503 504 /50x.html;

  # pass the PHP scripts to FastCGI server listening on 127.0.0.1:9000
  location ~ \.php$ {
    fastcgi_split_path_info ^(.+\.php)(/.+)$;
    fastcgi_param /home/six470/php_example
    fastcgi_pass 127.0.0.1:9000;
    fastcgi_index index.php;
    include fastcgi_params;
  }
}
```

1. Make the PHP site configuration active.

```bash
sudo ln -s /etc/nginx/sites-available/php /etc/nginx/sites-enabled/php
```

### Commentary

The following command sequence is useful for testing the PHP configuration
without requiring a reboot.

```bash
sudo /etc/init.d/php-fastcgi start
sudo /etc/init.d/nginx reload
```

The PHP site configuration is linked into `sites-enabled` because PHP is
currently MIT 6.470's default platform.
