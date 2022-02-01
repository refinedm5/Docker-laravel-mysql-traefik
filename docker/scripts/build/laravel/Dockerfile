FROM php:7.2-apache
MAINTAINER ikhsan demonspeedster at gmail.com
RUN apt-get update && apt-get install -y --fix-missing \
    git \
    openssl \
    apt-utils \
    zlib1g-dev \
    libzip-dev \
    libbz2-dev \
    libxml2 \
    libxml2-dev \
    bzip2 \
    libpng-dev \
    gnupg

RUN apt-get update -y && apt-get install -y libmcrypt-dev openssl libapache2-mod-security2
RUN docker-php-ext-install ctype xml json bcmath tokenizer mysqli bz2 pdo pdo_mysql gd mbstring zip && docker-php-ext-enable ctype xml json bcmath tokenizer bz2 mysqli pdo pdo_mysql gd mbstring zip
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer
RUN ln -s /etc/apache2/mods-available/rewrite.load /etc/apache2/mods-enabled/
RUN ln -s /etc/apache2/mods-available/authz_groupfile.load /etc/apache2/mods-enabled/
RUN ln -s /etc/apache2/mods-available/headers.load /etc/apache2/mods-enabled/
RUN ln -s /etc/apache2/mods-available/remoteip.load /etc/apache2/mods-enabled/
#RUN rm /etc/apache2/conf-enabled/security.conf
COPY apache2.conf /etc/apache2/
COPY modsecurity.conf /etc/modsecurity
RUN addgroup --gid 1001 corpweb
RUN gpasswd -a www-data corpweb
ENV TZ=Asia/Jakarta
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

