FROM php:7.4-fpm

# 安装必要的软件包，用于编译 PHP 扩展
RUN apt-get update && apt-get install -y \
        git \
        zlib1g-dev \
        libpcre3-dev \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libpng-dev \
        libwebp-dev \
        libxml2-dev \
        libssl-dev \
        && docker-php-ext-configure pdo_mysql --with-pdo-mysql=mysqlnd \
        && docker-php-ext-install pdo_mysql

# 下载并安装 Tideways
RUN git clone https://github.com/tideways/php-xhprof-extension.git /usr/src/php/ext/tideways \
    && cd /usr/src/php/ext/tideways \
    && phpize \
    && ./configure \
    && make \
    && make install \
    && echo "extension=tideways.so" > /usr/local/etc/php/conf.d/20-tideways.ini

# 清理安装缓存
RUN apt-get purge -y --auto-remove -o APT::AutoRemove::RecommendsImportant=false \
    && rm -rf /var/lib/apt/lists/*

# 启动 PHP-FPM
CMD ["php-fpm"]
