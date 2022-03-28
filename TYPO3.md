# Ubuntu 20.04♥中的TYPO3 —— TYPO3

**推荐使用TYPO3 v11/10**

安装GraphicsMagick/ImageMagick，推荐GraphicsMagick

    apt install graphicsmagick

编辑站点配置文件`/etc/nginx/conf.d/domain.tld.conf`

    server {
        ...
        location / {
            try_files $uri $uri/ /index.php$is_args$args;
        }

        location = /typo3 {
            rewrite ^ /typo3/;
        }

        location /typo3/ {
            absolute_redirect off;
            try_files $uri /typo3/index.php$is_args$args;
        }

        location ~ [^/]\.php(/|$) {
            ...
            fastcgi_buffer_size 32k;
            fastcgi_buffers 8 16k;
            fastcgi_connect_timeout 240s;
            fastcgi_read_timeout 240s;
            fastcgi_send_timeout 240s;
        }
    }

重启Nginx

    service nginx restart


新建PHP配置文件`/etc/php/7.4/mods-available/typo3.ini`

    ; configuration for typo3
    ; priority=30
    max_execution_time=240
    max_input_vars=1500

启用配置文件并重启PHP-FPM服务

    phpenmod typo3
    service php7.4-fpm restart

从[TYPO3官网](https://get.typo3.org/)下载最新版本（以v11.5.1例）至`/var/www/`并解压

    cd /var/www/
    wget --content-disposition get.typo3.org/11
    tar xzf typo3_src-11.5.1.tar.gz

安装前的准备工作

    cd /var/www/domain.tld/httpdocs
    ln -fs /var/www/typo3_src-11.5.1 typo3_src
    ln -fs typo3_src/index.php
    ln -fs typo3_src/typo3
    chown -R www-data:www-data *
    touch FIRST_INSTALL

创建数据库相关记录

    mysql -uroot
    CREATE USER typo3 IDENTIFIED BY 'password';
    CREATE DATABASE domain DEFAULT CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;
    GRANT ALL ON domain.* TO 'typo3';

浏览器访问`http://domain.tld`进行后续安装。

[<< 返回](README.md)