# Логика редиректов авиа

Основные положения, бизнес логика и инфраструктура по авиа редиректам пользователей с портала Путешествий на сайты партнеров.

## Точки входа. Виды редиректов.

На страницу редиректа можно попасть:

-   с колдуна
-   со страницы поиска (при клике по кнопке купить)
-   со страницы покупки (при клике по предложению партнёра)

Есть два типа редиректов:

-   быстрый (`instant redirect`)
-   долгий (`long redirect`)

### Instant redirect

Быстрый редирект осуществляется для пользователей пришедших с колдуна, либо для пользователей попавших в эксперимент (быстрый редирект ограничен для ряда партнёров, которые задаются в переменной окружения `AVIA_NOT_INSTANT_PARTNERS`).
"Быстрый" т.к. не поисходит инициализация поиска, обращение к бекенду происходят без перезапросов.
Если упростить - сходили в бекенд, получили ссылку на партнёра, перенаправили пользователя на сайт партнёра.
Если при быстром редиректе произошла ошибка, то в качестве фолбека будет выбран долгий редирект.

### Long redirect

Долгий редирект предполагает ряд проверок и опросов бекенда и т.к. это может занять продолжительное время, то редирект имеет интерфейсное представление (страница с прогресс баром).
При заходе по урлу происходит ряд базовых проверок (если какая-либо проверка не пройдена - редиректим на страницу ошибки), обновляется qid (идентификатор поиска) и в store записывается необходимая информация:

-   `qid`
-   `partner`
-   `redirectUrl` - ссылка на ручку, которая редиректит пользователя к партнеру, либо на страницу ошибки редиректа
-   `errorRedirectUrl` - ссылка на страницу ошибки редиректа

После этого возвращаем пользователю страницу с прогресс баром (`src/projects/avia/pages/AviaRedirect/index`).

![long-redirect-page](long-redirect.png)

На клиенте мы начинаем опрос бекенда (если в процессе опроса бекенд вернул `4XX` код ответа, то для последующих запросов выставляем параметр `book_on_yandex=false`), ищем в ответе бекенда варианты удовлетворяющие параметрам страницы редиректа (с багажом или без).
Если не нашли вариант - средиректим пользователя на страницу ошибки (по `errorRedirectUrl`).
Если нашли вариант - средиректим пользователя в api (по `redirectUrl`).

В случае ошибки в ручке, пользователя средиректит на страницу ошибки, в случае успеха возможны два варианта:

-   если в ответе ручки редиректа был параметр `post`, то мы вернём пользователю страницу с формой, которая автоматически засабмитится и перенесёт пользователя на страницу партнёра
-   если в ответе ручки редиректа не было параметра `post`, то сами средиректим пользователя на страницу партнёра

Код:

-   `/server/conrollers/aviaApiController/AviiaRedirectController`
-   `/server/services/AviaRedirectService`

### Страница ошибки редиректа

Переход на страницу ошибки редиректа осуществляется в случае невалидного урла редиректа либо ошибки при взаимодействии с бекендом.

-   url `/avia/redirect/error`
-   код `/server/avia/redirectErrorController`

При обработке запроса на страницу ошибки редиректа есть вероятность, что пользователь будет направлен обратно на страницу покупки.
Редирект на страницу покупки произойдёт только в том случае если по данному рейсу есть другие партнёры. После редиректа пользователь попадает на
страницу покупки с параметрами `fromError` и `partner`, указанный в параметре `partner` партнёр будет исключен из списка предложений (блок с ссылками на партнёров).

![order-page-with-error](order-page-with-error.png)

Если по данному рейсу был только один прартнёр, то редирект на страницу покупки не произойдет и пользователю будет показана страница ошибки редиректа.

![error-page](error-page.png)

## Цепочка клиентского взаимодействия по коду приложения

1. Пользователь попадает на роут `/avia/redirect/` с параметрами редиректа.
2. SSR декоратор `aviaRedirectPageController`:
    - Проверка на наличие необходимых query параметров.
    - Получение информации о партнере и информации о перелете.
    - При отсутствии необходимых параметров - редирект на страницу ошибки.
    - Подготовка redux для CSR, добавление в redux state параметров: redirectUrl(`/api/avia/redirect/redirect/`) и errorRedirectUrl(`/avia/redirect/error/`) с необходимыми query параметрами.
3. CSR компонента `AviaRedirect`:
    - Запуск поллинга ручки `/api/avia/redirect/check/` - обрабатывает контроллер `AviaRedirectController.checkVariantExistence`. Проверка актуальности варианта.
    - При возникновении проблем - редирект на страницу ошибки.
    - Если вариант актуален - редирект на `/api/avia/redirect/redirect/`.
4. Обработка контроллером `AviaRedirectController.longRedirect` роута `/api/avia/redirect/redirect/`.
    - Цепочка вызовов с подготовкой данных `longRedirect -> waitForRedirect -> getVariant -> getRedirectData -> getRedirectData(aviaRedirectService) -> redirect(aviaTicketDaemonApi)`.
    - При падении `v3/redirect` - редирект на страницу ошибки, логируем факт ошибки.
    - При успешном ответе `v3/redirect` - проверка параметров, логируем успешный переход, выполняем редирект на сайт партнера.

## Получение данных о редиректах из логов YT

В случае проблем записи логов средствами FileLogger, можно восстановить потерянные записи из YT при помощи YQL запроса:

```
USE hahn;

$get_yson_property = ($fields, $key) -> {
  RETURN Yson::ConvertToString(Yson::YPath(Yson::Parse($fields), $key));
};
$property_extra_qid = ($fields) -> { RETURN $get_yson_property($fields, "/extra/qid"); };
$property_extra_url = ($fields) -> { RETURN $get_yson_property($fields, "/extra/url"); };

SELECT
   iso_eventtime as isoEventTime, $property_extra_qid(fields) as qid, $property_extra_url(fields) as url
FROM
    RANGE('home/logfeller/logs/qloud-runtime-log/1d', '2020-06-22', '2020-06-23')
WHERE
   qloud_project     = 'travel'  AND
   qloud_application = 'front-next' AND
   qloud_environment = 'production' AND
   iso_eventtime > '2020-06-22 21:18:05' AND
   iso_eventtime < '2020-06-23 01:10:00' AND
   message LIKE 'AVIA_REDIRECT [%]'

ORDER BY isoEventTime
LIMIT 20000;
```

## Запись файловых логов средствами BaseFileLogger

Большинство шагов во время редиректа авиа логируется. Наиболее важным считается переход на сайт партнера, так как именно он фигурирует в финансовых отчетах.
Базовая логика наследуется по цепочке: `AviaJSONLog -> BaseJSONLog -> BaseFileLogger -> AppLogger`.
Интерфейс BaseFileLogger повторяет интерфейс встроенного логгера в [DataUI Core](https://ui.yandex-team.ru/core/telemetry/logging).
Весь процесс логирования BaseFileLogger дублируется встроенным логгером и позволяет восстановить картину при различных проблемах записи.
Для записи файловых логов используется эфемерный диск. Путь до логов редиректа: `/ephemeral/var/log/frontend/avia/json_redir.log`.
Папка создается после примонтирования эфемерного диска в скрипте: `deploy/pre_start/10_ephemeral`.

## Ротация логов(logrotate)

Для ротация логов используется пакет [yandex-logrotate](https://wiki.yandex-team.ru/logrotate/).
Примеры конфигурации и документацию можно посмотреть по [ссылке](https://linux.die.net/man/8/logrotate).
Внутри контейнера содержится базовая для всех конфигурация `etc/logrotate.conf` с оператором include для файлов с особыми настройками для различных типов логов `/etc/logrotate.d/.`.
Исходники конфигурации смотреть в `deploy/logrotate/logrotate.d/.`.

Какие именно логи мы ротируем:

1. Логи авиа `/ephemeral/var/log/frontend/avia/*.log`.
2. Логи logrotate `/var/log/logrotate/logrotate.log`.
3. Логи push-client `/var/log/statbox/push-client.log`.
4. Логи supervisord `/var/log/supervisord.log`.

Основные параметры конфигурации:

1. `nocompress` - не сжимать файлы после ротации;
2. `rotate` - количество копий старых версий лог файлов;
3. `hourly, daily, weekly, monthly` - временные промежутки ротации;
4. `size` - ротация при достижении определенного размера лог файла;
5. `postrotate` - скрипт, который нужно выполнить после ротации;
6. `sharedscripts` - выполнять скрипт из `postrotate` только один раз после ротации;
7. `missingok` - не выводить ошибку, при отсутствии лог файла;

## Запуск ротации логов(cron)

За запуск ротации логов по расписанию отвечает [cron](https://en.wikipedia.org/wiki/Cron).
Конфигурация supervisor для процесса cron здесь `deploy/supervisor/conf.d/02-cron.conf`.
Запуск внутри контейнера происходит здесь `deploy/pre_start/90_start`.
Внутри контейнера конфигурация cron находится в `/etc/cron.d/.`.
Исходники конфигурации смотреть в `deploy/cron/.`.
В момент подготовки контейнера выполняется проверка на наличие `cron.daily/logrotate` и его удаление.
Запуск задания планировщика ротации логов выполняется каждые 30 минут.
За лок процесса отвечает `yandex-lockf`, исключая двойной запуск заданий cron.

## Доставка логов

### Последовательность отправки логов

Последовательность доставки логов до YT:

1. У нас в контейнере крутится процесс [push-client](https://wiki.yandex-team.ru/logbroker/docs/push-client/) и поставляет логи в logbroker.
2. После отравки сообщений из приложения [logbroker](https://logbroker.yandex-team.ru/docs/) разбирает очередь.
3. За доставку данных из очереди непосредственно в [YT](https://wiki.yandex-team.ru/yt/) отвечает [logfeller](https://wiki.yandex-team.ru/logfeller/).

### Настройки push-client

Push-client может работать в двух режимах: в режиме `daemon` и режиме `cron`. У нас используется пакет `statbox-push-client-daemon`.
Файлы, за которыми следим и отправляем в logbroker: `deploy/statbox-push-client/files.yaml`.
Общие настройки push-client: `deploy/statbox-push-client/push-client.yaml`.
Настройки `master_addr` logbroker под конкретное окружение: `deploy/statbox-push-client/production/push-client.yaml` и `deploy/statbox-push-client/testing/push-client.yaml`.
За запуск процесса push-client отвечает supervisor: `deploy/supervisor/conf.d/03-push-client.conf`.
Сам запуск происходит в pre_start: `deploy/pre_start/90_start`.

### Интерфейс logbroker

Интерфейс аккаунта `rasp-front` и директории можно посмотреть на [logbroker.yandex-team.ru](https://logbroker.yandex-team.ru/logbroker/accounts/rasp-front?page=browser&type=account).
Все метрики по [avia-json-redir-log](https://logbroker.yandex-team.ru/logbroker/accounts/rasp-front/avia-json-redir-log?page=statistics&type=topic&tab=writeMetrics&shownTopics=all%20topics&metricsFrom=1596466543630&metricsTo=1596552943630&sortOrder=%22default%22).
Конфигурацию avia для [logfeller](https://a.yandex-team.ru/arc/trunk/arcadia/logfeller/configs/logs/travel_avia_hahn_logs.json?rev=7172603).
Описание конфигурации logfeller в [arcadia](https://a.yandex-team.ru/arc/trunk/arcadia/logfeller/configs).

### Логи в YT

Логи `avia-json-redir-log` можно посмотреть в [yt.yandex-team.ru](https://yt.yandex-team.ru/hahn/navigation?path=//home/avia/logs/avia-json-redir-log).

## Дальнейшие шаги

1. Разобрать работу solomon в контейнере вместе с push-client, оценить ресурсные затраты.
2. Посмотреть замену push-client на новый агент [Unified Agent](https://logbroker.yandex-team.ru/docs/unified_agent/).
3. Возможно унести всю обвязку логов в отдельный контейнер.
4. Посмотреть логи всех процессов в момент падения машин.
