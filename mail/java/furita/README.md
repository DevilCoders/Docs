#Автотесты YFurit-ы.

1) Клонируем проект git-ом
2) Собираем проект mvn clean compile
3) При запуске не забываем указывать проперти, т.к. серверов несколько, например:

3.1) Основной сервер (такие проперти по-умолчанию, их можно и не прописывать)
`-Dyfurita.host=furita-qa2.cmail.yandex.net
 -Dyfurita.port=80
 -Dtest.report.dir=target
 -Dis.corp=false
 -Dpassport.host=https://passport.yandex.ru/
 -Dpassport.url=passport.yandex.ru
 -Dselenium.baseURL=https://wmi-b2b.yandex.ru
 -Dmx.server=mxback-qa2.cmail.yandex.net
 -Dlog.version=local
 -Dtesting.scope=pg
 -Dis.pg=true
 -Dtesting.furita.scope=noncorp`
 
3.2) Корпоративная фурита:
`-Dyfurita.host=furita-corp-qa2.cmail.yandex.net
 -Dyfurita.port=80
 -Dtest.report.dir=target
 -Dis.corp=true
 -Dis.pg=false
 -Dpassport.host=https://passport.yandex-team.ru/
 -Dpassport.url=passport.yandex-team.ru
 -Dselenium.baseURL=https://wmicorp-qa.yandex-team.ru
 -Dmx.server=mxbackcorp-qa2.cmail.yandex.net
 -Dlog.version=local
 -Dmailboxes.yaml.file=accounts/corp.yaml
 -Dmsearch.url=http://new-msearch-proxy.mail.yandex.net:8051
 -Dmsearch.query.host=furita-qa2.cmail.yandex.net`
   или достаточно указать:
   `-Dtesting.furita.scope=corp
    -Dtesting.scope=corp
    -Dpassport.host=https://passport.yandex-team.ru/
    -Dpassport.url=passport.yandex-team.ru
    -Dselenium.baseURL=https://wmicorp2-qa.yandex-team.ru`
   
3.3) Почтовый тестинг https://wiki.yandex-team.ru/pochta/testing/
(Часто в нерабочем состоянии, надо проверять)
`-Dmx.server=mxbacktst1o.cmail.yandex.net
 -Dselenium.baseURL=https://web-tst1j.yandex.ru
 -Dpassport.url=passport-test.yandex.ru
 -Dpassport.host=https://passport-test.yandex.ru/
 -Dyfurita.host=furita.tst.cmail.yandex.net
 -Dyfurita.port=80
 -Dtest.report.dir=target
 -Dis.corp=false
 -Dlog.version=local
 -Dtesting.scope=test
 -Dmailboxes.yaml.file=accounts/testing.yaml
 -Dmsearch.url=http://mail-msearch-proxy-qa2.search.yandex.net:10430
 -Dmsearch.query.host=mxbacktst1o.cmail.yandex.net`
 
  или достаточно указать:
  `-Dtesting.furita.scope=testing
   -Dpassport.url=passport-test.yandex.ru
   -Dpassport.host=https://passport-test.yandex.ru/
   -Dselenium.baseURL=https://web-tst1j.yandex.ru
   -Dtesting.scope=test
   -Dhound.port=9090`


###Тестирование FURITA
Джоба для сборки пакета и запуска тестов:
https://jenkins.mail.yandex.net/job/mail-furita-package-install_test/

Удобно управляться со страницей и перезапускать упавшие 
http://aqua.yandex-team.ru/tools/aquaRunpack/testpers-mail-search.htm


###Полезные ссылки
Об актуальных аспектах текущего запуска тестов можно посмотреть здесь:
https://wiki.yandex-team.ru/users/alex89/Отпуск/