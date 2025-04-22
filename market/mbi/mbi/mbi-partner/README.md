## Локальный запуск из IDEA
##### Use classpath of module
`mbi-partner`

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
-Djava.library.path=<каталог проекта ya idea>/dlls
-Djava.awt.headless=true
```
Последний параметр нужен, чтобы загрузить нативную библиотеку tickek_parser2 для Tvm. Нужно указать каталог, в котором был сгенерирован проект через ya ide idea.

Для локального запуска с datasources-ng-dev
Надо настроить креденшиалы для доступа. Для этого в ~/.bash_profile (для Ubuntu в ~/.profile) на ноутбуке пишем следующие строки:
```
export ETCD_USERNAME=datasources_read_all
export ETCD_PASSWORD="<password>"
```
1. <password> (и, если надо, username) нужно взять из конфигов confd с дев машинки. Например, с помощью такой команды: ssh aida "sudo cat /etc/confd/confd.toml".
2. Перезапускаем IDEA!
3. Проверяем, что в настройках IDEA стоит галка Build tools -> Gradle -> Delegate IDE build/run actions to Gradle

при проблемах с ipv6 на маках делаем ```sudo ifconfig awdl0 down```, либо подключаемся по сетевому кабелю


##### Before launch
Канонично `gradle build`, но с идеевским `Build` тоже работает и даже собирается/запускается несколько быстрее,
плюс можно использовать hot swap классов.

## Выкладка приложения на сервер

[Подоробнее о параметрах и их назначении можно почитать на вики](https://wiki.yandex-team.ru/market/development/java/mbuild/application-plugin/#structure)

Выложить приложение на *braavos* можно командой из корня репозитория:
```
./uploadToDev.sh partner-api
```

После этого приложение будет расположено на сервере *braavos* по пути ```~/dev/mbi-partner/```

Для запуска приложения из директории на сервере нужно вызвать ```bin/mbi-partner-start.sh```.
Приложение будет запущено в текущем процессе терминала и чтобы его остановить можно послать терминалу сигнал ```Ctrl+C```.
Закрытие терминала также вызовет остановку приложения, чтобы этого не происходило - приложение можно запускать из ```screen``` или командой ```nohup bin/mbi-partner-start.sh &```
