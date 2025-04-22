#MX - автотесты notsolitesrv, nwsmtp.

1) Чекаутим https://a.yandex-team.ru/arcadia/mail/java/mx
2) Экспортим путь до java8: export JAVA_HOME=<path>/jdk
3) Собираем проект mvn clean compile
4) Настроить idea: https://wiki.yandex-team.ru/testirovanie/functesting/communication/automation-setup/
5) При запуске не забываем указывать проперти, например:
`
 -ea
 -Dis.local.debug=true
 -Dlog.version=local
 -Dmx.port=25
 -Dmx.server=nw_host
 -Dnsls.host=nsls_host
 -Dnsls.port=1234
 -Dtesting.scope=pg
`
5)  Запросить: доступ до секретов, дырки до тестовых хостов

###Тестирование nwsmtp

1. Джоба для запуска: https://common.jenkins.mail.yandex.net/view/Delivery/job/nwsmtp-aqua/
2. Для тестов mxback-out: необходимо выставить проперти mx.port=27
3. Для тестов smtp кластеров: необходимо выставить проперти use.tls=true

###Тестирование notsolitesrv

1. Джоба для запуска: https://common.jenkins.mail.yandex.net/view/Delivery/job/notsolitesrv-aqua/


### Деплой изменений(джоба)

1. Джоба для деплоя: https://common.jenkins.mail.yandex.net/view/Delivery/job/build-aqua/

### Деплой изменений(консоль)

1. Деплоим: mvn clean install deploy -P production,aqua-report,aqua-report-archive
