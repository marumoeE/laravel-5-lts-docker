# ベースイメージを設定
FROM php:7.4-fpm-buster

# SHELL設定
SHELL ["/bin/bash", "-oeux", "pipefail", "-c"]

# 環境変数設定
ENV COMPOSER_ALLOW_SUPERUSER 1
ENV COMPOSER_HOME /composer
ENV COMPOSER_MEMORY_LIMIT=-1

# Composerをインストール
RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" && \
  php composer-setup.php && \
  php -r "unlink('composer-setup.php');" && \
  mv composer.phar /usr/local/bin/composer

# Laravelに必要なパッケージをインストール(&設定など)
RUN apt-get update && \
apt-get -y install git unzip libzip-dev libicu-dev libonig-dev && \
apt-get clean && \
rm -rf /var/lib/apt/lists/* && \
docker-php-ext-install intl pdo_mysql zip bcmath

RUN apt-get update && apt-get install -y libfreetype6-dev libjpeg62-turbo-dev libmcrypt-dev libpng-dev \
    && docker-php-ext-configure gd --with-freetype --with-jpeg \
    && docker-php-ext-install -j$(nproc) gd exif

# php.ini をマウント
COPY ./php.ini /usr/local/etc/php/php.ini

# Node.jsをインストール
RUN apt-get update && \
  apt-get install -y curl gnupg
RUN curl -sL https://deb.nodesource.com/setup_12.x | bash -
RUN apt-get install -y nodejs
RUN npm install npm@latest -g

WORKDIR /work