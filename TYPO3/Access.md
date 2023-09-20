# Ubuntu 22.04♥中的TYPO3 —— 访问权限

修改站点配置文件`/etc/nginx/conf.d/domain.tld.conf`

    server {
        ...
        # Prevent clients from accessing hidden files (starting with a dot)
        # This is particularly important if you store .htpasswd files in the site hierarchy
        # Access to `/.well-known/` is allowed.
        # https://www.mnot.net/blog/2010/04/07/well-known
        # https://tools.ietf.org/html/rfc5785
        location ~* /\.(?!well-known\/) {
            deny all;
        }
    
        # Prevent clients from accessing to backup/config/source files
        location ~* (?:\.(?:bak|conf|dist|fla|in[ci]|log|psd|sh|sql|sw[op])|~)$ {
            deny all;
        }
    
        # TYPO3 - Block access to composer files
        location ~* composer\.(?:json|lock) {
            deny all;
        }
    
        # TYPO3 - Block access to flexform files
        location ~* flexform[^.]*\.xml {
            deny all;
        }
    
        # TYPO3 - Block access to language files
        location ~* locallang[^.]*\.xlf {
            deny all;
        }
    
        # TYPO3 - Block access to static typoscript files
        location ~* ext_conf_template\.txt|ext_typoscript_constants\.(?:txt|typoscript)|ext_typoscript_setup\.(?:txt|typoscript) {
            deny all;
        }
    
        # TYPO3 - Block access to miscellaneous protected files
        location ~* /.*\.(?:bak|co?nf|cfg|ya?ml|ts|typoscript|dist|fla|in[ci]|log|sh|sql)$ {
            deny all;
        }
    
        # TYPO3 - Block access to recycler and temporary directories
        location ~ _(?:recycler|temp)_/ {
            deny all;
        }
    
        # TYPO3 - Block access to configuration files stored in fileadmin
        location ~ fileadmin/(?:templates)/.*\.(?:txt|ts|typoscript)$ {
            deny all;
        }
    
        # TYPO3 - Block access to libaries, source and temporary compiled data
        location ~ ^(?:vendor|typo3_src|typo3temp/var) {
            deny all;
        }
    
        # TYPO3 - Block access to protected extension directories
        location ~ (?:typo3conf/ext|typo3/sysext|typo3/ext)/[^/]+/(?:Configuration|Resources/Private|Tests?|Documentation|docs?)/ {
            deny all;
        }
    }

重启Nginx

    service nginx restart

[<< 返回](../README.md)