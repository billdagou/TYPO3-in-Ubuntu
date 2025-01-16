# Ubuntu 24.04♥中的TYPO3 —— Binlog

新建binlog配置文件`/etc/mysql/mysql.conf.d/binlog.cnf`

    [mysqld]
    binlog_expire_logs_seconds = 604800

重启MySQL

    service mysql restart

*详细配置以[官方文档](https://dev.mysql.com/doc/refman/8.0/en/replication-options-binary-log.html)为准*

[<< 返回](../README.md)