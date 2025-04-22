## Сущности в базе
- [Оффер в поисковых таблицах](https://yql.yandex-team.ru/Operations/Ybnk81Z1OxnLHVUwTADj7k0a-L4meNoFs4Igmqg1Mwg=)

## Количество офферов
- [Количество офферов по цвету в сервисной таблице](https://yql.yandex-team.ru/Operations/YR9ocQuEI-QKY3qcV7QTmAQxtDeKOpb4GMEy7YriTJo=)
- [Количество офферов с определенными скрытиями](https://yql.yandex-team.ru/Operations/YWAGfpfFt7_woKAQ3MNIpNbE3PInO8LLTE3ZKeqKCZs=)
- [Количество офферов с определенным вердиктом / кодом ошибки](https://yql.yandex-team.ru/Operations/YV8QRK5OD5ffmmN8KZ08dfqB3mMwdx5ODzQya4bB4gI=)

## Задания на парсинг
- [Задания на синий парсинг](https://yql.yandex-team.ru/Operations/YES5XL94hrXemzKBx8xoAVejR68yq0mEbz5Ch-GmyFA=) отсортированные по времени, по всем 30-минутным таблицам
- фильтровать можно по колонкам: business_id, feed_id
- [Задание на проверку фида](https://yql.yandex-team.ru/Operations/YW_7qdjKS6X7rKEm_oVwbnUd0DDafeBfPFdJ8AwJDI8=)
- [Сессии к ClickHouse](https://yql.yandex-team.ru/Operations/YJwQUNK3DAet8XcSmLcxELWo8FBbGLvGYPug2ylPWoE=)

## Строллер
- [Посмотреть какие запросы в строллер были по бизнесу](https://yql.yandex-team.ru/Operations/YbxmXAVK8AskqQWjketx344kCwrVcIBz3GKV-q2_SmU=)

## Скорость событийной поставки в баннерленд
- [Перцентили от парсинга до записи в топик](https://yql.yandex-team.ru/Operations/YanH2ShnuY2pWyzch9-3D-JIFIdORjkf9tVAt3uv4mo=)

## Быстрый пайплайн
- [Топ по feed_id в market-quick-log](https://yql.yandex-team.ru/Operations/Yajf-ihnuY2pWc3X7NdsFkSKwE9Qwr5Fzg0Csfid3XE=)

## PAPI
- [События по бизнесу](https://yql.yandex-team.ru/Operations/YROuNQuEI1ttwsBTN_ml2-7lGAtWeefSstx6wLJZtuM=)

## Diff офферов в хранилище и в быстром слое SaaS
- [Разница между стейтов хранилища и саасом](https://yql.yandex-team.ru/Operations/YKJd-fMBw8wapwmsMROjZyV61JiXUI1hdzJYu8CZA3o=)
- Выходную временную таблицу можно скормить бинарнику [saas_dumper](https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/routines/tasks/saas_docs_dumper) в качестве фильтра идентификаторов офферов при посттроении таблицы для отправки в SaaS с помощью [saas_push](https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/routines/tasks/saas_docs_dumper#otpravka-dokumentov-s-pomoshyu-saas_push-predpochititelnyj-variant).

## Ответ MDM на оффера от datacamp 
по business_id и offer_id:
- сообщение [от datacamp в mdm](https://yql.yandex-team.ru/Operations/YX-pyAVK8IhSHjlhjZUQZyNgFjaDwZxuw56-ZjzhNh8=)
- ответ [от mdm](https://yql.yandex-team.ru/Operations/YX-ok5fFtxLpivyOK2yvljqFIy5lIJIBtO7qlXgq43w=)

## Перцентили публикации для новых офферов
- [запрос по выгрузке](https://yql.yandex-team.ru/Operations/YYLVK65OD9giQyJVXJfPoxw47tSpnKvIg89xXaQxJUs=)
- зависит от скорости исправления ошибок партнерами

## Запросы и ответы УК
- [Ответы по офферу](https://yql.yandex-team.ru/Operations/YTJRnZfFt4z_hex8B6F2A9Sq0Wr7_a_w5tMh9h1yVU0=)
- [Логфеллер запросы](https://a.yandex-team.ru/arc/trunk/arcadia/logfeller/configs/logs/market_arnold_logs.json?blame=true&rev=r8844144#L4718)
- [Логфеллер ответы](https://a.yandex-team.ru/arc/trunk/arcadia/logfeller/configs/logs/market_arnold_logs.json?blame=true#L4738)

## ECOM выгрузка
- [Урлы картинок и офферов](https://yql.yandex-team.ru/Operations/YVcsktK3DHqKZLx1oH9x5B6nC7CmioIkU364pSFJTdI=)

## MBOC
- [Отправка офферов в сторону MBOC](https://yql.yandex-team.ru/Operations/YMjn1vMBwxsCIUUaV9tipauqLrOrZpvhyM_DsuU6w8w=)
- [Отправка офферов из MBOC в Хранилище](https://yql.yandex-team.ru/Operations/Ybxneq5OD5cZoL3C0B7-q3JRAAjDpAZoTUigh_DX5YA=)

## StockStorage
- [Отправка офферов сторону SS](https://yql.yandex-team.ru/Operations/YPqMe_MBw55cYJf33E7sCp0PKPLZ-hf-0mZUdBpqmos=) - в примере тестинг
- [Отправка офферов из SS в Хранилище](https://yql.yandex-team.ru/Operations/YPBiwAuEI3xk-Le4TaobVj_HLxm2df63DiHN9xlJVIo=) - в примере тестинг
