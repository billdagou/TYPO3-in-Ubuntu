# Ubuntu 18.04♥中的TYPO3 —— 文件上传

新建/修改PHP配置文件`/etc/php/7.2/mods-available/php.ini`

    ; configuration for php
    ; priority=30
    memory_limit=128M
    post_max_size=16M
    upload_max_filesize=16M

启用配置文件并重启PHP-FPM服务

    phpenmod php
    service php7.2-fpm restart

新建Nginx配置文件`/etc/nginx/conf.d/nginx.conf`

    client_max_body_size 16M;

重启Nginx

	service nginx restart

[<< 返回](README.md)