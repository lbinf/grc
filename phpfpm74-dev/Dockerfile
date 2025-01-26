# 使用官方PHP 7.4 FPM基础镜像
FROM php:7.4-fpm

# 更新包列表并安装必要的工具
RUN apt-get update && \
    apt-get install -y \
    git \
    wget \
    curl \
    vim \
    gdb \
    tcpdump \
    libzip-dev \
    libonig-dev \
    libxml2-dev \
    libssl-dev \
    libcurl4-openssl-dev \
    libreadline-dev \
    libfreetype6-dev \
    libjpeg62-turbo-dev \
    libpng-dev \
    libicu-dev \
    libxslt1-dev \
    && rm -rf /var/lib/apt/lists/*

# 安装PHP扩展
RUN docker-php-ext-install \
    zip \
    mbstring \
    pdo_mysql \
    mysqli \
    xml \
    gd \
    intl \
    opcache \
    bcmath \
    soap \
    xsl \
    && pecl install redis && docker-php-ext-enable redis

# 安装 Xdebug
RUN #pecl install xdebug && docker-php-ext-enable xdebug

RUN pecl install xdebug-3.0.4 && docker-php-ext-enable xdebug

# 配置 Xdebug
COPY ./xdebug.ini /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini

# 安装 phptrace
RUN git clone https://github.com/Qihoo360/phptrace.git ~/phptrace
#    cd /tmp/phptrace && \
#    /usr/local/bin phpize ./configure --with-php-config=/usr/local/bin/php-config && \
#    make && make cli && make install all && \
#    echo "extension=trace.so" > /usr/local/etc/php/conf.d/phptrace.ini

# 下载并安装 swoole_loader74
#RUN wget https://example.com/path/to/swoole_loader74.so -O /usr/local/lib/php/extensions/no-debug-non-zts-20190902/swoole_loader74.so && \

COPY swoole_loader74.so    /usr/local/etc/php/conf.d/swoole_loader74.so
RUN  echo "extension=swoole_loader74.so" > /usr/local/etc/php/conf.d/swoole_loader.ini

# 安装 tcpdump
RUN apt install -y libcap2-bin && setcap cap_net_raw+ep /usr/sbin/tcpdump

# 安装并配置 Opcache GUI
RUN git clone https://github.com/amnuts/opcache-gui.git /var/www/html/opcache-gui

# 设置工作目录
WORKDIR /var/www/html

# 暴露端口
EXPOSE 9000

# 启动命令
CMD ["php-fpm"]
