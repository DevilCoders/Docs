# Саджест

- Подсказывает популярные запросы по введенному префиксу.
- Основан на [яндексовом](https://wiki.yandex-team.ru/suggest/?from=%252Fserp%252Fsuggest%252F) саджесте.

## Пайплайн данных
1. Сервис пишет логи с запросами
1. Логи доставляются в YT
1. Происходит предобработка данных (приведение к нижнему регистру, удаление повторных пробельных символов, вычисление частотность, отрубание хвоста)
1. Из полученных данных в sandbox варится словарь
1. Новый словарь доставляется до бэкендов саджеста и заменяет собой старый
1. Сервис обращается к бэкенду саджеста по мере набора пользователем текста

## Существующие саджесты
Сейчас саджесты живут в коммунальном инстансе саджеста. При росте нагрузки можно отселиться в отдельный.
 
### Саджест для поисковой строки
Планируемая нагрузка: 100 RPS для запуска, 1к RPS далее.

```
> curl 'https://suggest-multi.yandex.net/classified/searchline?query=iph'
[{"text":"iphone"},{"text":"iphone 7"},{"text":"iphone x"},{"text":"iphone 8"},{"text":"iphone 11"},{"text":"iphone 6"},{"text":"iphone xr"},{"text":"iphone 6s"},{"text":"iphone 7 plus"},{"text":"iphone se"}]
```

1. TODO: формат лога
1. Данных сервиса пока нет. Вместо них используется [выгрузка из метрики](https://yt.yandex-team.ru/hahn/navigation?path=//home/verticals/general/export/suggest/q) по запросам к Авито/Юле. 
1. Процесс не регулярный, поэтому сейчас это [разовый](https://yql.yandex-team.ru/Operations/XxCAkhpqvwcQz7ISkhH_-I3OLIEn3HgBRSnltY47qSQ=) `YQL`-запрос
1. [Задача](https://sandbox.yandex-team.ru/task/728249125/view) в `Sandbox`

### Саджест для формы добавления
Планируемая нагрузка: 10 RPS

```
> curl 'https://suggest-multi.yandex.net/classified/add_form?query=дж'
[{"text":"джинсы"},{"text":"джемпер"},{"text":"джинсы для беременных"},{"text":"джинсовая куртка"},{"text":"джинсовка"},{"text":"джинсы женские"},{"text":"юбка джинсовая"},{"text":"джинсы мужские"},{"text":"джинсы новые"},{"text":"джинсы zara"}]
```

1. Вместо лога используется база объявлений
1. Данных сервиса пока нет. Вместо них используются объявления [спарешнные](https://yql.yandex-team.ru/Operations/XxXVe53udvLAZFOBc36nG_ULC4YcbCqjivwEmdQslOc=) с Авито.
1. [Задача](https://sandbox.yandex-team.ru/task/728531496/view) в `Sandbox`

## Как добавить новый саджест
1. Собрать данные на `YT`. При необходимости регуляризовать процесс.
1. Склонировать существующую sandbox-задачу и изменить название словаря и пути к таблице/полям. Поднять локально сервис со своим словарем можно по [инструкции](https://wiki.yandex-team.ru/serp/suggest/ez/).
1. При необходимости добавить/изменить [обработчик запроса](https://a.yandex-team.ru/arc/trunk/arcadia/quality/trailer/suggest/web_server/handlers/classified?rev=7130688).
1. Прописать в [конфигурации](https://a.yandex-team.ru/arc/trunk/arcadia/quality/trailer/suggest/configs/multi/daemon.conf?rev=7130688#L311) новый компонент. NB! alias имеет формат `real handler name` -> `alias handler name`, где `real` – то, что слушает наш хэндлер, `alias` – то, что торчит наружу.  
1. После того, как сервис и конфиг выкачен, новым саджестом можно начинать пользоваться. За выкладкой можно смотреть в [nanny](https://nanny.yandex-team.ru/ui/#/services/catalog/suggest_multi/).

## Поддержка
 - [Telegram](https://t.me/joinchat/FVD7Qyv-rWqUEP-8)

## Графики
 - [RPS](https://solomon.yandex-team.ru/?project=suggest&cluster=multi&service=handlers&l.host=cluster&l.sensor=success&graph=auto&cs=gradient&checks=-%2F_golovan%3B%2Fping&l.handler=%2Fclassified%2F*&b=1h&e=)
 - [Latency](https://solomon.yandex-team.ru/?project=suggest&cluster=multi&service=handlers&l.host=cluster&l.sensor=latency&graph=auto&cs=gradient&checks=-%2F_golovan%3B%2Fping&l.handler=%2Fclassified%2F*&b=1h&e=)
 - [Errors](https://solomon.yandex-team.ru/?project=suggest&cluster=multi&service=handlers&l.host=cluster&l.sensor=error&graph=auto&cs=gradient&checks=-%2F_golovan%3B%2Fping&l.handler=%2Fclassified%2F*&b=1h&e=)