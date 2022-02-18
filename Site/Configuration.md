# Ubuntu 20.04♥中的TYPO3 —— 站点配置（完整）

新建站点配置文件`/etc/nginx/conf.d/domain.tld.conf`

    server {
        listen 80;
        server_name domain.tld;
        return 301 https://www.domain.tld$request_uri;
    }

    server {
        listen 443 ssl;
        server_name www.domain.tld;

        access_log /var/www/domain.tld/access.log;
        error_log /var/www/domain.tld/error.log;

        root /var/www/domain.tld/httpdocs;
        index index.html index.htm index.php;

        ssl_certificate /path/to/ssl/certificate.crt;
        ssl_certificate_key /path/to/ssl/certificate.key;

        location ~ _(?:recycler|temp)_/ {
            deny all;
        }
        location ~ fileadmin/(?:templates)/.*\.(?:txt|ts|typoscript)$ {
            deny all;
        }
        location ~ ^(?:vendor|typo3_src|typo3temp/var) {
            deny all;
        }
        location ~ (?:typo3conf/ext|typo3/sysext|typo3/ext)/[^/]+/(?:Configuration|Resources/Private|Tests?|Documentation|docs?)/ {
            deny all;
        }

        location ~* (?i:^\.|^#.*#|^(?:ChangeLog|ToDo|Readme|License)(?:\.md|\.txt)?|^composer\.(?:json|lock)|^ext_conf_template\.txt|^ext_typoscript_constants\.txt|^ext_typoscript_setup\.txt|flexform[^.]*\.xml|locallang[^.]*\.(?:xml|xlf)|\.(?:bak|co?nf|cfg|ya?ml|ts|typoscript|tsconfig|dist|fla|in[ci]|log|sh|sql(?:\..*)?|sqlite(?:\..*)?|sw[op]|git.*|rc)|.*~)$ {
            deny all;
        }

        location ~* \.(?:git|svn|hg) {
            deny all;
        }

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
            fastcgi_split_path_info ^(.+?\.php)(/.*)$;
            if (!-f $document_root$fastcgi_script_name) {
                return 404;
            }

            fastcgi_buffer_size 32k;
            fastcgi_buffers 8 16k;
            fastcgi_connect_timeout 240s;
            fastcgi_read_timeout 240s;
            fastcgi_send_timeout 240s;

            fastcgi_param HTTP_PROXY "";
            fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
            fastcgi_pass unix:/run/php/php7.4-fpm.sock;
            fastcgi_index index.php;

            include fastcgi_params;

            fastcgi_param TYPO3_CONTEXT Production;
        }
    }

重启Nginx

    service nginx restart

参考文档：
* [站点配置](../Site.md)
* [站点重定向](../Nginx/Redirect.md)
* [HTTPS](../Nginx/Https.md)
* [应用上下文](../TYPO3/ApplicationContext.md)
* [访问权限](../TYPO3/Access.md)

[<< 返回](../README.md)