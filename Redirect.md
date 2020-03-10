# Ubuntu 18.04♥中的TYPO3 —— 页面重定向

修改站点配置文件`/etc/nginx/conf.d/domain.tld.conf`

    server {
        listen 80;
        server_name domain.tld;
        return 301 http://www.domain.tld$request_uri;
    }
    
    server {
        listen 80;
        server_name www.domain.tld;
        ...
    }

重启Nginx

    service nginx restart

*实际配置以[官方文档](http://nginx.org/en/docs/http/ngx_http_rewrite_module.html#return)为准*

[<< 返回](README.md)