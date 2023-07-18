# Ubuntu 22.04♥中的TYPO3 —— 资源压缩

修改站点配置文件`/etc/nginx/conf.d/domain.tld.conf`

    server {
        ...
        location ~ \.js\.gzip$ {
            add_header Content-Encoding gzip;
            gzip off;
            types { text/javascript gzip; }
        }
        location ~ \.css\.gzip$ {
            add_header Content-Encoding gzip;
            gzip off;
            types { text/css gzip; }
        }
    }

重启Nginx

    service nginx restart

[<< 返回](../README.md)