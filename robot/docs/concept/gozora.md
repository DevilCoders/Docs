# Введение

GoZora — это проект лёгкой http-прокси, призванный заменить сервис Zora Online. Основной упор сделан на простоту, надёжность и низкие накладные расходы.

Вам подойдёт Гозора, если у вас один из таких сценариев:
* Вы проксируете пользовательские запросы (например, пользователь жмёт на кнопку, а в ответ нужно послать запрос)
* Вы ходите в ограниченный набор API (например, Telegram API)
* У вас есть договорённость с сайтами, в которые вы хотите ходить

Вам **не** подойдёт Гозора, если:
* Вам нужно учитывать ограничение в robots и/или на рейт запросов к хостам — для этого нужна [Zora](https://docs.yandex-team.ru/robot/concept/zora);
* У вас батчевый процесс, то есть вам нужно качать много и часто — для этого есть батчевая инфраструктура Робота ([KwYT](https://docs.yandex-team.ru/robot/concept/kwyt-rth)/картиночная база/[Самовар](https://docs.yandex-team.ru/robot/concept/samovar)/[Zora](https://docs.yandex-team.ru/robot/concept/zora));
* Ваша библиотека не поддерживает добавление кастомных заголовков или Basic Auth — для авторизации Гозора использует TVM (например, в youtube-dl нельзя задать свои заголовки).

## Порядок подключения
* Для подключения необходимо заполнить [форму](https://forms.yandex-team.ru/surveys/60658/) и дождаться выполнения тикета.

{% cut "Форма для подключения" %}

<iframe height="700" width="100%" frameborder="0" src="https://forms.yandex-team.ru/surveys/60658/?iframe=1"></iframe> 

{% endcut %}

* Для доступа к GoZora вам понадобится TVM тикет от вашего сервиса. Для тестов и отладки можно использовать [tvmknife](https://wiki.yandex-team.ru/passport/tvm2/debug/#tvmknife). Пример: 

```js
(bash)
TVM_TICKET=$(ya tool tvmknife get_service_ticket sshkey --src <ВАШ TVM source id> --dst 2023123)
curl -v -kx http://go.zora.yandex.net:1080 --proxy-header "x-ya-service-ticket: $TVM_TICKET" --proxy-header "x-ya-client-id: <ваш clientId>" https://ya.ru/
```

Передача URL через хедер:

```js
(bash)
curl -v http://go.zora.yandex.net:1080/ -H "x-ya-dest-url: https://ya.ru/" -H "x-ya-service-ticket: $TVM_TICKET" -H "x-ya-client-id: <ваш clientId>"
```

* Убедиться, что в [Puncher](https://puncher.yandex-team.ru) заказаны дырки от вашего сервиса до [http://go.zora.yandex.net:1080](http://go.zora.yandex.net:1080).
* Если нужен источник, который умеет роторить (выполнять js на загружаемой странице), то необходимо воспользоваться этой инструкцией по подключению: [Gorotor](https://docs.yandex-team.ru/robot/concept/gozora#podklyuchenie-gorotor).

Аутентификация через Basic Auth:

```js
(bash)
GOZORA_SOURCE=my_service_name
curl -v -kx http://$GOZORA_SOURCE:$TVM_TICKET@go.zora.yandex.net:1080 https://ya.ru
curl -U $GOZORA_SOURCE:$TVM_TICKET -v -kx http://go.zora.yandex.net:1080 https://ya.ru
```

{% note warning %}

curl старых версий обрезает user/password, поэтому на старых curl команды ниже могут не работать.

{% endnote %}

## Доступ для тестинга GoZora

Для вашего тестинга не стоит использовать тестовую Gozora. Для этих целей вы можете заказать отдельные продовые источники, либо просто пользоваться одним и тем же. Обычно разные источники нужны в редких случаях: когда на графиках нужно разделять продовый и тестовый поток или если тестинг может использовать всю квоту для прода.

## GoZora Intourist
Кроме основного инстанса GoZora (http://go.zora.yandex.net:1080/) существует инстанс GoZora Intourist, в которм для скачек используются адреса не RU регионов. На текущий момент в инстансе используются адреса из регионов US, GB, FR, DE, TR.

Есть общий L3-баласер:
```js
http://gozora-intourist.zora.yandex.net:1080/
```
А так же L3-балансеры для каждого из регионов:
* us.go.zora.yandex.net
* gb.go.zora.yandex.net
* fr.go.zora.yandex.net
* de.go.zora.yandex.net
* tr.go.zora.yandex.net

## Специальные заголовки


Заголовок |Значение по умолчанию|Описание
:--- | :--- | :---
X-Yandex-Req-Id<br/>X-Yandex-ReqId<br/>**X-Ya-Req-Id**<br/>X-Ya-ReqId|-| Уникальная строка идентификатор запроса для логов
X-Ya-Ignore-Certs|false|Игнорировать невалидные сертификаты для https соединений
X-Ya-Service-Ticket|-|TVM тикет для авторизации клиента
X-Ya-Dest-Url|-|URL для скачивания. Это альтернативный способ передачи цели скачивания для библиотек не поддерживающих proxy
X-Ya-Follow-Redirects<br/>X-Yandex-Redirs (для совместимости)|false|Следование по редиректам (см. особенности поддержки редиректов)
X-Ya-Client-Id|-|Идентификатор клиента (имя источника) нужен, когда один TvmId используется для нескольких клиентов
X-Ya-User-Agent|-|Заголовок для переопределения user-agent'а

## Особенности работы редиректов
GoZora поддерживает возможность следования по редиректам X-Ya-Follow-Redirects (с помощью хедера **X-Ya-Follow-Redirects**) , но есть важные особенности:
* всем целям редиректа передаётся оригинальный запрос как есть (т. е. не учитываются куки и изменения метода запроса GET, POST, etc);
* редиректы осуществляются для всех 3xx кодов при наличии Location в response;
* если была ошибка при следование по редиректу, то возвращается последний успешно получений ответ в цепочке редиректов;
* количество редиректов в цепочке ограничено — 10 редиректами.
## Графики 

<iframe height="700" width="100%" frameborder="0" src="https://solomon.yandex-team.ru/?project=zora&cluster=production&host=cluster&dashboard=gozora-client-health&l.client=saved-copy"></iframe> 

## Мониторинги и алерты

В Соломоне есть [дашборд](https://nda.ya.ru/t/aOdXHXOd5EseEz). Вы можете указать в нем свой Client_id, чтобы посмотреть статистику по вашему источнику. На этот график можно делать нужные мониторинги и алерты.

## Примеры
[Python](https://a.yandex-team.ru/arc/trunk/arcadia/robot/zora/gozora/samples/python/gozora/gozora.py)

## Подключение Gorotor

Если вам нужно совершать запросы с исполнением javascript на страницах, для этого можно использовать инструмент Gorotor. Для этого:
1. Используйте TVM-авторизацию.
2. Предоставьте имя источника, RPS лимиты
3. Запросите доступы в Puncher: gorotor.zora.yandex.net, порты tcp: http/23555, messagebus/23655
4. Дождитесь выкатки кофигурации GoZora и Gorotor (можно узнавать у дежурного по Zora или в тикете на переезд/подключение).

## Подключение https

У GoZora есть свой сертификат, который можно поставить в систему. За получением сертификата можно обратиться в [чат Zora Telegram](https://t.me/joinchat/CfwpTT8thXxCIp5TQi-CtQ).

## Обратная связь:
- С проблемами можно приходить в [чат Zora Telegram](https://t.me/joinchat/CfwpTT8thXxCIp5TQi-CtQ)
- Для ошибок можно также завести задачу в очереди [Zorahelpdesk](https://st.yandex-team.ru/createTicket?queue=ZORAHELPDESK) и призвать [дежурного](https://abc.yandex-team.ru/services/fetcher/duty/) 
