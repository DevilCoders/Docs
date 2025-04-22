# Stunnel

Stunnel - служба, которая необходима при проксировании запросов к внешним партнерам, использующим интеграцию с КриптоПро.

Официальная документация по конфигурированию stunnel - [тут](https://www.stunnel.org/static/stunnel.html).

Stunnel живет на squid'ах и поставляется ролью [stunnel](https://a.yandex-team.ru/arc_vcs/classifieds/infra/vertis-ansible/roles/stunnel) через ansible-pull. **Все изменения, проводимые в ручном режиме, необходимо фиксировать в роли.**

## Конфигурация

Stunnel конфигурируется через конфиг [stunnel.conf](https://a.yandex-team.ru/arc_vcs/classifieds/infra/vertis-ansible/roles/stunnel/files/etc/opt/cprocsp/stunnel/stunnel.conf)

Чтобы настроить новый туннель, необходимо добавить в конфиг новую секцию с новым портом:

```
[<tunnel name>]
client = yes
accept = :::<порт, на котором stunnel будет слушать клиентов на нашей стороне>
connect = <ipv4-адрес:порт партнера>
verify = 0
```

Можно добавить несколько строк с директивой `connect`, чтобы указать несколько ip-адресов на стороне партнера.

Если на стороне партнера работает аутентификация клиентов с помощью сертификатов, необходимо добавить следующую строку:
```
cert = <путь до файла с цепочкой сертификатов или SHA1 Thumbprint>
```

Получение SHA1 Thumbprint сертификата описана в следующей секции.

Для применения изменений необходим рестарт stunnel.

## Пошаговая инструкция по работе с сертификатами

Файлы с сертификатами и криптоконтейнерами необходимо положить в `/var/opt/cprocsp/keys/root/<tunnel name>/`

На следующем этапе необходимо установить криптоконтейнер с расширением pfx следующим образом:

`sudo /opt/cprocsp/bin/amd64/certmgr -install -pfx -file /var/opt/cprocsp/keys/root/<tunnel name>/<cryptocontainer_name.pfx> -pin <пароль от криптоконтейнера> -silent`.

Вывод данной команды также содержит SHA1 Thumbprint, который необходимо использовать при конфигурации stunnel.

Проверить корректность установки криптоконтейнера можно проверить командой `/opt/cprocsp/bin/amd64/certmgr -list`.

## Тестирование туннеля

Для проверки работоспособности туннеля необходимо использовать пропатченный `curl`. Инструкцию по его сборке можно найти [здесь](https://gist.github.com/phpdude/47eecbb61fdc2819bd60cd8d0ad725cc).

С его помощью можно сделать тестовый запрос на squid, на котором поднят stunnel, с указанием порта из `stunnel.conf` в соответствии с документацией API, которую предоставляет партнер.

Примеры запросов:
```
curl -k -H "Content-Type: application/json" \
-H "Host: bdapi.mts.ru" -v --user test:test http://squid-01-sas.test.vertis.yandex.net:4432/scoring/v1/score \
-d '{"msisdn":79854297478, "agreement": true, "features":[{"name":"f1"}]}'}
```

```
curl --location --request POST 'http://squid-01-sas.test.vertis.yandex.net:4431/collatauto' \
--header 'Content-Type: text/plain' \
--data-raw '<some data>'
```
