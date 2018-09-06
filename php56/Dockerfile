FROM php:5.6-fpm
 
#MAINTAINER Will "Will.zhou@xiaoxiongyouxi.com"
 
#更换源 http://mirrors.163.com/.help/debian.html
#COPY sources.list /etc/apt/sources.list
 
# Install modules
# composer需要先安装zip
RUN \
apt-get update \
&& apt-get install -y --no-install-recommends \
libmcrypt-dev \
libssl-dev \
libfreetype6-dev \
libjpeg62-turbo-dev \
libpng-dev \
libcurl4-openssl-dev \
libmagickwand-dev \
libmemcached-dev \
libmemcached11 \
graphicsmagick \
libgraphicsmagick1-dev \
wget \
&& apt-get autoremove \
&& apt-get clean \
&& rm -r /var/lib/apt/lists/*
 
# install php modules
RUN \
# 安装扩展
docker-php-ext-install -j$(nproc) \
iconv mcrypt gettext curl mysqli pdo pdo_mysql zip \
mbstring bcmath opcache xml simplexml sockets hash soap \
&& docker-php-ext-configure gd \
--with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
&& docker-php-ext-install -j$(nproc) gd
 
#通过pecl安装扩展,在国内不能通过pecl安装redis和mongodb扩展，可以手动现在编译安装
RUN \
pecl install redis-3.1.0 \
&& pecl install memcached-2.2.0 \
&& pecl install xdebug-2.5.0 \
&& pecl install mongo-1.6.16 \
&& docker-php-ext-enable redis memcached xdebug mongo

RUN curl -fsSL 'https://xcache.lighttpd.net/pub/Releases/3.2.0/xcache-3.2.0.tar.gz' -o xcache.tar.gz \
    && mkdir -p xcache \
    && tar -xf xcache.tar.gz -C xcache --strip-components=1 \
    && rm xcache.tar.gz \
    && ( \
        cd xcache \
        && phpize \
        && ./configure --enable-xcache \
        && make -j$(nproc) \
        && make install \
    ) \
    && rm -r xcache \
    && docker-php-ext-enable xcache

RUN curl -fsSL 'http://pecl.php.net/get/gmagick-1.1.7RC3.tgz' -o gmagick.tgz \
    && mkdir -p gmagick \
    && tar -zxf gmagick.tgz -C gmagick --strip-components=1 \
    && rm gmagick.tgz \
    && ( \
        cd gmagick \
        && phpize \
        && ./configure --with-gmagick=/usr/local/gmagick/ \
        && make -j$(nproc) \
        && make install \
    ) \
    && rm -r gmagick \
    && docker-php-ext-enable gmagick

RUN curl -fsSL 'http://www.xunsearch.com/scws/down/scws-1.2.3.tar.bz2' -o scws.bz2 \
    && mkdir -p scws \
    && tar -xjf scws.bz2 -C scws --strip-components=1 \
    && rm scws.bz2 \
    && ( \
        cd scws \
        && ./configure --prefix=/usr/local/scws \
        && make && make install \
        && cd phpext \
        && phpize \
        && ./configure --with-scws=/usr/local/scws/ \
        && make -j$(nproc) \
        && make install \
    ) \
    && rm -r scws \
    && docker-php-ext-enable scws

 
# composer 
# composer中国镜像
# 注意：需要先安装lumen，在安装laravel，否则报错
# 不应在镜像中绑定国内的镜像，因为镜像可能会用到国外的服务器
# 测试国内的容易抽风。。
#&& curl -sS https://getcomposer.org/installer -o /composer.php \
#&& php composer.php \
#&& mv composer.phar /usr/local/bin/composer \
#&& composer config -g repo.packagist composer http://packagist.phpcomposer.com \
#&& rm -f composer.php \
#&& chmod 755 /usr/local/bin/composer \
#&& php -r "if (hash('SHA384', file_get_contents('composer-setup.php')) === 'fd26ce67e3b237fffd5e5544b45b0d92c41a4afe3e3f778e942e43ce6be197b9cdc7c251dcde6e2a52297ea269370680') { echo 'Installer verified';  } else { echo 'Installer corrupt'; unlink('composer-setup.php');  }" \
RUN cd / \
&& php -r "readfile('https://getcomposer.org/installer');" > composer-setup.php \
&& php composer-setup.php  --filename=composer  --install-dir=/usr/local/bin/ \
&& rm composer-setup.php \
&& composer clearcache \
&& composer clear-cache
 
 
# 解决时区问题
ENV TZ "Asia/Shanghai"
 
# 终端设置
# 执行php-fpm时，默认值是dumb，这时在终端操作时可能会出现：terminal is not fully functional
ENV TERM xterm
 
# Define mountable directories.
VOLUME /var/www
 
# 工作目录
WORKDIR /var/www
 
EXPOSE 9000

CMD ["php-fpm", "-F"]
