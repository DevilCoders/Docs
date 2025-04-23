The documetation
================

If you want build the package, follow to sandbox service and use YA_PACKAGE task

Contain:

 - config
 - slave/master
 - latency
 - slb
 - slavelag send to graphite
 - some MySQL metrics from 'SHOW GLOBAL STATUS;' send to graphite


`src/mysql_monitoring.conf`

**Monrun**: /etc/monrun/conf.d/mysql_monitoring.conf


`src/monitoring_client.conf`

**Config for script**: /etc/yandex/cs-mysql-monitoring/default.conf


`src/mysql_monitoring.py`

**Monitoring script**: /usr/lib/config-monitoring-market/mysql_monitoring


**Default users**:

`GRANT REPLICATION CLIENT ON *.* TO 'monitor'@'localhost' IDENTIFIED BY PASSWORD '*1975D095AC033CAF4E1BF94F7202A9BBFEEB66F1';`


**All MySQL metrics**:

http://dev.mysql.com/doc/refman/5.5/en/server-status-variables.html
