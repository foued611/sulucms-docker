FROM php:7.0-fpm

RUN apt-get update \
    && apt-get install -y \
    curl libicu-dev libbz2-dev libxslt-dev \
    libmcrypt-dev libpspell-dev libxml2-dev \
    libzzip-dev zlib1g-dev libssl-dev \
    libldap2-dev libmagickwand-dev libgd2-xpm-dev \
    libgd-dev libfreetype6-dev libjpeg62-turbo-dev \
    libpng12-dev bzip2 openjdk-7-jdk \
    openssh-server g++ supervisor \
    git ant vim \
    --no-install-recommends --fix-missing \
    && rm -r /var/lib/apt/lists/*

RUN docker-php-ext-install \
    bcmath bz2 calendar dba \
    exif ftp gettext pcntl pdo_mysql \
    opcache intl sockets mcrypt xsl \
    mysqli pspell soap wddx xmlrpc zip

RUN pecl install -f imagick redis xdebug \
    && docker-php-ext-enable imagick redis xdebug

RUN docker-php-ext-configure gd \
    --enable-gd-native-ttf \
    --with-jpeg-dir=/usr/include/ \
    --with-png-dir=/usr/include/ \
    --with-freetype-dir=/usr/include/ \
    && docker-php-ext-install gd

RUN docker-php-ext-configure ldap \
    --with-libdir=lib/x86_64-linux-gnu \
    && docker-php-ext-install ldap

RUN curl -sS https://getcomposer.org/installer | php \
    && mv composer.phar /usr/local/bin/composer

RUN usermod -u 1000 www-data \
    && echo "    IdentityFile /home/www-data/.ssh/id_rsa" >> /etc/ssh/ssh_config

RUN curl -sL https://deb.nodesource.com/setup_7.x | bash \
    && apt-get install -y nodejs

WORKDIR /var/www/

ENV PATH /var/www/node_modules:$PATH

RUN npm install -g gulp yarn

ADD ./php.ini /usr/local/etc/php/conf.d/php.ini
ADD ./www.conf /usr/local/etc/php-fpm.d/www.conf

USER www-data

CMD ["php-fpm"]

EXPOSE 9000
