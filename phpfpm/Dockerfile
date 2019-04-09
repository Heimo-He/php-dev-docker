FROM  php:7.1-fpm
COPY ./conf/php.ini /usr/local/etc/php/php.ini
#    更改为阿里云镜像
RUN sed -i 's/deb.debian.org/mirrors.aliyun.com/g' /etc/apt/sources.list \
    && apt-get update && apt-get install -y \
    openssl \
    libfreetype6-dev \
    libpng-dev \
    libjpeg-dev \
    libzip-dev \
    zip \
#    需要openssl扩展取消以下注释-begin
    wget \
    && rm -rf /var/lib/apt/lists/* \
    && wget https://www.openssl.org/source/openssl-1.1.1b.tar.gz \
    && tar -xzvf ./openssl-1.1.1b.tar.gz \
    && cd openssl-1.1.1b \
    && ./config --prefix=/usr/local/ssl --openssldir=/usr/local/ssl \
    && make \
    && make install \
    && rm -rf /var/www/html/openssl-1.1.1b.tar.gz \
    && rm -rf /var/www/html/openssl-1.1.1b \
#    需要openssl扩展取消以下注释-end
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-png-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install gd \
    && docker-php-ext-install mysqli \
    && docker-php-ext-install pdo_mysql \
    && docker-php-ext-install mbstring \
    && pecl install swoole \
    && docker-php-ext-enable swoole \
    && pecl install redis \
    && docker-php-ext-enable redis