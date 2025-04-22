## Локальный запуск из IDEA
##### Use classpath of module
`mbi-shop-tms`

##### Main class
`ru.yandex.common.util.application.XmlAppContextMain`

##### Working directory
`$MODULE_WORKING_DIR$`

##### VM-options
```
-Dspring.profiles.active=development,transparent_security_filter
-Dservant.home.dir=src/main/properties.d
-Dspring.context.initializers=ru.yandex.market.core.initializer.LocalStartContextInitializer
-Dhttp.port=<your port>
```

Для локального запуска с datasources-ng-dev
Надо настроить креденшиалы для доступа. Для этого в ~/.bash_profile (для Ubuntu в ~/.profile) на ноутбуке пишем следующие строки:
```
export ETCD_USERNAME=datasources_read_all
export ETCD_PASSWORD="<password>"
```
1. \<password> (и, если надо, username) нужно взять из конфигов confd с дев машинки. Например, с помощью такой команды: ssh aida "sudo cat /etc/confd/confd.toml".
2. Перезапускаем IDEA!
3. Проверяем, что в настройках IDEA стоит галка Build tools -> Gradle -> Delegate IDE build/run actions to Gradle

при проблемах с ipv6 на маках делаем ```sudo ifconfig awdl0 down```, либо подключаемся по сетевому кабелю
