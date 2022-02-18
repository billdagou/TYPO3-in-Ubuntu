# Ubuntu 20.04♥中的TYPO3 —— 资源缓存

新建缓存配置文件`/etc/nginx/conf.d/expires.conf`

    map $sent_http_content_type $expires {
        default 1M;
        
        text/css                              1y;
        
        application/json                      0s;
        application/ld+json                   0s;
        application/schema+json               0s;
        application/vnd.geo+json              0s;
        application/xml                       0s;
        text/xml                              0s;
    
        image/vnd.microsoft.icon              1w;
        image/x-icon                          1w;
    
        text/x-component                      1M;
    
        text/html                             0s;
    
        application/javascript                1y;
        application/x-javascript              1y;
        text/javascript                       1y;
    
        application/manifest+json             1w;
        application/x-web-app-manifest+json   0s;
        text/cache-manifest                   0s;
    
        audio/ogg                             1M;
        image/bmp                             1M;
        image/gif                             1M;
        image/jpeg                            1M;
        image/png                             1M;
        image/svg+xml                         1M;
        image/webp                            1M;
        video/mp4                             1M;
        video/ogg                             1M;
        video/webm                            1M;
    
        application/atom+xml                  1h;
        application/rdf+xml                   1h;
        application/rss+xml                   1h;
    
        application/vnd.ms-fontobject         1M;
        font/eot                              1M;
        font/opentype                         1M;
        application/x-font-ttf                1M;
        application/font-woff                 1M;
        application/x-font-woff               1M;
        font/woff                             1M;
        application/font-woff2                1M;
    
        text/x-cross-domain-policy            1w;
    }
    expires $expires;

重启Nginx

    service nginx restart

*详细配置以[官方文档](http://nginx.org/en/docs/http/ngx_http_headers_module.html#expires)为准*

[<< 返回](../README.md)