# Ubuntu 20.04♥中的TYPO3 —— 页面压缩

新建GZzip配置文件`/etc/nginx/conf.d/gzip.conf`

    gzip on;
    gzip_comp_level 5;
    gzip_min_length 1K;
    gzip_proxied any;
    gzip_vary on;
    gzip_types
        application/atom+xml
        application/javascript
        application/json
        application/ld+json
        application/manifest+json
        application/rdf+xml
        application/rss+xml
        application/schema+json
        application/vnd.geo+json
        application/vnd.ms-fontobject
        application/x-font-ttf
        application/x-javascript
        application/x-web-app-manifest+json
        application/xhtml+xml
        application/xml
        font/eot
        font/opentype
        image/bmp
        image/svg+xml
        image/vnd.microsoft.icon
        image/x-icon
        text/cache-manifest
        text/css
        text/html
        text/javascript
        text/plain
        text/vcard
        text/vnd.rim.location.xloc
        text/vtt
        text/x-component
        text/x-cross-domain-policy
        text/xml;

重启Nginx

    service nginx restart

*详细配置以[官方文档](http://nginx.org/en/docs/http/ngx_http_gzip_module.html)为准*

[<< 返回](../README.md)