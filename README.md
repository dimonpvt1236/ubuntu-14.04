apache-php
===================================

A Docker image based on Ubuntu 14.04, serving the old PHP 5.5.9 running as Apache Module. Useful for Web developers in need for an old PHP version. In addition, the `error_reporting` setting in php.ini is configurable per container via environment variable.

Tags
-----

* latest: Ubuntu 14.04 (LTS), Apache 2.4.7, PHP 5.5.9 with support for setting `error_reporting`

Usage
------

```
$ docker run -d -P dimonpvt1236/ubuntu-14.04
```

With all the options:

```bash
$ docker run -d -p 8080:80 \
    -v /home/user/webroot:/var/www \
    -e PHP_ERROR_REPORTING='E_ALL & ~E_STRICT' \
    dimonpvt1236/ubuntu-14.04
```

* `-v [local path]:/var/www` maps the container's webroot to a local path
* `-p [local port]:80` maps a local port to the container's HTTP port 80
* `-e PHP_ERROR_REPORTING=[php error_reporting settings]` sets the value of `error_reporting` in the php.ini files.

### Access apache logs

Apache is configured to log both access and error log to STDOUT. So you can simply use `docker logs` to get the log output:

`docker logs -f container-id`


Installed packages
-------------------
* Ubuntu Server 14.04, based on ubuntu docker image
* apache2
* php5
* php5-cli
* libapache2-mod-php5
* php5-gd
* php5-ldap
* php5-mysql
* php5-pgsql

Configurations
----------------

* Apache: .htaccess-Enabled in webroot (mod_rewrite with AllowOverride all)
* php.ini:
  * display_errors = On
  * error_reporting = E_ALL & ~E_DEPRECATED & ~E_NOTICE (default, overridable per env variable)
