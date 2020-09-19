FROM centos:centos8

# apache, phpパッケージなどを導入
RUN dnf -y update
# RUN dnf -y install httpd
# RUN dnf install -y php php-mbstring php-xml php-xmlrpc php-gd php-pdo php-mysqlnd php-json php-fpm
RUN dnf -y install \
  sudo
  wget
  mysql
  zip unzip

# inatall httpd
RUN dnf -y install httpd httpd-tools

# apache設定ファイル
RUN mv /etc/httpd/conf/httpd.conf /etc/httpd/conf/httpd.conf.default
COPY httpd.conf /etc/httpd/conf/httpd.conf

# install epel-release
RUN dnf -y install epel-release

# install dev tool
RUN dnf -y groupinstall "Development Tools"
RUN dnf -y install git vim zsh curl

# install remi repo
RUN dnf -y install https://rpms.remirepo.net/enterprise/remi-release-8.rpm

# install php73
RUN \
  dnf -y install \
    php73-php \
    php73-php-mbstring \
    php73-php-common \
    php73-php-xml \
    php73-php-mysqlnd \
    php73-php-pdo \
    php73-php-gd \
    php73-php-cli \
    php73-php-intl \
    php73-php-opcache --nogpgcheck \
    php73-php-json \
    php73-php-pecl-xdebug \
    php73-php-zip

RUN ln -s /bin/php73 /bin/php

# clear dnf cache
RUN dnf clean all

# PHPをモジュール版に変更
RUN mv /etc/httpd/conf.modules.d/00-mpm.conf /etc/httpd/conf.modules.d/00-mpm.conf.default
COPY 00-mpm.conf /etc/httpd/conf.modules.d/00-mpm.conf

# PHP設定ファイル(エラー表示させるように)
RUN mv /etc/opt/remi/php73/php.ini /etc/opt/remi/php73/php.ini.default
COPY php.ini /etc/opt/remi/php73/php.ini

# composerのインストール
RUN curl -sS https://getcomposer.org/installer | php
RUN mv composer.phar /usr/local/bin/composer

# symfonyのCLIインストール
RUN wget https://get.symfony.com/cli/installer -O - | bash
RUN echo 'export PATH="$HOME/.symfony/bin:$PATH"' >> ~/.bash_profile

# oilコマンド(FuelPHPのCLI)インストール
RUN curl https://get.fuelphp.com/oil | sh

CMD ["/usr/sbin/httpd","-D","FOREGROUND"]

WORKDIR /var/www/html