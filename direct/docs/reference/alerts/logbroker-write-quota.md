# logbroker-write-quota

[Сырые события в juggler](https://juggler.yandex-team.ru/raw_events/?query=host%3Ddirect.solomon-alert.logbroker-write-quota-usage.lbk%7Chost%3Ddirect.solomon-alert.logbroker-write-quota-usage.lbkp%7Chost%3Ddirect.solomon-alert.logbroker-write-quota-usage.lbkx%7Chost%3Ddirect.solomon-alert.logbroker-write-quota-usage.lbkxt).
[Примеры алертов](https://juggler.yandex-team.ru/aggregate_checks/?query=namespace%3Ddirect.prod%26host%3Ddirect.prod_resources%26(service%3Dlogbroker-write-quota%7Cservice%3Dlogbroker-write-quota-np)).

## Описание { #description }
Проверяем, что скорость записи в логброкер не приближается к лимиту.  
Для этого сравниваем среднюю скорость записи за последние NN минут с ограничением квоты.

Если мы достигем лимита — запись будет ограничена — логи начнут отставать, а экспорты будут падать по таймауту или тормозить.


## Диагностика { #diagnostics }
1. По сырому событию определи:
   ![screenshot from juggler raw event page](_assets/logbroker-write-quota-raw-event.png "пример сырого события")
   - кластер (`lbk*`): он записан в конце хоста сырого события
   - аккаунт (`direct*`): он есть в имени или описании сырого события, `/Root/PersQueue/System/Quoters/` — после слеша
   - открой график утилизации квоты, ссылка на него стоит в конце описания события
   (этот же график есть на странице [метрик записи в Logbroker](../graphs/logbroker-write-metrics.md), называется **QuotaConsumed**)
1. Оцени тренд: мы уже уперлись в лимит (100%) или скоро (минуты-часы) это сделаем?
1. Найди на странице [метрик записи в Logbroker](../graphs/logbroker-write-metrics.md) соответствующий график **BytesWrittenOriginal** — он покажет в какие топики пишется больше всего данных
1. Если есть ярковыраженный "топик—лидер", разузнай про него больше:
   - за какую функциональность он отвечает
   - насколько она критична
   - ожидаем ли рост количества данных


## Решение { #solution }

Будет зависеть от ответов на несколько вопросов:
- уперлись в лимит или еще есть запас
- резкий рост или плавный
- важности топика
- это продакшн или тестинг

### Уперлись в лимит, продакшн, crossdc
Кластер lbkx, аккаунт direct.

Если мы уже уперлись в лимит или вот-вот это сделаем, действовать нужно решительно.

Можно ли уменьшить объем записи (_подкрутить_, выключить)? — Сделай это.  
Если нет (данные критичные и от них не избавиться), можно попробовать временно поднять квоту. Обратись с этим к дежурным Logbroker, все нужные контакты есть в их [чате](../chats.md#logbroker).


### Продакшн, обычный логброкер
Кластер lbk, аккаунт direct.

Локальный всплеск и он понятно, что скоро должен пройти?
Уточни у коллег, что нам некритично отставание в заливке логов и тогда можно ограничиться небольшим даунтаймом.


### Плавный рост утилизации
Объёмы данных все время растут. Если это как раз такой случай: утилизация росла долго и стала пробивать порог, то:
1. Подними пороги алерта в разумных (не выше 90%) пределах
1. Сообщи [отвественным за ресурсы](https://abc.yandex-team.ru/services/direct/?scope=quotas_management), что мы приближаемся к квоте и нужно её дозаказать


## Ссылки
- [графики](../graphs/logbroker-write-metrics.md)
- [Solomon-алерт для crossdc](https://solomon.yandex-team.ru/admin/projects/direct/alerts/logbroker-crossdc-write-quota)
- [Solomon-алерт для обычного logbroker](https://solomon.yandex-team.ru/admin/projects/direct/alerts/logbroker-common-write-quota)

