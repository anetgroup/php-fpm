FROM php:7.0-fpm

RUN apt-get update && \
  DEBIAN_FRONTEND=noninteractive apt-get install -y \
    libfreetype6-dev \
    libjpeg62-turbo-dev \
    libmcrypt-dev \
    libpng12-dev \
    libbz2-dev \
    libxml2-dev \
    git \
    zip \
    unzip \
    netcat \
  && rm -r /var/lib/apt/lists/*

RUN docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/
RUN docker-php-ext-install mysqli gd pdo_mysql opcache soap

RUN pecl install -o -f redis \
  &&  rm -rf /tmp/pear \
  &&  echo "extension=redis.so" > /usr/local/etc/php/conf.d/redis.ini

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer
RUN composer global require hirak/prestissimo

RUN echo "date.timezone=Europe/Prague" > /usr/local/etc/php/conf.d/datetime.ini
RUN echo "memory_limit = -1" > /usr/local/etc/php/conf.d/memory_limit.ini
RUN echo "max_execution_time = 300" > /usr/local/etc/php/conf.d/max_execution_time.ini
