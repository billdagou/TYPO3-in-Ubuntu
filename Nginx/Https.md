# Ubuntu 24.04♥中的TYPO3 —— HTTPS

修改站点配置文件`/etc/nginx/conf.d/domain.tld.conf`

    server {
        listen 443 ssl;
        ssl_certificate /path/to/ssl/certificate.crt;
        ssl_certificate_key /path/to/ssl/certificate.key;
        ...
    }

重启Nginx

    service nginx restart

*实际配置以[官方文档](http://nginx.org/en/docs/http/converting_rewrite_rules.html)为准*

[<< 返回](../README.md)