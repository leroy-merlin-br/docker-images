# Leroy Merlin Brasil - Docker Images

## PHP
### Supported tags and respective `Dockerfile` links
-	[`7.4`, `latest` (*php/7.4/Dockerfile*)](https://github.com/leroy-merlin-br/docker-images/blob/master/php/7.4/Dockerfile)
-	[`7.4-apache`, `apache` (*php/7.4-apache/Dockerfile*)](https://github.com/leroy-merlin-br/docker-images/blob/master/php/7.4-apache/Dockerfile)
-	[`7.4-fpm`, `fpm` (*php/7.4-fpm/Dockerfile*)](https://github.com/leroy-merlin-br/docker-images/blob/master/php/7.4-fpm/Dockerfile)
-	[`7.4-fpm-nginx`, `fpm-nginx` (*php/7.4-fpm-nginx/Dockerfile*)](https://github.com/leroy-merlin-br/docker-images/blob/master/php/7.4-fpm-nginx/Dockerfile)
-	[`7.3` (*php/7.3/Dockerfile*)](https://github.com/leroy-merlin-br/docker-images/blob/master/php/7.3/Dockerfile)
-	[`7.3-apache` (*php/7.3-apache/Dockerfile*)](https://github.com/leroy-merlin-br/docker-images/blob/master/php/7.3-apache/Dockerfile)
-	[`7.3-fpm` (*php/7.3-fpm/Dockerfile*)](https://github.com/leroy-merlin-br/docker-images/blob/master/php/7.3-fpm/Dockerfile)
-	[`7.3-fpm-nginx` (*php/7.3-fpm-nginx/Dockerfile*)](https://github.com/leroy-merlin-br/docker-images/blob/master/php/7.3-fpm-nginx/Dockerfile)

### How to use this image

Please refer to the [official PHP image documentation.](https://github.com/docker-library/docs/blob/master/php/README.md)

Our images contain `mongodb`, `pcntl` and `zip` extensions. Also `git` and `composer` are already installed.

Also, one big difference for the `apache` version is that the default container user is `www-data`.
Apache is configured to run as `www-data` on port `80`.
By doing this, we ensure correct file permissions on shared folders between host and container.

To customize the image, if you neet `root` permissions, you must change your user to `root`.
For example:

```dockerfile
FROM leroymerlinbr/php:apache

USER root

RUN apt-get update -qq \
  && apt-get install -qq --no-install-recommends \
    libfreetype6-dev \
    libjpeg62-turbo-dev \
    libpng-dev \
 && docker-php-ext-install -j$(nproc) iconv \
 && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
 && docker-php-ext-install -j$(nproc) gd

USER www-data
```

The other difference is that we already configured a `env` for `DocumentRoot`,
so to change the default `DocumentRoot` in Apache (away from `/var/www/html`):

```dockerfile
FROM leroymerlinbr/php:7.1-apache

ENV APACHE_DOCUMENT_ROOT /path/to/new/root
```
(The `env` can then be modified at container runtime as well.)

## License

View [PHP license information](http://php.net/license/) for the software contained in this image.

As with all Docker images, these likely also contain other software which may be under other licenses (such as Bash, etc from the base distribution, along with any direct or indirect dependencies of the primary software being contained).

The PHP images are based on [official PHP docker image](https://hub.docker.com/_/php).

This repository is licensed under [MIT](LICENSE).


## Deprecation notice
THIS REPOSITORY AND IMAGES WILL BE DEPRECATED ON AUGUST 2021.
THE TEAM WILL KEEP SUPPORTING PHP CUSTOM IMAGES IN DOCKER HUB BUT IN A PRIVATE REPOSITORY.