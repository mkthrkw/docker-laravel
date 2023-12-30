FROM php:8.2-rc-fpm

#ローカルにあるphp.iniをインストールしたphp.iniにコピー、上書き
COPY ./php.ini /usr/local/etc/php/php.ini

#パッケージ（git unzip libzip-dev libicu-dev libonig-dev）をインストール
#キャッシュクリア
#拡張ライブラリ（intl pdo_mysql zip bcmath）をインストール
RUN apt-get update && \
  apt-get -y install --no-install-recommends git unzip libzip-dev libicu-dev libonig-dev cron && \
  apt-get clean && \
  rm -rf /var/lib/apt/lists/* && \
  docker-php-ext-install intl pdo_mysql zip bcmath

#composer
COPY --from=composer /usr/bin/composer /usr/bin/composer

#サーバー環境変数を設定
ENV COMPOSER_ALLOW_SUPERUSER=1 \
  COMPOSER_HOME=/composer


# Node.jsをインストール
RUN curl -fsSL https://deb.nodesource.com/setup_18.x | bash
RUN apt-get install -y nodejs


#xdebugのインストール
RUN pecl install xdebug-3.2.0 \
  && docker-php-ext-enable xdebug



#cronファイルをコピーして起動
#COPY ./cron.d/ /etc/cron.d/
#RUN chmod 0644 /etc/cron.d/* &&\
#    touch /var/log/cron.log
#CMD cron -f

WORKDIR /var/www/html