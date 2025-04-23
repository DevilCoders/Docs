## Настройка TVM
Все взаимодействие с Trust'ом закрыто [TVM'ом](https://wiki.yandex-team.ru/passport/tvm2/).
При этом по client-tvm-id определяется не просто приложение, которое обращается к трасту, но и платежный терминал, по которому будет считаться выручка.
Почему так сделано - одному богу известно.

### Получение токена для локального подключения к трасту напрямую
1. Мы уже в Аркадии, поэтому достаточно настроить **ya tool** ([гайд](https://docs.yandex-team.ru/devtools/intro/quick-start-guide#ya-setup)).
2. Установить **tvmknife** ([гайд](https://wiki.yandex-team.ru/passport/tvm2/debug/#ustanovka)).
3. Сгенерировать tvm-тикет через **tvmknife**, например: `echo 'tvm_trust_autoru_secret' | ya tool tvmknife get_service_ticket client_credentials -d 2001798 -s 2032938`, где tvm_trust_autoru_secret - [секрет](https://yav.yandex-team.ru/secret/sec-01eaywqqz34nh01m6kkfa7aj11/explore/version/ver-01fv2gdxsme9cvqcek2t9rbztr) от TVM интеграции автору с трастом.
4. Полученный tvm-тикет подставлять в качестве заголовка **X-Ya-Service-Ticket** при вызове траста, например, через curl или postman.
```
curl --location --request GET 'https://trust-payments-test.paysys.yandex.net:8028/trust-payments/v2/products/boost' \
--header 'X-Ya-Service-Ticket: {tvm_ticket}'
```
### Настройка TVM для локального подключения к трасту из банкира
1. Установить библиотеку **ticket_parser2_java** в свой JDK ([гайд](https://wiki.yandex-team.ru/users/mors741/tvm-ticketparser2java-lib-from-sources/))
2. Скачать сертификат **YandexInternalRootCA**: `curl https://crls.yandex.net/YandexInternalRootCA.crt > YandexInternalRootCA.crt`
3. Установить сертификат в свой JDK: `sudo $JAVA_HOME/bin/keytool -keystore $JAVA_HOME/lib/security/cacerts -keypass changeit -storepass changeit -importcert -alias yandexinternalrootca -file ~/Downloads/YandexInternalRootCA.crt`
4. Добавить конфигурации подключения в [storage.local.conf](../../banker-dao/src/main/resources/storage.local.conf)
