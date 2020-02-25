FROM centos:centos8

RUN dnf -y update

# apache, phpパッケージなどを導入
RUN dnf -y install httpd
RUN dnf install -y php php-mbstring php-xml php-xmlrpc php-gd php-pdo php-mysqlnd php-json php-fpm
RUN dnf -y install mysql
RUN dnf -y install zip unzip


# PHPをモジュール版に変更
RUN mv /etc/httpd/conf.modules.d/00-mpm.conf /etc/httpd/conf.modules.d/00-mpm.conf.default
COPY 00-mpm.conf /etc/httpd/conf.modules.d/00-mpm.conf

# composerのインストール
RUN curl -sS https://getcomposer.org/installer | php
RUN mv composer.phar /usr/local/bin/composer

CMD ["/usr/sbin/httpd","-D","FOREGROUND"]

WORKDIR /var/www/html