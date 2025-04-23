# Краткий гайд по решению возможных проблем по дежурству

* Чат по пикам: https://t.me/joinchat/VBs2rb8A-jcdvkm0
* Чат с мониторингами: https://t.me/joinchat/RKzQjhRE6nqkB-Vu

## Старая пика

По старой пике никаких фейлов не происходило. Приходили с готовыми пр и просьбами посмотреть. Это обычно не критичные
задачи. Старая пика живет в отдельной репе https://github.com/YandexClassifieds/pica-pica/
Договорились, что по старой пике мы только экстренно смотрим критичное. На остальное не тратим ресурсы.

## Новая пика

* Пика - сервис по асинхронной прокачке какртинок по ссылкам через аватарницу, включая прокачку меты. Неймспейс в
  аватарнице используется клиентский.
* Код и дока, включая дизайн лежит в монорепе
  etc-mono: https://github.com/YandexClassifieds/verticals-backend/tree/master/etc-mono/services/pica
* Сейчас используется для двух доменов - объявления - o-yandex, недвижка - realty. Каждый домен живет в своей БД.
* Прод базы тут: https://ydb.yandex-team.ru/db/ydb-ru/verticals/production/pica/browser. rw доступ на группу выдан.
  Тестинговые в коммуналке common.
* Графики: [апи](https://grafana.vertis.yandex-team.ru/d/LweVQEcMk/pica-api?orgId=1&refresh=1m)
  , [контроллер](https://grafana.vertis.yandex-team.ru/d/k06glE5Gk/pica-controller?orgId=1&refresh=1m)
  , [сгенерированное для апи](https://grafana.vertis.yandex-team.ru/d/fB2fKWmnz/pica-api?orgId=1)
  , [сгенерированное для контроллера](https://grafana.vertis.yandex-team.ru/d/CXABKZi7k/pica-controller?orgId=1)

Основная концепция: новые запросы из апи (getOrCreate) кладутся в очередь, асинхронно прокачиваем в аву и асинхронно
прокачиваем мету. все изменения отправляем через брокер в ыть и кафку. но можно ходить в апи getOrCreate проверять
статус. Походы в аватарницу и по клиентским хостам закрыты рейтлимитерами (настраивается в конфиге). Запросы несколько
раз ретраятся в случае фейлов.

Примеры вопросов:

1. почему не прокачивается картинка или почему очередь прокачки долго разгребается. Обычно очередь долго разгребается
   из-за рейтлимита на хост или на неймспейс в аве. Тут могут помочь графики и запросы ниже:

* [запрос в базу, показывающий распределение очереди по партициям](https://yql.yandex-team.ru/Operations/YSRBR_MBw0edgjhllffbs8xszQnya4PDeWpzlh_epJU=)
* [запрос в ыть за историей изменений по определенным параметрам и датам](https://yql.yandex-team.ru/Operations/YMvqFfMBwxsCIzloS5P3ORv35GYuDEznPcU1d0CGYOQ=)
* [запрос за логами черех CH over YT](https://yql.yandex-team.ru/Operations/YMv5m9K3DJRposE0twXgV66J0qH65MjeuSHLS6S4wPE=)
* [распределение картинок хоста по статусам](https://yql.yandex-team.ru/Operations/YPhLFBJKfYFM9igrDKyULVr7m1HaKoyk7gdQ4LOdhgs=)

2. вопросы по нормализацию URL (результат прокачки неожиданный). Один раз приходили с такой задачей. Шаблоны для
   запросов можно посмотреть там же в комментах, в т.ч. запросы логов
   аватарницы. https://st.yandex-team.ru/VSCOMMONBACK-26
3. еще реже приходили с багами, например https://st.yandex-team.ru/VSCOMMONBACK-20 - такое вполне ждет меня
4. также могло быть так, что хост отвечал с ошибками, мы ретраили, но в итоге все равно закешировали ошибку. это можно
   поправить, если сходить к нам в апи с force=true. тогда мы в любом случае перекачаем картинку.
