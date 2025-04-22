## Локальный запуск из IDEA
### Use classpath of module
`mbi-billing`

### Main class
`ru.yandex.common.util.application.XmlAppContextMain`

### Working directory
`$MODULE_WORKING_DIR$` - эту переменную необходимо добавить в поле
`working directory`

### VM-options
```
-Djava.library.path=<каталог проекта ya idea>/dlls
-Djna.library.path=<каталог проекта ya idea>/dlls
-Dspring.profiles.active=development,transparent_security_filter
-Dservant.home.dir=src/main/properties.d
-Dspring.context.initializers=ru.yandex.market.core.initializer.LocalStartContextInitializer
-Dsimple.host.name="$(/bin/hostname -f)"
-Dlog.dir=../logs/
```

Для локального запуска с datasources-ng-dev
Надо настроить креденшиалы для доступа. Для этого в ~/.bash_profile (для Ubuntu в ~/.profile) на ноутбуке пишем следующие строки:
```
export ETCD_USERNAME=datasources_read_all
export ETCD_PASSWORD="<password>"
```
1. &lt;password> (и, если надо, username) нужно взять из конфигов confd с дев машинки. Например, с помощью такой команды: ```ssh aida.yandex.ru "sudo cat /etc/confd/confd.toml"```.
2. Перезапускаем IDEA!
3. Проверяем, что в настройках IDEA стоит галка Build tools -> Gradle -> Delegate IDE build/run actions to Gradle
