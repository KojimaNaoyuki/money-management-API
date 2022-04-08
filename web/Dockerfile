FROM php:8.0-apache

# phpの設定ファイルとhttpdの設定ファイルをコンテナ内に設コピー
COPY ./php/php.ini /usr/local/etc/php/
COPY ./apache/000-default.conf /etc/apache2/sites-enabled/

RUN apt-get update

# Laravelプロジェクト作成に必要なパッケージをインストール
RUN apt -y install git unzip

# phpで必要なモノをインストール
RUN docker-php-ext-install pdo_mysql mysqli

# composerのインストール
RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" \
    && php -r "if (hash_file('sha384', 'composer-setup.php') === '906a84df04cea2aa72f40b5f787e49f22d4c2f19492ac310e8cba5b96ac8b64115ac402c8cd292b8a03482574915d1a8') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;" \
    && php composer-setup.php \
    && php -r "unlink('composer-setup.php');" \
    && mv composer.phar /usr/local/bin/composer

#Laravelプロジェクトの作成
RUN composer create-project laravel/laravel --prefer-dist money-management-API