# Ubuntu 20.04♥中的TYPO3 —— 站点配置

**以下内容仅作为参考**

创建站点根目录`/var/www/domain.tld/httpdocs/`

    mkdir -p /var/www/domain.tld/httpdocs

设置用户和用户组

    chown -R www-data:www-data /var/www/domain.tld/httpdocs

新建配置文件`/etc/php/7.4/fpm/pool.d/zzz.conf`（加载顺序需在`www.conf`之后）

    [www]
    listen.owner = nginx
    listen.group = nginx

重启PHP-FPM

    service php7.4-fpm restart

新建站点配置文件`/etc/nginx/conf.d/domain.tld.conf`

    server {
        listen 80;
        server_name domain.tld;

        access_log /var/www/domain.tld/access.log;
        error_log /var/www/domain.tld/error.log;

        root /var/www/domain.tld/httpdocs/;
        index index.html index.htm index.php;

        location ~ [^/]\.php(/|$) {
            fastcgi_split_path_info ^(.+?\.php)(/.*)$;
            if (!-f $document_root$fastcgi_script_name) {
                return 404;
            }

            fastcgi_param HTTP_PROXY "";
            fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
            fastcgi_pass unix:/run/php/php7.4-fpm.sock;
            fastcgi_index index.php;

            include fastcgi_params;
        }
    }

重启Nginx

    service nginx restart

详细配置请参考[站点配置（完整版）](Site/Configuration.md)

[>> TYPO3](TYPO3.md)