# Ubuntu 20.04♥中的TYPO3 —— 访问权限

修改站点配置文件`/etc/nginx/conf.d/domain.tld.conf`

    server {
        ...
        // Access block for folders
        location ~* _(?:recycler|temp)_/ {
            deny all;
        }
        location ~* fileadmin/templates/.*\.(?:txt|ts)$ {
            deny all;
        }
        location ~* ^(?:vendor|typo3_src|typo3temp/var) {
            deny all;
        }
        location ~* (?:typo3conf/ext|typo3/sysext|typo3/ext)/[^/]+/(?:Configuration|Resources/Private|Tests?|Documentation|docs?)/ {
            deny all;
        }
        
        // Access block for files
        location ~* (?i:^\.|^#.*#|^(?:ChangeLog|ToDo|Readme|License)(?:\.md|\.txt)?|^composer\.(?:json|lock)|^ext_conf_template\.txt|^ext_typoscript_constants\.txt|^ext_typoscript_setup\.txt|flexform[^.]*\.xml|locallang[^.]*\.(?:xml|xlf)|\.(?:bak|co?nf|cfg|ya?ml|ts|typoscript|tsconfig|dist|fla|in[ci]|log|sh|sql(?:\..*)?|sqlite(?:\..*)?|sw[op]|git.*)|.*(?:~|rc))$ {
            deny all;
        }
        
        // Block access to vcs directories
        location ~* \.(?:git|svn|hg) {
            deny all;
        }
    }

重启Nginx

    service nginx restart

[<< 返回](README.md)