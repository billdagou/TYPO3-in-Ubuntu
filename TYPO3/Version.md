# Ubuntu 22.04♥中的TYPO3 —— 版本文件

修改站点配置文件`/etc/nginx/conf.d/domain.tld.conf`

    server {
        ...
        if (!-e $request_filename) {
            rewrite ^/(.+)\.(\d+)\.(php|js|css|png|jpg|gif|gzip)$ /$1.$3 last;
        }
    }

重启Nginx

    service nginx restart

[<< 返回](../README.md)