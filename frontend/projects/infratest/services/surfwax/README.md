# surfwax

WebDriver прокси, запускающий браузеры в Sandbox по запросу.

<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->


- [Пользователям](#%D0%BF%D0%BE%D0%BB%D1%8C%D0%B7%D0%BE%D0%B2%D0%B0%D1%82%D0%B5%D0%BB%D1%8F%D0%BC)
  - [Зачем мне SurfWax вместо Selenium Grid?](#%D0%B7%D0%B0%D1%87%D0%B5%D0%BC-%D0%BC%D0%BD%D0%B5-surfwax-%D0%B2%D0%BC%D0%B5%D1%81%D1%82%D0%BE-selenium-grid)
  - [Какие гарантии?](#%D0%BA%D0%B0%D0%BA%D0%B8%D0%B5-%D0%B3%D0%B0%D1%80%D0%B0%D0%BD%D1%82%D0%B8%D0%B8)
  - [Как устроена авторизация?](#%D0%BA%D0%B0%D0%BA-%D1%83%D1%81%D1%82%D1%80%D0%BE%D0%B5%D0%BD%D0%B0-%D0%B0%D0%B2%D1%82%D0%BE%D1%80%D0%B8%D0%B7%D0%B0%D1%86%D0%B8%D1%8F)
  - [Какие браузеры поддерживаются?](#%D0%BA%D0%B0%D0%BA%D0%B8%D0%B5-%D0%B1%D1%80%D0%B0%D1%83%D0%B7%D0%B5%D1%80%D1%8B-%D0%BF%D0%BE%D0%B4%D0%B4%D0%B5%D1%80%D0%B6%D0%B8%D0%B2%D0%B0%D1%8E%D1%82%D1%81%D1%8F)
  - [Какие клиенты и инструменты тестирования поддерживаются?](#%D0%BA%D0%B0%D0%BA%D0%B8%D0%B5-%D0%BA%D0%BB%D0%B8%D0%B5%D0%BD%D1%82%D1%8B-%D0%B8-%D0%B8%D0%BD%D1%81%D1%82%D1%80%D1%83%D0%BC%D0%B5%D0%BD%D1%82%D1%8B-%D1%82%D0%B5%D1%81%D1%82%D0%B8%D1%80%D0%BE%D0%B2%D0%B0%D0%BD%D0%B8%D1%8F-%D0%BF%D0%BE%D0%B4%D0%B4%D0%B5%D1%80%D0%B6%D0%B8%D0%B2%D0%B0%D1%8E%D1%82%D1%81%D1%8F)
  - [Кто уже использует SurfWax?](#%D0%BA%D1%82%D0%BE-%D1%83%D0%B6%D0%B5-%D0%B8%D1%81%D0%BF%D0%BE%D0%BB%D1%8C%D0%B7%D1%83%D0%B5%D1%82-surfwax)
  - [Как попробовать?](#%D0%BA%D0%B0%D0%BA-%D0%BF%D0%BE%D0%BF%D1%80%D0%BE%D0%B1%D0%BE%D0%B2%D0%B0%D1%82%D1%8C)
  - [Как подключить?](#%D0%BA%D0%B0%D0%BA-%D0%BF%D0%BE%D0%B4%D0%BA%D0%BB%D1%8E%D1%87%D0%B8%D1%82%D1%8C)
  - [API](#api)
- [Руководство по поддержке](#%D1%80%D1%83%D0%BA%D0%BE%D0%B2%D0%BE%D0%B4%D1%81%D1%82%D0%B2%D0%BE-%D0%BF%D0%BE-%D0%BF%D0%BE%D0%B4%D0%B4%D0%B5%D1%80%D0%B6%D0%BA%D0%B5)
  - [Перевод сервиса на SurfWax](#%D0%BF%D0%B5%D1%80%D0%B5%D0%B2%D0%BE%D0%B4-%D1%81%D0%B5%D1%80%D0%B2%D0%B8%D1%81%D0%B0-%D0%BD%D0%B0-surfwax)
    - [Инструкция по переводу](#%D0%B8%D0%BD%D1%81%D1%82%D1%80%D1%83%D0%BA%D1%86%D0%B8%D1%8F-%D0%BF%D0%BE-%D0%BF%D0%B5%D1%80%D0%B5%D0%B2%D0%BE%D0%B4%D1%83)
  - [Эксперимент](#%D1%8D%D0%BA%D1%81%D0%BF%D0%B5%D1%80%D0%B8%D0%BC%D0%B5%D0%BD%D1%82)
  - [Как по id сессии определить задачу в Sandbox, в рамках которой она поднималась?](#%D0%BA%D0%B0%D0%BA-%D0%BF%D0%BE-id-%D1%81%D0%B5%D1%81%D1%81%D0%B8%D0%B8-%D0%BE%D0%BF%D1%80%D0%B5%D0%B4%D0%B5%D0%BB%D0%B8%D1%82%D1%8C-%D0%B7%D0%B0%D0%B4%D0%B0%D1%87%D1%83-%D0%B2-sandbox-%D0%B2-%D1%80%D0%B0%D0%BC%D0%BA%D0%B0%D1%85-%D0%BA%D0%BE%D1%82%D0%BE%D1%80%D0%BE%D0%B9-%D0%BE%D0%BD%D0%B0-%D0%BF%D0%BE%D0%B4%D0%BD%D0%B8%D0%BC%D0%B0%D0%BB%D0%B0%D1%81%D1%8C)
  - [Потребление квоты](#%D0%BF%D0%BE%D1%82%D1%80%D0%B5%D0%B1%D0%BB%D0%B5%D0%BD%D0%B8%D0%B5-%D0%BA%D0%B2%D0%BE%D1%82%D1%8B)
  - [Балансер](#%D0%B1%D0%B0%D0%BB%D0%B0%D0%BD%D1%81%D0%B5%D1%80)
    - [L3-балансер](#l3-%D0%B1%D0%B0%D0%BB%D0%B0%D0%BD%D1%81%D0%B5%D1%80)
    - [L7-балансер](#l7-%D0%B1%D0%B0%D0%BB%D0%B0%D0%BD%D1%81%D0%B5%D1%80)
  - [Сервис в YDeploy](#%D1%81%D0%B5%D1%80%D0%B2%D0%B8%D1%81-%D0%B2-ydeploy)
  - [База в YDB](#%D0%B1%D0%B0%D0%B7%D0%B0-%D0%B2-ydb)
  - [Кастомные метрики](#%D0%BA%D0%B0%D1%81%D1%82%D0%BE%D0%BC%D0%BD%D1%8B%D0%B5-%D0%BC%D0%B5%D1%82%D1%80%D0%B8%D0%BA%D0%B8)
  - [Алерты](#%D0%B0%D0%BB%D0%B5%D1%80%D1%82%D1%8B)
  - [Разбор алертов](#%D1%80%D0%B0%D0%B7%D0%B1%D0%BE%D1%80-%D0%B0%D0%BB%D0%B5%D1%80%D1%82%D0%BE%D0%B2)
    - [surfwax_selenoid_broken_status](#surfwax_selenoid_broken_status)
    - [surfwax_session_create](#surfwax_session_create)
  - [Заканчивается квота в S3](#%D0%B7%D0%B0%D0%BA%D0%B0%D0%BD%D1%87%D0%B8%D0%B2%D0%B0%D0%B5%D1%82%D1%81%D1%8F-%D0%BA%D0%B2%D0%BE%D1%82%D0%B0-%D0%B2-s3)
  - [Сборка LXC-контейнера для задачи SURFWAX_SELENOID](#%D1%81%D0%B1%D0%BE%D1%80%D0%BA%D0%B0-lxc-%D0%BA%D0%BE%D0%BD%D1%82%D0%B5%D0%B9%D0%BD%D0%B5%D1%80%D0%B0-%D0%B4%D0%BB%D1%8F-%D0%B7%D0%B0%D0%B4%D0%B0%D1%87%D0%B8-surfwax_selenoid)
  - [Создание квоты](#%D1%81%D0%BE%D0%B7%D0%B4%D0%B0%D0%BD%D0%B8%D0%B5-%D0%BA%D0%B2%D0%BE%D1%82%D1%8B)
    - [Автоматический режим](#%D0%B0%D0%B2%D1%82%D0%BE%D0%BC%D0%B0%D1%82%D0%B8%D1%87%D0%B5%D1%81%D0%BA%D0%B8%D0%B9-%D1%80%D0%B5%D0%B6%D0%B8%D0%BC)
    - [Ручной режим](#%D1%80%D1%83%D1%87%D0%BD%D0%BE%D0%B9-%D1%80%D0%B5%D0%B6%D0%B8%D0%BC)
  - [Добавление браузера в квоту](#%D0%B4%D0%BE%D0%B1%D0%B0%D0%B2%D0%BB%D0%B5%D0%BD%D0%B8%D0%B5-%D0%B1%D1%80%D0%B0%D1%83%D0%B7%D0%B5%D1%80%D0%B0-%D0%B2-%D0%BA%D0%B2%D0%BE%D1%82%D1%83)
  - [Удаление браузера из квоты](#%D1%83%D0%B4%D0%B0%D0%BB%D0%B5%D0%BD%D0%B8%D0%B5-%D0%B1%D1%80%D0%B0%D1%83%D0%B7%D0%B5%D1%80%D0%B0-%D0%B8%D0%B7-%D0%BA%D0%B2%D0%BE%D1%82%D1%8B)
  - [Перенос браузера из одной группы в другую](#%D0%BF%D0%B5%D1%80%D0%B5%D0%BD%D0%BE%D1%81-%D0%B1%D1%80%D0%B0%D1%83%D0%B7%D0%B5%D1%80%D0%B0-%D0%B8%D0%B7-%D0%BE%D0%B4%D0%BD%D0%BE%D0%B9-%D0%B3%D1%80%D1%83%D0%BF%D0%BF%D1%8B-%D0%B2-%D0%B4%D1%80%D1%83%D0%B3%D1%83%D1%8E)
  - [Добавление датацентра в исключения для квоты](#%D0%B4%D0%BE%D0%B1%D0%B0%D0%B2%D0%BB%D0%B5%D0%BD%D0%B8%D0%B5-%D0%B4%D0%B0%D1%82%D0%B0%D1%86%D0%B5%D0%BD%D1%82%D1%80%D0%B0-%D0%B2-%D0%B8%D1%81%D0%BA%D0%BB%D1%8E%D1%87%D0%B5%D0%BD%D0%B8%D1%8F-%D0%B4%D0%BB%D1%8F-%D0%BA%D0%B2%D0%BE%D1%82%D1%8B)
  - [Кэши браузеров](#%D0%BA%D1%8D%D1%88%D0%B8-%D0%B1%D1%80%D0%B0%D1%83%D0%B7%D0%B5%D1%80%D0%BE%D0%B2)
    - [Сборка кэшей браузеров](#%D1%81%D0%B1%D0%BE%D1%80%D0%BA%D0%B0-%D0%BA%D1%8D%D1%88%D0%B5%D0%B9-%D0%B1%D1%80%D0%B0%D1%83%D0%B7%D0%B5%D1%80%D0%BE%D0%B2)
    - [Добавление кэшей браузеров в квоту](#%D0%B4%D0%BE%D0%B1%D0%B0%D0%B2%D0%BB%D0%B5%D0%BD%D0%B8%D0%B5-%D0%BA%D1%8D%D1%88%D0%B5%D0%B9-%D0%B1%D1%80%D0%B0%D1%83%D0%B7%D0%B5%D1%80%D0%BE%D0%B2-%D0%B2-%D0%BA%D0%B2%D0%BE%D1%82%D1%83)
    - [Раскатка кэшей браузеров по sandbox-клиентам](#%D1%80%D0%B0%D1%81%D0%BA%D0%B0%D1%82%D0%BA%D0%B0-%D0%BA%D1%8D%D1%88%D0%B5%D0%B9-%D0%B1%D1%80%D0%B0%D1%83%D0%B7%D0%B5%D1%80%D0%BE%D0%B2-%D0%BF%D0%BE-sandbox-%D0%BA%D0%BB%D0%B8%D0%B5%D0%BD%D1%82%D0%B0%D0%BC)
- [Локальная среда разработки](#%D0%BB%D0%BE%D0%BA%D0%B0%D0%BB%D1%8C%D0%BD%D0%B0%D1%8F-%D1%81%D1%80%D0%B5%D0%B4%D0%B0-%D1%80%D0%B0%D0%B7%D1%80%D0%B0%D0%B1%D0%BE%D1%82%D0%BA%D0%B8)
  - [Пререквизиты](#%D0%BF%D1%80%D0%B5%D1%80%D0%B5%D0%BA%D0%B2%D0%B8%D0%B7%D0%B8%D1%82%D1%8B)
  - [Подготовка окружения](#%D0%BF%D0%BE%D0%B4%D0%B3%D0%BE%D1%82%D0%BE%D0%B2%D0%BA%D0%B0-%D0%BE%D0%BA%D1%80%D1%83%D0%B6%D0%B5%D0%BD%D0%B8%D1%8F)
  - [Запуск сервиса без ординатора](#%D0%B7%D0%B0%D0%BF%D1%83%D1%81%D0%BA-%D1%81%D0%B5%D1%80%D0%B2%D0%B8%D1%81%D0%B0-%D0%B1%D0%B5%D0%B7-%D0%BE%D1%80%D0%B4%D0%B8%D0%BD%D0%B0%D1%82%D0%BE%D1%80%D0%B0)
  - [Запуск сервиса с ординатором](#%D0%B7%D0%B0%D0%BF%D1%83%D1%81%D0%BA-%D1%81%D0%B5%D1%80%D0%B2%D0%B8%D1%81%D0%B0-%D1%81-%D0%BE%D1%80%D0%B4%D0%B8%D0%BD%D0%B0%D1%82%D0%BE%D1%80%D0%BE%D0%BC)
  - [Тест работоспособности](#%D1%82%D0%B5%D1%81%D1%82-%D1%80%D0%B0%D0%B1%D0%BE%D1%82%D0%BE%D1%81%D0%BF%D0%BE%D1%81%D0%BE%D0%B1%D0%BD%D0%BE%D1%81%D1%82%D0%B8)
  - [Завершение работы](#%D0%B7%D0%B0%D0%B2%D0%B5%D1%80%D1%88%D0%B5%D0%BD%D0%B8%D0%B5-%D1%80%D0%B0%D0%B1%D0%BE%D1%82%D1%8B)
- [Релиз новой версии](#%D1%80%D0%B5%D0%BB%D0%B8%D0%B7-%D0%BD%D0%BE%D0%B2%D0%BE%D0%B9-%D0%B2%D0%B5%D1%80%D1%81%D0%B8%D0%B8)
  - [Пререквизиты](#%D0%BF%D1%80%D0%B5%D1%80%D0%B5%D0%BA%D0%B2%D0%B8%D0%B7%D0%B8%D1%82%D1%8B-1)
  - [Раскатка сервиса](#%D1%80%D0%B0%D1%81%D0%BA%D0%B0%D1%82%D0%BA%D0%B0-%D1%81%D0%B5%D1%80%D0%B2%D0%B8%D1%81%D0%B0)
    - [Раскатка в staging](#%D1%80%D0%B0%D1%81%D0%BA%D0%B0%D1%82%D0%BA%D0%B0-%D0%B2-staging)
    - [Раскатка в production](#%D1%80%D0%B0%D1%81%D0%BA%D0%B0%D1%82%D0%BA%D0%B0-%D0%B2-production)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

## Пользователям

### Зачем мне SurfWax вместо Selenium Grid?

[Пост](https://clubs.at.yandex-team.ru/devtools-frontend/375) в Этушке.

### Какие гарантии?

SLO на создание сессии браузера составляет 120 секунд, но, как правило, даже в худшем случае сессии [поднимаются](https://yasm.yandex-team.ru/alert/surfwax_session_create) гораздо быстрее.

Количество "проваленных" запросов на поднятие сессий через SurfWax будет отображаться на графике после задачи [FEI-24028](https://st.yandex-team.ru/FEI-24028) (на данный момент соизмеримо с количеством "проваленных" запросов на поднятие сессий через Selenium Grid).

### Как устроена авторизация?

Как и в текущем Selenium Grid – никак. Авторизация будет реализована в задаче [FEI-22538](https://st.yandex-team.ru/FEI-22538).

### Какие браузеры поддерживаются?

- десктопный chrome (+ headless chrome и chrome в режиме мобильной эмуляции)
- десктопный firefox
- мобильный chrome в android
- searchapp (мобильное приложение) в android
- [wip] ie и edge ([ссылка](https://goals.yandex-team.ru/compilations/own?login=gavryushin&goal=119235) на цель)
- [wip] ios в safari ([ссылка](https://goals.yandex-team.ru/filter?user=20199&goal=118573) на цель)

### Какие клиенты и инструменты тестирования поддерживаются?

SurfWax не зависит от клиента и/или инструмента тестирования. Запросы на поднятие сессий и выполнение действий в этих сессия можно отправлять хоть curl-ом.

### Кто уже использует SurfWax?

- [СЕРП](https://a.yandex-team.ru/arc/trunk/arcadia/frontend/projects/web4)
- [Картинки и Видео](https://a.yandex-team.ru/arc/trunk/arcadia/frontend/projects/fiji)
- Все сервисы монорепо [frontend](https://a.yandex-team.ru/arc/trunk/arcadia/frontend/services) (> 80 проектов)
- [Коллекции](https://github.yandex-team.ru/mm-interfaces/collections)
- [Маркет](https://github.yandex-team.ru/market)
- [Директ](https://a.yandex-team.ru/arc/trunk/arcadia/direct/frontend/services)
- [Партнерский код](https://github.yandex-team.ru/wanya/pcode/)
- [Учебник](https://github.yandex-team.ru/pelican/schoolbook-frontend)
- [Вики](https://github.yandex-team.ru/data-ui/wiki)
- [Селф-Сервис](https://github.yandex-team.ru/IMS/vh-selfservice)
- [Tracker](https://github.yandex-team.ru/data-ui/tracker)
- [Vconf](https://a.yandex-team.ru/arc/trunk/arcadia/hrtech/frontend/services/vconf)
- [IDM](https://a.yandex-team.ru/arc_vcs/data-ui/idm/)

### Как попробовать?

Использовать в качестве endpoint `http://default@sw.yandex-team.ru:80/v0`, где доступен браузер `chrome` версии `91.0`:
```js
{
    browserName: "chrome",
    browserVersion: "91.0"
}
```

Данная квота носит демонстративных характер и не предназначена для использования в production.

### Как подключить?

Обратиться с запросом в [поддержку](https://forms.yandex-team.ru/surveys/17756/) (выбрать в качестве инструмента `SurfWax`).

### API

- получение списка всех квот:
  ```bash
  curl https://sw.yandex-team.ru/api/v0/quotas
  ```
- получение браузеров квоты:
  ```bash
  curl https://sw.yandex-team.ru/api/v0/quotas/<quota_name>/browsers
  # curl https://sw.yandex-team.ru/api/v0/quotas/default/browsers
  ```
- получение кэшей квоты:
  ```bash
  curl https://sw.yandex-team.ru/api/v0/quotas/<quota_name>/caches
  # curl https://sw.yandex-team.ru/api/v0/quotas/default/browsers
  ```

### Графики
Данные о количестве и времени поднятия сессий выгружаются в yasm.

[Общий дашборд с графиками](https://yasm.yandex-team.ru/template/panel/surfax-panel)

Возможно создавать свои дашборды/графики с разбиением по квотам, браузерам и версиям браузеров.
В yasm собираются такие сигналы (события):
- `unistat-handleCreateSession_QUOTA_BROWSER-NAME_BROWSER-VERSION_calls_count_dmmm` для
  количества сессий;
- `unistat-handleCreateSession_QUOTA_BROWSER-NAME_BROWSER-VERSION_duration_ms_dhhh` для времени поднятия сессий.

Работа с UI графиков в деталях описана в [документации Golovan](https://wiki.yandex-team.ru/golovan/userdocs/templatium). Ниже приводится несколько примеров, по аналогии с которыми можно делать свои собственные графики/дашборды:
- [График количества запросов сессий в web4, chrome 72.1](https://yasm.yandex-team.ru/panel/shadowusr._QINdyw)
- [График времени поднятия сессий в web4, chrome 72.1](https://yasm.yandex-team.ru/panel/shadowusr._llterj)
- [Графики количества запросов сессий и их времени поднятия в web4, десктопные браузеры на linux (desktop-linux)](https://yasm.yandex-team.ru/panel/shadowusr._8HTPuy)

## Руководство по поддержке

### Перевод сервиса на SurfWax

[График](https://logs.selenium.yandex-team.ru/app/kibana#/visualize/edit/a9481b50-2cc4-11ec-9f79-1ddce196f3ad?_g=(filters:!(),refreshInterval:(pause:!t,value:0),time:(from:now-7d,mode:quick,to:now))&_a=(filters:!(('$state':(store:appState),meta:(alias:!n,disabled:!t,index:c924cc80-27d9-11ea-a4de-f590eeb20dc3,key:browser,negate:!f,params:(query:taskId,type:phrase),type:phrase,value:taskId),query:(match:(browser:(query:taskId,type:phrase)))),('$state':(store:appState),meta:(alias:!n,disabled:!f,index:c924cc80-27d9-11ea-a4de-f590eeb20dc3,key:status,negate:!f,params:(query:SESSION_CREATED,type:phrase),type:phrase,value:SESSION_CREATED),query:(match:(status:(query:SESSION_CREATED,type:phrase))))),linked:!f,query:(language:lucene,query:''),uiState:(),vis:(aggs:!((enabled:!t,id:'1',params:(),schema:metric,type:count),(enabled:!t,id:'3',params:(customInterval:'2h',drop_partials:!f,extended_bounds:(),field:'@timestamp',interval:d,min_doc_count:1,timeRange:(from:now-7d,mode:quick,to:now),useNormalizedEsInterval:!t),schema:segment,type:date_histogram),(enabled:!t,id:'2',params:(field:user.keyword,missingBucket:!f,missingBucketLabel:Missing,order:desc,orderBy:'1',otherBucket:!t,otherBucketLabel:Other,size:5),schema:group,type:terms)),params:(addLegend:!t,addTimeMarker:!f,addTooltip:!t,categoryAxes:!((id:CategoryAxis-1,labels:(show:!t,truncate:100),position:bottom,scale:(type:linear),show:!t,style:(),title:(),type:category)),grid:(categoryLines:!f,style:(color:%23eee)),legendPosition:right,seriesParams:!((data:(id:'1',label:Count),drawLinesBetweenPoints:!t,mode:stacked,show:true,showCircles:!t,type:histogram,valueAxis:ValueAxis-1)),times:!(),type:histogram,valueAxes:!((id:ValueAxis-1,labels:(filter:!f,rotate:0,show:!t,truncate:100),name:LeftAxis-1,position:left,scale:(mode:normal,type:linear),show:!t,style:(),title:(text:Count),type:value))),title:'Selenium%20users',type:histogram))) количества созданных сессий через `sg.yandex-team.ru`. Наша цель полностью снять нагрузку с `sg.yandex-team.ru` и перевести её на `sw.yandex-team.ru`.

#### Инструкция по переводу

- оговорить факт перехода с руководителем сервиса или ответственным за инфраструктуру сервиса, в качестве аргументов привести [пост](https://clubs.at.yandex-team.ru/devtools-frontend/375) в этушке
- оценить нагрузку, которую создаёт сервиc:
  - оценить количество запусков тестов в CI в день (`total_tests_runs_per_day`)
  - оценить максимальное количество одновременных запусков тестов в CI (`max_parallel_tests_runs_per_day`)
  - оценить среднее время выполнения в минутах одного успешного запуска тестов в CI с округлением вверх до значения кратного пяти (`tests_run_execution_time_min`), то есть если прогон тестов занимает 12 минут, то значение можно округлить до 15 минут
  - посчитать количество браузеров для групп desktop-linux и android, необходимое на один запуск тестов (`desktop_linux_parallel_sessions_per_tests_run` и `android_parallel_sessions_per_tests_run`)

    Браузеры из группы desktop-linux:
      - десктопный chrome (+ headless chrome и chrome в режиме мобильной эмуляции)
      - десктопный firefox

    Браузеры из группы android:
      - мобильный chrome в android
      - searchapp (мобильное приложение) в android

    Если сервис использует hermione, то количество браузеров для разных групп рассчитывается на основании значений опции `sessionsPerBrowser` в конфиге.
  - посчитать среднее количество задач `SURFWAX_SELENOID` для обслуживания одного запуска тестов (`surfwax_selenoid_tasks_count_per_tests_run`):
      ```
      desktop_linux_parallel_sessions_per_tests_run / (32 / cpu_cores_per_session (desktop-linux)) + android_parallel_sessions_per_tests_run / (32 / cpu_cores_per_session (android))
      ```
      где `cpu_cores_per_session (desktop-linux)` и `cpu_cores_per_session (android)` значения из [таблицы](https://yc.yandex-team.ru/folders/aku9fojph5675foon66g/ydb/databases/etn00la4p1rbuf918p9u/browse?path=%2Fbrowser_groups) базы данных для соответствующих групп браузеров
  - посчитать потенциальное максимальное количество одновременно запущенных задач `SURFWAX_SELENOID`:
    ```
    surfwax_selenoid_tasks_count_per_tests_run * max_parallel_tests_runs_per_day
    ```
  - посчитать количество задач `SURFWAX_SELENOID` для обслуживания всех сборок в день (`required_surfwax_selenoid_tasks_count_per_day`):
    ```
    surfwax_selenoid_tasks_count_per_tests_run * total_tests_runs_per_day
    ```
  - посчитать на основании [документации](https://docs.yandex-team.ru/sandbox/quota#quota-points) потребляемую квоту одной задачей `SURFWAX_SELENOID` в единицах `qp` (`surfwax_selenoid_task_quota_consumption`):
      ```
      (32 ядра * 3600 секунд * (tests_run_execution_time_min / 60 ) часов * 10µQP) / 1000000
      ```
  - посчитать потенциальную потребляемую квоту всеми задачами `SURFWAX_SELENOID` за день в единицах `qp` (`surfwax_selenoid_tasks_potential_quota_consumption_per_day`):
      ```
      required_surfwax_selenoid_tasks_count_per_day * surfwax_selenoid_task_quota_consumption
      ```
  - если у сервиса нет собственной группы в Sandbox, то создать группу с [дефолтным](https://docs.yandex-team.ru/sandbox/quota#default-quota) количеством `qp` ([ссылка](https://jing.yandex-team.ru/files/gavryushin/Screen%20Shot%202021-10-22%20at%2014.26.19.png) на картинку)
  - посчитать свободную квоту сервиса в Sandbox в единицах `qp`:
    - открыть страницу `https://sandbox.yandex-team.ru/admin/groups/<group>/general`, где `<group>` (upper case) – это имя группы в Sandbox, под которым запускаются остальные CI процессы сервиса
    - на странице найти ([ссылка](https://jing.yandex-team.ru/files/gavryushin/Screen%20Shot%202021-10-22%20at%2013.11.06.png) на картинку), сколько всего квоты `GENERIC_LINUX_HDD` и `GENERIC_LINUX_SSD`  выделено для сервиса (`total_hdd_quota` и `total_ssd_quota`)
    - перейти в графану (ссылка на странице *Open grafana*) и оценить максимальное потребление сервисом квоты `GENERIC_LINUX_HDD` и `GENERIC_LINUX_SSD` за прошлую неделю ([ссылка](https://jing.yandex-team.ru/files/gavryushin/Screen%20Shot%202021-10-22%20at%2021.47.08.png) на картинку) (`max_hdd_quota_consumption` и `max_ssd_quota_consumption`)
    - посчитать суммарную максимальную используемую квоту сервиса (`initial_max_quota_consumption`):
      ```
      max_hdd_quota_consumption + max_ssd_quota_consumption
      ```
    - посчитать свободную квоту сервиса (`free_quota`):
      ```
      (total_hdd_quota + total_ssd_quota) - initial_max_quota_consumption
      ```
  - запросить для сервиса квоту `GENERIC_LINUX_HDD` (или `GENERIC_LINUX_SSD`) в долг в размере `surfwax_selenoid_tasks_potential_quota_consumption_per_day`:
    - создаем задачу в QAFW с заявкой на перенос квоты (пример - https://st.yandex-team.ru/QAFW-4168). В рамках QAFW-задачи будет создана заявка в Диспенсере([пример](https://st.yandex-team.ru/DISPENSERTREQ-4084)), эту заявку должен принять ответственный из `abc`, за которым закреплена группа в Sandbox-е
    - записываем информацию о долге в [задачу FEI-24032](https://st.yandex-team.ru/FEI-24032)
    - после принятия железа ответственный за `abc` должен на странице `https://abc.yandex-team.ru/services/<abc-name>/folders/` в столбце "Провайдер" кликнуть в Sandbox, чтобы открыть провайдер ([картинка](https://jing.yandex-team.ru/files/gavryushin/2022-02-11%2013.20.08.jpg))
    - если операция делается впервые, то потребуется создание аккаунта с ролью «Управляющий квотами». Тут называем аккаунт ровно так же как и называется группа в Sandbox (**учитывая регистр**) и выбираем “Вычислительный кластер” в поле “Пространство аккаунтов” ([картинка](https://jing.yandex-team.ru/files/gavryushin/2022-02-11%2013.23.17.jpg))
    - ответственный за `abc` должен нажать кнопку "Спустить весь баланс" ([картинка](https://jing.yandex-team.ru/files/gavryushin/2022-02-11%2013.25.49.jpg))
    - проверить изменения квоты на графике `https://grafana.yandex-team.ru/d/000015873/sandbox-quota-consumption-production?orgId=1&var-owner=<YOUR_QUOTA_NAME>`
- настроить в staging окружении SurfWax-а квоту для сервиса (все последующие действия необходимо выполнять с базой, развернутой в [staging](https://yc.yandex-team.ru/folders/aku9fojph5675foon66g/ydb/databases/etn00ocfct9j340onqag/browse), через выполнения SQL-запросов в интерфейсе ([ссылка](https://jing.yandex-team.ru/files/gavryushin/Screen%20Shot%202021-10-22%20at%2015.02.53.png) на картинку)):
  - [создать](https://a.yandex-team.ru/arc/trunk/arcadia/frontend/projects/infratest/services/surfwax/README.md#создание-квоты) квоту для сервиса в [таблице](https://yc.yandex-team.ru/folders/aku9fojph5675foon66g/ydb/databases/etn00ocfct9j340onqag/browse?path=%2Fquota) базы данных
  - [добавить](https://a.yandex-team.ru/arc/trunk/arcadia/frontend/projects/infratest/services/surfwax/README.md#dobavlenie-brauzera-v-kvotu) необходимые браузеры в квоту сервиса в [таблицу](https://yc.yandex-team.ru/folders/aku9fojph5675foon66g/ydb/databases/etn00ocfct9j340onqag/browse?path=%2Fquotas_browsers) базы данных, браузеры станут доступны в течение получаса
  - добавить кэши браузеров, использующихся в сервисе, в таблицу базы данных:
    - если какой-то из уже переведенных сервисов на SurfWax использует такой же [набор браузеров](https://yc.yandex-team.ru/folders/aku9fojph5675foon66g/ydb/databases/etn00ocfct9j340onqag/browse?path=%2Fquotas_browsers), то [добавить](https://a.yandex-team.ru/arc/trunk/arcadia/frontend/projects/infratest/services/surfwax/README.md#dobavlenie-keshej-brauzerov-v-kvotu) уже существующий id кэша в [таблицу](https://yc.yandex-team.ru/folders/aku9fojph5675foon66g/ydb/databases/etn00ocfct9j340onqag/browse?path=%2Fbrowser_groups_caches) базы данных
    - если ни один из уже переведенных сервисов на SurfWax НЕ использует такой же набор браузеров, то [собрать](https://a.yandex-team.ru/arc/trunk/arcadia/frontend/projects/infratest/services/surfwax/README.md#sborka-keshej-brauzerov) и [добавить](https://a.yandex-team.ru/arc/trunk/arcadia/frontend/projects/infratest/services/surfwax/README.md#dobavlenie-keshej-brauzerov-v-kvotu) кэш в [таблицу](https://yc.yandex-team.ru/folders/aku9fojph5675foon66g/ydb/databases/etn00ocfct9j340onqag/browse?path=%2Fbrowser_groups_caches) базы данных
- запросить доступ роботу `robot-surfwax` до группы сервиса в Sandbox у ответственного за сервис
- перевести сервис на SurfWax, развернутый в окружении staging:
  - для соответствующих браузеров заменить в конфигах инструмента тестирования `sg.yandex-team.ru` на `http://<quota_name>@sw-staging.yandex-team.ru:80/v0` (в случае использования hermione необходимо изменять значение опции `gridUrl`), где `<quota_name>` – это соответствующее название квоты сервиса из [таблицы](https://yc.yandex-team.ru/folders/aku9fojph5675foon66g/ydb/databases/etn00ocfct9j340onqag/browse?path=%2Fquota) базы данных
  - увеличить в конфигах инструмента тестирования таймаут на время поднятия сессии до 150 секунд (в случае использования hermione необходимо изменять значение опции `sessionRequestTimeout`); это костыль, чтобы в yasm записывались данные по запросам на поднятие сессий, которые сервис не успел отдать за SLO в 120 секунд ([FEI-23812](https://st.yandex-team.ru/FEI-23812))
  - если сервис использует hermione в качестве запуска тестов:
    - обновить инструмент до >=4.4.1 или >=3.12.1, если сервис использует hermione@4.x или hermione@3.x соответственно, иначе завести в сервис задачу на обновление до более свежей версии
    - если удалось обновить hermione до минимально требуемой версии, то подключить плагин [hermione-surfwax-router](https://a.yandex-team.ru/arc/trunk/arcadia/frontend/projects/infratest/packages/hermione-surfwax-router) таким образом, чтобы он был включен только при запуске тестов в CI
    - если сервис использует плагин `hermione-debug`, то необходимо обновить плагин до последней версии и поправить опции согласно [документации](https://a.yandex-team.ru/arc/trunk/arcadia/frontend/projects/infratest/packages/hermione-debug/README.md#surfwax)
    - если сервис использует функциональность из плагина `html-reporter`, которая добавляет ссылку на логи сессий браузеров в html-отчет, то необходимо заменить значение опции `metaInfoBaseUrls.sessionId` с `https://selenium.yandex-team.ru/logs/` на `https://sw-staging.yandex-team.ru/log/`
  - Проверить:
    - в логах запуска тестов в CI для соответствующих браузеров id сессий содержат подстроку `--` (наличие двух дефисов подряд специфично только для сессий, которые были созданы с помощью SurfWax)
    - запуск тестов в CI стабильно проходит успешно
    - время запуска тестов в CI не увеличивается
    - количество ретраев в CI не увеличивается
    - корректно работает функциональность из плагина `hermione-debug` (если используется hermione и плагин подключен)
    - html-отчет содержит корректные ссылки на логи сессий (если используется hermione и подключена соответствующая функциональность)
- настроить в production окружении SurfWax-а квоту для сервиса по аналогии с тем, как настраивалась квота для окружения в staging (все последующие действия необходимо выполнять с базой, развернутой в [production](https://yc.yandex-team.ru/folders/aku9fojph5675foon66g/ydb/databases/etn00la4p1rbuf918p9u/browse), через выполнения SQL-запросов в интерфейсе)
- перевести сервис на SurfWax, развернутый в окружении production, заменив в конфигах инструмента тестирования `sw-staging.yandex-team.ru` на `sw.yandex-team.ru`
- еще раз проверить, что все работает корректно
- влить изменения
- через сутки после внедрения SurfWax:
  - открыть страницу `https://sandbox.yandex-team.ru/admin/groups/<group>/general`
  - перейти в графану и оценить максимальное потребление сервисом квоты `GENERIC_LINUX_HDD` и `GENERIC_LINUX_SSD` за прошлые сутки в единицах `qp` (`max_hdd_quota_consumption_with_surfwax` и `max_ssd_quota_consumption_with_surfwax`)
  - посчитать реальное потребление квоты задачами `SURFWAX_SELENOID` за день в единицах `qp` (`surfwax_selenoid_tasks_real_quota_consumption_per_day`):
    ```
    (max_hdd_quota_consumption_with_surfwax + max_ssd_quota_consumption_with_surfwax) - initial_max_quota_consumption
    ```
  - если `surfwax_selenoid_tasks_real_quota_consumption_per_day - surfwax_selenoid_tasks_potential_quota_consumption_per_day > 0`, то дозапросить для сервиса квоту `GENERIC_LINUX_HDD` (или `GENERIC_LINUX_SSD`) из группы [SEARCH_INTERFACES_BROWSERS](https://sandbox.yandex-team.ru/admin/groups/SEARCH_INTERFACES_BROWSERS/general) в долг в размере (записав долг в задачу [FEI-24032](https://st.yandex-team.ru/FEI-24032)):
    ```
    surfwax_selenoid_tasks_real_quota_consumption_per_day - surfwax_selenoid_tasks_potential_quota_consumption_per_day
    ```
  - если `surfwax_selenoid_tasks_real_quota_consumption_per_day - surfwax_selenoid_tasks_potential_quota_consumption_per_day < 0`, то вернуть часть взятой квоты в долг в группу [SEARCH_INTERFACES_BROWSERS](https://sandbox.yandex-team.ru/admin/groups/SEARCH_INTERFACES_BROWSERS/general) (зафиксировав часть возвращенного долга в задаче [FEI-24032](https://st.yandex-team.ru/FEI-24032))
- анонсировать в сервисе, что выполнен переход на SurfWax, и поддержка браузеров переехала в INFRADUTY (рассылка/канал/клубик) (пример [поста](https://clubs.at.yandex-team.ru/pcode/73) в этушке)
- добавить переведенный сервис в список тех, кто [уже использует SurfWax](https://a.yandex-team.ru/arc/trunk/arcadia/frontend/projects/infratest/services/surfwax#kto-uzhe-ispolьzuet-surfwax?)

### Эксперимент

> ⚠️ На данный момент под экспериментом ничего не запускается

Проект web4 может находиться под экспериментом, который заключается в том, чтобы постепенно перевести на SurfWax 100 % запусков hermione-тестов в каком-то конкретном браузере во всех сборочных контекстах (dev, pull-request, merge-queue).
Эксперимент включается/выключается в [генезисе](https://a.yandex-team.ru/arc/trunk/arcadia/serp/genisys/sandbox-ci/production/config.yml) через параметр `enable_surfwax_exp_for` со значениями от `0` до `1`, где `0` - эксперимент раскатан на 0 % сборок hermione-тестов, а `1` - эксперимент раскатан на 100 % сборок hermione-тестов.

### Как по id сессии определить задачу в Sandbox, в рамках которой она поднималась?

- выполнить:
  ```js
  node -e 'console.log(Buffer.from("<SESSION_ID>".split("--")[0], "base64").toString().match(/\[(.+)\]/)[1]);'
  ```
- в Sandbox в качестве типа задачи указать `SURFWAX_SELENOID`, а в качестве output-параметра указать `endpoint` со значением из вывода предыдущей команды
- по приблизительному времени создания сессии и времени создания задач `SURFWAX_SELENOID` можно оценить, в какой из задач предположительно поднималась сессия

### Потребление квоты

- [Дашбор](https://grafana.yandex-team.ru/d/000015873/sandbox-quota-consumption-production?orgId=1&var-owner=SEARCH_INTERFACES_BROWSERS&from=now-30d&to=now&refresh=1m) потребления квоты `SEARCH_INTERFACES_BROWSERS`
- [График](https://grafana.yandex-team.ru/d/000015873/sandbox-quota-consumption-production?viewPanel=5&orgId=1&refresh=1m&from=now-7d&to=now&var-owner=SEARCH_INTERFACES_BROWSERS&var-group_by_days=0) запущенных задач `SEARCH_INTERFACES_BROWSERS`
- [График](https://datalens.yandex-team.ru/preview/1mzcgewz12pev-graph?staticQuotaOwner=SEARCH_INTERFACES_BROWSERS&staticQuotaTaskType=SELENOID&staticQuotaTag=SANDBOX-ROUTER&dynamicQuotaOwner=SEARCH_INTERFACES_BROWSERS&dynamicQuotaTaskType=SURFWAX_SELENOID&dynamicQuotaTag=PRODUCTION) "статическая квота vs динамическая квота"
- [Дашборд](https://grafana.yandex-team.ru/d/000016022/sandbox-api-stats-for-user-production?orgId=1&var-user=robot-surfwax&var-quota_owner=SEARCH_INTERFACES_BROWSERS) потребления API квоты Sandbox роботом `robot-surfwax`

### Балансер

На сервисе настроен L3+L7-балансер с доменом `sw.yandex-team.ru` (`sw-staging.yandex-team.ru` для staging).

#### L3-балансер

- [production](https://l3.tt.yandex-team.ru/service/11714); [дашборд](https://grafana.yandex-team.ru/d/ZwwomqJMk/l3-vs-sw-yandex-team-ru?orgId=1) в графане
- [staging](https://l3.tt.yandex-team.ru/service/12704); [дашборд](https://grafana.yandex-team.ru/d/6-6ZZYQGz/l3-vs-sw-staging-yandex-team-ru?orgId=1) в графане

#### L7-балансер

Балансер настроен при помощи [awacs](https://wiki.yandex-team.ru/awacs/) (L3-балансер был автоматически создан и настроен при создании L7-балансера):

- [production](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/sw.yandex-team.ru/show/)
- [staging](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/sw-staging.yandex-team.ru/show/)

Вкладка с мониторингами находится на главной странице каждого из namespace-ов.

### Сервис в YDeploy

- [production](https://deploy.yandex-team.ru/stages/surfwax-production)
- [staging](https://deploy.yandex-team.ru/stages/surfwax-staging)

Вкладка с мониторингами находится на главной странице каждого из stage-ов.

### База в YDB

- [production](https://ydb.yandex-team.ru/db/ydb-ru/surfwax/production/surfwax/browser)
- [staging](https://ydb.yandex-team.ru/db/ydb-ru-prestable/surfwax/staging/surfwax/browser)

### Кастомные метрики

[Панель](https://yasm.yandex-team.ru/template/panel/surfax-panel) production окружения в Головане.

[Конфигурация](https://a.yandex-team.ru/arc/trunk/arcadia/frontend/projects/infratest/services/surfwax/monitoring/panels/surfwax/template.jinja2) панели находится рядом с кодом и после правок выгружается следующим образом из корня `surfwax`:

```bash
$ npm run yasm:upload
```

### Алерты

[Конфигурация](https://a.yandex-team.ru/arc/trunk/arcadia/frontend/projects/infratest/services/surfwax/monitoring/surfwax.monitorado.yml) алертов в juggler тоже находится рядом с кодом и выгружается с помощью инструмента [monitorado](https://a.yandex-team.ru/arc/trunk/arcadia/frontend/packages/monitorado#monitorado) из корня `surfwax`:

```bash
$ MONITORADO_OAUTH_TOKEN=<token> npm run monitoring:upload
```

Если вы не знаете `<token>`, то в логах первого запуска будет предоставлена ссылка для его получения.

### Разбор алертов

#### surfwax_selenoid_broken_status

Этот алерт срабатывает на регулярные падения задач `SURFWAX_SELENOID` в течение определённого промежутка времени (задаётся в конфигурации) и создаёт тикет в очередь `INFRADUTY`.

Разбор тикета в `INFRADUTY` происходит следующий образом:
- найти задачи `SURFWAX_SELENOID`, [время падения](https://sandbox.yandex-team.ru/tasks?children=false&author=robot-surfwax&status=FAILURE%2CEXCEPTION%2CTIMEOUT&tags=PRODUCTION&type=SURFWAX_SELENOID&order=-id&limit=100) которых матчится на время срабатывания алерта (ссылка на список упавших задач также есть в комментарии к соответствующему тикету в `INFRADUTY`)
- провести исследование на предмет системной проблемы с задачами `SURFWAX_SELENOID` (задачи чаще падают, чем завершаются успешно)
- в случае обнаружения системной проблемы разобраться с причиной с высоким приоритетом, иначе считать срабатывание мониторинга как `false positive` и закрыть тикет (если мониторинг часто срабатывает как `false positive`, то необходимо подкрутить пороги в конфигурации)

#### surfwax_session_create

Алёрт пока не настраивается через `monitorado`. [График](https://yasm.yandex-team.ru/alert/surfwax_session_create) алерта.

Этот алерт создаёт тикет в очередь `INFRADUTY` и срабатывает, если сервис в течение 60 секунд непрерывно проваливал SLO, то есть не отдавал сессии за 120 секунд.

**Срабатываение этого алерта является КРИТИЧНЫМ, так как сервис, предположительно, перестал работать.**

Возможные варианты разбора алерта и решения тикета в `INFRADUTY`:
- проверить [не проводятся ли учения](https://t.me/joinchat/PaZhvX5pm5phcPFN) в данный момент времени
  - если деградация работы сервиса связана с деградацией нижележащей инфраструктуры (Sandbox, YDB, YDeploy и т. д.), то необходимо создать или найти соответствующую задачу на разбор в сервисе-смежнике
  - если проблем в нижележащей инфраструктуре не обнаружено, то, скорее всего, проблема в самом сервисе ([FEI-22766](https://st.yandex-team.ru/FEI-22766))
- посмотреть [список задач](https://sandbox.yandex-team.ru/tasks?children=false&status=QUEUE&tags=PRODUCTION&type=SURFWAX_SELENOID&order=-id&limit=100) `SURFWAX_SELENOID` в статусах `QUEUE`. Если таких задач много, то это значит, что ресурсы перестали выделяться Sandbox-ом. Нужно разобраться с причиной, по которой задачи не стартуют (вообще нет [свободных агентов](https://sandbox.yandex-team.ru/clients/cpu?alive=true&busy=false&tags=GENERIC%20%26%20~MULTISLOT%20%26%20LINUX&limit=100500), недостаточно ресурсов в квоте, поломка на стороне Sandbox и т. д.).
- посмотреть [список задач](https://sandbox.yandex-team.ru/tasks?children=true&order=-id&status=EXECUTE&tags=PRODUCTION&type=SURFWAX_SELENOID&limit=100) `SURFWAX_SELENOID` в статусах `EXECUTE` и [количество запросов](https://yc.yandex-team.ru/folders/aku9fojph5675foon66g/ydb/databases/etn00la4p1rbuf918p9u/browse?path=%2Fqueue_counter_group) в очереди. Если в таблице в поле `queued` ненулевые значения, а новые задачи `SURFWAX_SELENOID` не стартуют, то проблема на стороне компонента `ordinator`:
  - если в таблице `queue_counter_group` в поле `queued` ненулевые значения наблюдаются только для какой-то конкретной квоты (поле `quota_name`), то нужно проверить не превышен ли для этой квоты лимит максимально запущенных задач `SURFWAX_SELENOID`. Лимит для квоты указан в таблице [quota](https://yc.yandex-team.ru/folders/aku9fojph5675foon66g/ydb/databases/etn00la4p1rbuf918p9u/browse?path=%2Fquota) в поле `agents_max_limit`. Количество задач, запущенных для квоты, можно сформировать на базе [фильтра](https://sandbox.yandex-team.ru/tasks?children=true&all_tags=true&order=-id&status=EXECUTE&tags=PRODUCTION&type=SURFWAX_SELENOID&limit=100), добавив в список тегов название квоты. Если для квоты превышен лимит запущенных задач `SURFWAX_SELENOID`, то необходимо понять действительно ли все эти задачи нужны и не перерасходуется ли квота впустую (для этого можно сопоставить максимальное число выделенных браузеров в задачах `SURFWAX_SELENOID` с реально создаваемой квотой нагрузкой). Если количество запущенных задач действительно необходимо, чтобы обслуживать увеличившуюся нагрузку от квоты, то поднять лимит:
    ```yql
    PRAGMA TablePathPrefix("/ru/surfwax/production/surfwax");

    UPDATE quota
    SET
      agents_max_limit = 100500 -- значение должно быть приемлемым
    WHERE
      name = "<quota_name>"
    ;
    ```
    Тикет в `INFRADUTY` в этом случае нужно закрыть в пользу задачи [FEI-23623](https://st.yandex-team.ru/FEI-23623).
  - посмотреть на [график](https://grafana.yandex-team.ru/d/000016022/sandbox-api-stats-for-user-production?orgId=1&var-user=robot-surfwax&var-quota_owner=SEARCH_INTERFACES_BROWSERS) потребления API квоты в Sandbox роботом `robot-surfwax`. При превышении потребления квоты нужно создать обращение вида `блокер` в [DEVTOOLSSUPPORT](https://forms.yandex-team.ru/surveys/devtools/) с просьбой увеличить квоту. Но перед этим нужно убедится, что выжирание API квоты не является следствием наших внутренних проблем (баг в одном из компонентов surfwax-а). Для этого необходимо найти [падающие таски SURFWAX_SELENOID](https://sandbox.yandex-team.ru/tasks?children=false&author=robot-surfwax&status=FAILURE%2CEXCEPTION%2CTIMEOUT&tags=PRODUCTION&type=SURFWAX_SELENOID&order=-id&limit=100) и понять насколько часто они сейчас падают и нет ли среди них ошибок указывающих на поломку сервиса. Т.е. возможно, что компонент `ordinator` создает новые задачи `SURFWAX_SELENOID` они быстро падают и он идет создавать еще столько же и так до бесконечности. В итоге вся квота API sandbox-а выжирается (пример такой проблемы - https://st.yandex-team.ru/INFRADUTY-21724). Если проблема в surfwax не обнаружена, то тикет в `INFRADUTY` нужно закрыть в пользу задач [FEI-23622](https://st.yandex-team.ru/FEI-23622) и [FEI-23925](https://st.yandex-team.ru/FEI-23925).
  - проанализировать [логи](https://deploy.yandex-team.ru/stages/surfwax-production/logs?deploy-unit=ordinator&limit=100) компонента `ordinator` на наличие ошибок и/или каких-то сообщений, позволяющих диагностировать проблему, скопировать лог в соответствующий тикет в `INFRADUTY` и призвать [gavryushin](https://staff.yandex-team.ru/gavryushin)
  - перейти к таблице [locks](https://yc.yandex-team.ru/folders/aku9fojph5675foon66g/ydb/databases/etn00la4p1rbuf918p9u/browse?path=%2Flocks) в базе и посмотреть обновляются ли значения колонки `locked_at`. Если значения не обновляются, то это значит, что сервис по какой-то причине "поймал" deadlock, нужно призвать [gavryushin](https://staff.yandex-team.ru/gavryushin) в соответствующий тикет в `INFRADUTY`. Для восстановления работоспособности сервиса необходимо сбросить все значения колонки `locked_at` в `null`:
    ```yql
    PRAGMA TablePathPrefix("/ru/surfwax/production/surfwax");

    UPDATE locks
    SET
      locked_at = null
    ;
    ```
- если по [графику](https://yasm.yandex-team.ru/template/panel/surfax-panel/-/2/) видно, что сессии через какое-то время стали отдаваться менее чем за 120 секунд, то есть сервис не сломан, то прикрепить инцидент к эпику [FEI-23650](https://st.yandex-team.ru/FEI-23650) про снижение SLO на выдачу сессий
- если ничего не помогает, то передеплоить сервис (с призывом [gavryushin](https://staff.yandex-team.ru/gavryushin) в соответствующий `INFRADUTY` тикет):
  - [перейти](https://deploy.yandex-team.ru/stages/surfwax-production/edit/du-webdriver-proxy/box-web-app/wl-workload) в настройки конфигурации компонента `webdriver-proxy` в YDeploy
  - изменить значение переменной окружения `ZERO_DIFF` (с `1` на `0` или наоборот)
  - прожать `Update`, а затем `Deploy`

### Заканчивается квота в S3

Если на почту пришло письмо следующего содержания:
```
Привет!

Вы получили это письмо, так как являетесь ответственным за проект "SurfWax" в Dispenser (https://dispenser.yandex-team.ru/db/projects/surfwax).
Потребление по квоте "Квота на HDD" в сервисе "S3" для проекта "SurfWax" превысило лимит в 80 %...
```
то необходимо увеличить квоту HDD в S3 для проекта SurfWax. Это делается следующим образом:
- перейти в [список шаблонов](https://st.yandex-team.ru/createTicket?queue=MDSSUPPORT) задач очереди `MDSSUPPORT`
- выбрать шаблон "Перенести квоту"
- в форме заполнить поля:
  - Откуда перенести квоту? `S3`
  - ABC-сервис откуда перенести: `Инфраструктура разработки фронтенда (FEI)`
  - Куда перенести квоту? `S3`
  - ABC-сервис куда перенести: `SurfWax`
  - Сколько квоты перенести: `2 TiB`
- будет создана задача, в рамках которой квота будет увеличена

### Сборка LXC-контейнера для задачи SURFWAX_SELENOID

- выполнить:
    ```bash
    $ npm run build-spec && node ./build-spec/__helpers__/build_lxc.js
    ```
- в логах предыдущей команды появится id-задачи в Sandbox, которая создаёт LXC-ресурс
- на странице созданного ресурса прожать кнопку Important, чтобы выставился атрибут `ttl=inf`
- указать в параметре `container` задачи [SURFWAX_SELENOID](https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/projects/surfwax/selenoid/__init__.py) в качестве дефолтного значения id ранее созданного ресурса

### Создание квоты

Создание квоты возможно в ручном и в автоматическом режимах.

#### Автоматический режим

Для заведения квоты в автоматическом режиме используется интерактивный скрипт из папки `scripts/sw-quota-tools`. Подробнее смотрите в [документации скрипта](https://a.yandex-team.ru/arc/trunk/arcadia/frontend/projects/infratest/services/surfwax/scripts/sw-quota-tools/README.md). Перед использованием скрипта следует ознакомиться с документацией про заведение квоты в ручном режиме для лучшего понимания процесса.

#### Ручной режим

```yql
--!syntax_v1

-- Добавление квоты "default"

PRAGMA TablePathPrefix("/ru-prestable/surfwax/staging/surfwax");
-- PRAGMA TablePathPrefix("/ru/surfwax/production/surfwax");

INSERT INTO
    quota
    (id, name, created_at, owner, agents_max_limit, agent_kill_timeout_ms, agent_queue_time_limit_ms, agent_secret_id)
VALUES
    (
        RandomUuid(0),
        "default", -- название квоты, как правило, совпадает с именем сервиса
        CurrentUtcTimestamp(),
        "DEFAULT", -- название группы в Sandbox, под которой будут запускаться задачи `SURFWAX_SELENOID`
        200, -- максимально допустимое количество одновременно запущенных задач `SURFWAX_SELENOID`,
             -- при превышении которого новые задачи создаваться не будут, как правило, расчитывается из пиковой нагрузки
        1200000, -- ttl задачи `SURFWAX_SELENOID`, которое определяется как среднее время выполнения
                 -- одного успешного запуска тестов с округлением вверх до значения кратного пяти + 5 min
        300000, -- суммарное допустимое время простоя задач `SURFWAX_SELENOID` в статусах `QUEUE` в единицу времени,
                -- при превышения которого новые задачи создаваться не будут, как правило, можно оставить без изменений для всех квот
        "sec-01f470dn6b1f8683v4js63kn05" -- оставить без изменений для всех квот
    );
```

### Добавление браузера в квоту

- убедиться, что для браузера определена группа в таблице `browser_groups`, если нет, то добавить следующим образом:
    ```yql
    --!syntax_v1

    -- Добавление группы "desktop-linux"

    PRAGMA TablePathPrefix("/ru-prestable/surfwax/staging/surfwax");
    -- PRAGMA TablePathPrefix("/ru/surfwax/production/surfwax");

    INSERT INTO
        browser_groups
        (
            name,
            platform,
            sessions_per_agent_limit,
            cpu_cores_per_session,
            ramdrive_gb_per_session,
            ram_gb_per_session,
            ramdrive_size_gb,
            session_request_timeout_ms, -- тайм аут на общее поднятие сессии
            session_startup_timeout_ms, -- тайм аут выполнения запроса сессии от webproxy к agent
            browser_platform
        )
    VALUES
    (
        "desktop-linux",
        "linux",
        0,
        1.1428,
        1,
        1,
        28,
        120000,
        60000,
        "Linux"
    );
    ```
- убедиться, что нужный браузер существует в таблице `browsers`, если нет, то добавить следующим образом:
    ```yql
    --!syntax_v1

    -- Добавление браузера "chrome" версии "72.1" с соответствующим конфигом в формате Yson

    PRAGMA TablePathPrefix("/ru-prestable/surfwax/staging/surfwax");
    -- PRAGMA TablePathPrefix("/ru/surfwax/production/surfwax");

    INSERT INTO
        browsers
        (id, name, version, group, config, created_at)
    VALUES
        (
            RandomUuid(0),
            "chrome",
            "72.1",
            "desktop-linux",
            -- нужно использовать образ из 'registry.yandex.net', иначе, как правило,
            -- образ придется пересобирать с учетом дополнительных требований сервиса и специфики нижележащей инфраструктуры
            '{"image"="registry.yandex.net/selenium/chrome:72.0-devtools";"path"="/";"port"= "4444";"tmpfs"={"/tmp"="size=128m"}}',
            CurrentUtcTimestamp()
        );
    ```
- добавить браузер в таблицу `quotas_browsers_relation` в нужную квоту следующим образом:
    ```yql
    --!syntax_v1

    -- Добавление браузера "chrome" версии "72.1" в квоту "default"

    PRAGMA TablePathPrefix("/ru-prestable/surfwax/staging/surfwax");
    -- PRAGMA TablePathPrefix("/ru/surfwax/production/surfwax");

    INSERT INTO
        quotas_browsers_relation
        (id, quota_id, browser_id, created_at)
    VALUES
        (
            RandomUuid(0),
            "<QUOTA_ID>", -- нужно подставить uuid нужной квоты из таблицы quota
            "<BROWSER_ID>", -- нужно подставить uuid нужного браузера из таблицы browsers
            CurrentUtcTimestamp()
        );
    ```

### Удаление браузера из квоты

Удаление браузера из квоты происходит путём инициализации колонки `deleted_at` у удаляемого браузера:
```yql
--!syntax_v1

PRAGMA TablePathPrefix("/ru-prestable/surfwax/staging/surfwax");
-- PRAGMA TablePathPrefix("/ru/surfwax/production/surfwax");

UPDATE quotas_browsers_relation
SET
    deleted_at = CurrentUtcTimestamp()
WHERE
    quota_id = "<QUOTA_ID>" AND -- нужно подставить uuid нужной квоты из таблицы quota
    browser_id = "<BROWSER_ID>"; -- нужно подставить uuid нужного браузера из таблицы browsers
```

### Перенос браузера из одной группы в другую

Знание о том, к какой группе принадлежит браузер, находится в таблице `browsers` в колонке `group`. Перенос браузера из одной группы в другую осуществляется следующими изменениями в этой таблице:
```yql
--!syntax_v1

-- Перенос браузера "chrome" версии "72.1" из группы "linux" в группу "desktop-linux"
-- осуществляется путём инициализации колонки `deleted_at` у браузера из группы "linux" и
-- добавления нового такого же браузера, но со значением "desktop-linux" у колонки `group`

PRAGMA TablePathPrefix("/ru-prestable/surfwax/staging/surfwax");
-- PRAGMA TablePathPrefix("/ru/surfwax/production/surfwax");

UPDATE browsers
SET
    deleted_at = CurrentUtcTimestamp()
WHERE name = "chrome" AND version = "72.1" AND group = "linux";

REPLACE INTO browsers
    (id, name, version, group, config, created_at)
VALUES (
    '<BROWSER_ID>',
    'chrome',
    '72.1',
    'desktop-linux',
    '{"image"="registry.yandex.net/selenium/chrome:72.0-devtools";"path"="/";"port"="4444"}',
    CurrentUtcTimestamp()
);
```

### Добавление датацентра в исключения для квоты

Исключение датацентра происходит путем добавления его в список из колонки `exclude_dcs`:
```yql
--!syntax_v1

-- Добавление датацентра "MAN" в исключения на подъем сессий для квоты "music"

PRAGMA TablePathPrefix("/ru-prestable/surfwax/staging/surfwax");
-- PRAGMA TablePathPrefix("/ru/surfwax/production/surfwax");

UPDATE quota
SET
    exclude_dcs = Yson::From(['MAN'])
WHERE name == 'music';
```

### Кэши браузеров

#### Сборка кэшей браузеров

- перейти в [последнюю успешную задачу](https://sandbox.yandex-team.ru/tasks?children=true&status=SUCCESS&type=SURFWAX_BUILD_LAYERS_CACHE&order=-id&limit=20&input_parameters=%7B%22cache_type%22%3A%22browsers%22%7D) `SURFWAX_BUILD_LAYERS_CACHE`
- перезапустить задачу `SURFWAX_BUILD_LAYERS_CACHE`, выставив параметр `cache_type` в значение `browsers` и изменив значение параметра `browsers` таким образом, чтобы оно соответствовало списку браузеров из таблицы `quotas_browsers` для необходимой квоты в базе
- при успешном завершении задача `SURFWAX_BUILD_LAYERS_CACHE` сварит ресурс `SURFWAX_LAYERS_CACHE`
- перейти на страницу ресурса и прожать кнопку Important (это добавит ресурсу атрибут `ttl=inf`)

#### Добавление кэшей браузеров в квоту

Добавить id ресурса в таблицу `browser_groups_caches` для нужной квоты следующим образом:
```yql
--!syntax_v1

-- Добавление кэша для квоты "default" и группы браузеров "desktop-linux"

PRAGMA TablePathPrefix("/ru-prestable/surfwax/staging/surfwax");
-- PRAGMA TablePathPrefix("/ru/surfwax/production/surfwax");

INSERT INTO
    browser_groups_caches
    (quota_name, browser_group, cache_id)
VALUES (
    "default",
    "desktop-linux",
    100500 -- id ресурса в Sandbox
);
```

#### Раскатка кэшей браузеров по sandbox-клиентам

После сборки кэшей браузеров, есть возможность предварительно загрузить эти ресурсы на sandbox-клиенты, чтобы сократить время на их получение в задаче `SURFWAX_SELENOID`.

Для этого необходимо:

- создать задачу `SURFWAX_SYNC_RESOURCES`
- указать осмысленное описание, которое даст понять цель задачи
- если знаете какие конкретно ресурсы нужно раскатить по клиентам
  - выставить параметр `Source for getting resources` в значение `Custom`
  - в параметре `Resources` указать необходимые ресурсы
- если знаете ресурсы каких квот нужно раскатить
  - выставить параметр `Source for getting resources` в значение `From DB`
  - указать в параметре `Source environment` из какой БД необходимо получать список ресурсов (по умолчанию `production`)
  - в параметре `Quota names` указать список необходимых квот. Если оставить список пустым, то будут использованы все квоты. :warning: Подумайте, есть ли в этом необходимость и не будет ли лучше указать конкретные квоты
- указать в параметре `Agents coverage`, в пределах от 0 (*не  включая*) до 1, процент клиентов, на которые будут раскатаны ресурсы (по умолчанию `1`)

## Локальная среда разработки

> ⚠️ На маках разрабатываться [не получится](https://docs.docker.com/config/daemon/ipv6/), так как сервис поднимается в докер-контейнерах, из которых нужен доступ к YDB, которая IPV6 -only. Дальнейшая инструкция подходит для разработки только на Linux-хостах (в частности на виртуалках в QYP).

### Пререквизиты

- [установить](https://docs.docker.com/engine/install/ubuntu/) docker
- [установить](https://docs.docker.com/compose/install/) docker-compose версии `1.27.4` (TODO: необходимо поддержать более свежие версии docker-compose)
- [залогиниться](https://wiki.yandex-team.ru/qloud/docker-registry/#cli) в `registry.yandex.net`
- если Linux-host IPV6-only (виртуалки в QYP, как правило, IPV6-only):
  - указать в `/etc/docker/daemon.json`:
    ```json
    {
      "ipv6": true,
      "fixed-cidr-v6": "fd00::/80"
    }
    ```
  - если окружение настраивается на виртуалке в QYP, то выполнить:
    ```bash
    $ sudo ip6tables -t nat -A POSTROUTING -s fd00::/80 ! -o docker0 -j MASQUERADE # в случае перезагрузки виртуалки необходимо эту команду выполнить снова
    $ sudo systemctl stop docker.service
    $ sudo ip link delete docker0
    $ sudo systemctl start docker.service
    ```
- должна быть возможность запускать докер без рута:
    ```bash
    # создать группу, если ее нет
    sudo groupadd docker
    # добавить юзера в группу
    sudo usermod -aG docker $USER
    newgrp docker

    # проверить
    docker run hello-world

    # если не помогло - ребут
    ```


- [создать](https://ydb.yandex-team.ru/docs/getting_started/create_manage_database) базу в YDB (рекомендуется использовать многодатацентровый кластер, например, ydb-ru)
- [смонтировать](https://docs.yandex-team.ru/devtools/intro/quick-start-guide#mount) исходники Arc с дополнительной опцией `--allow-root`:
    ```bash
    # в /etc/fuse.conf должна быть включена опция user_allow_other
    $ arc mount -m arcadia/ -S store/ --allow-root
    ```

### Подготовка окружения

[Выполнить](https://a.yandex-team.ru/arc/trunk/arcadia/frontend/projects/infratest#разработка) необходимые действия для разработки в infratest.

Из корня `surfwax`:
- `npm run setup-env`, после чего в файле `.env`
  - в переменную `YDB_TOKEN` положить [токен](https://yql.yandex-team.ru/oauth)
  - в переменную `SANDBOX_TOKEN` положить [токен](https://sandbox.yandex-team.ru/oauth/token)
- указать в `./config/db/development.json` (значения `entrypoint` и `database` могут отличаться, их можно узнать в [YDB UI](https://ydb.yandex-team.ru/databases) на вкладке Info после перехода в конкретную базу):
    ```json
    {
      "entrypoint": "ydb-ru.yandex.net:2135",
      "database": "/ru/home/<login>/mydb"
    }
    ```
- инициализировать базу:
    ```bash
    npm run up -- migrator
    ```
- перейти в созданную базу в [интерфейсе](https://ydb.yandex-team.ru/databases) и через YQL Kit:
  - инициализировать группы браузеров `desktop-linux` и `android`:
      ```yql
      --!syntax_v1

      PRAGMA TablePathPrefix("/ru/home/<login>/mydb/<login>_dev"); -- тут нужно обратить внимание, что <login> нужно указать свой

      INSERT INTO
          browser_groups
          (
              name,
              platform,
              sessions_per_agent_limit,
              cpu_cores_per_session,
              ramdrive_gb_per_session,
              ram_gb_per_session,
              ramdrive_size_gb,
              session_request_timeout_ms,
              session_startup_timeout_ms,
              browser_platform
          )
      VALUES
          (
              "desktop-linux",
              "linux",
              0,
              1.1428,
              1,
              1,
              28,
              120000,
              60000,
              "Linux"
          ),
          (
            "android",
            "linux",
            0,
            3.5555,
            1.4,
            1.4,
            28,
            180000,
            120000,
            "Android"
          );
      ```
  - инициализировать дефолтную квоту:
      ```yql
      --!syntax_v1

      PRAGMA TablePathPrefix("/ru/home/<login>/mydb/<login>_dev"); -- тут нужно обратить внимание, что <login> нужно указать свой

      INSERT INTO
          quota
          (id, name, created_at, owner, agents_max_limit, agent_kill_timeout_ms, agent_queue_time_limit_ms, agent_secret_id)
      VALUES
          (
              RandomUuid(0),
              "default",
              CurrentUtcTimestamp(),
              "SURFWAX_STAGING_BROWSERS",
              20,
              1200000,
              300000,
              "sec-01f470dn6b1f8683v4js63kn05"
          );
      ```
  - инициализировать дефолтный список доступных браузеров:
      ```yql
      --!syntax_v1

      PRAGMA TablePathPrefix("/ru/home/<login>/mydb/<login>_dev"); -- тут нужно обратить внимание, что <login> нужно указать свой

      INSERT INTO
          browsers
          (id, name, version, group, config, created_at)
      VALUES
          (
              RandomUuid(0),
              "chrome",
              "85.0",
              "desktop-linux",
              '{"image"="registry.yandex.net/selenium/chrome:85.0";"path"="/";"port"= "4444";"tmpfs"={"/tmp"="size=128m"}}',
              CurrentUtcTimestamp() - DateTime::IntervalFromMinutes(60)
          ),
          (
              RandomUuid(0),
              "firefox",
              "79.0",
              "desktop-linux",
              '{"image"="registry.yandex.net/selenium/firefox:79.0";"path"="/wd/hub";"port"= "4444";"tmpfs"={"/tmp"="size=128m"}}',
              CurrentUtcTimestamp() - DateTime::IntervalFromMinutes(60)
          ),
          (
              RandomUuid(0),
              "chrome",
              "phone-73.0",
              "android",
              '{"image"="registry.yandex.net/selenium/chrome:phone-73.0";"path"="/wd/hub";"port"= "4723"}',
              CurrentUtcTimestamp() - DateTime::IntervalFromMinutes(60)
          ),
          (
              RandomUuid(0),
              "android-phone",
              "searchapp-8.80",
              "android",
              '{"image"="registry.yandex.net/selenium/android-phone:searchapp-8.80-light";"port"= "4723"}',
              CurrentUtcTimestamp() - DateTime::IntervalFromMinutes(60)
          );
      ```
   - инициализировать список доступных браузеров в квоте `default`:
       ```yql
       --!syntax_v1

       PRAGMA TablePathPrefix("/ru/home/<login>/mydb/<login>_dev"); -- тут нужно обратить внимание, что <login> нужно указать свой

       INSERT INTO
           quotas_browsers_relation
           (id, quota_id, browser_id, created_at)
       VALUES
           (
               RandomUuid(0),
               "<QUOTA_ID>", -- нужно подставить uuid нужной квоты из таблицы quota
               "<BROWSER_ID>", -- нужно подставить uuid нужного браузера из таблицы browsers
               CurrentUtcTimestamp() - DateTime::IntervalFromMinutes(30)
           ),
           (
               RandomUuid(1),
               "<QUOTA_ID>", -- нужно подставить uuid нужной квоты из таблицы quota
               "<BROWSER_ID>", -- нужно подставить uuid нужного браузера из таблицы browsers
               CurrentUtcTimestamp() - DateTime::IntervalFromMinutes(30)
           )
           -- ...
     ;
       ```
   - добавить кэши для браузеров:
      ```yql
       --!syntax_v1

       PRAGMA TablePathPrefix("/ru/home/<login>/mydb/<login>_dev"); -- тут нужно обратить внимание, что <login> нужно указать свой

       INSERT INTO
           browser_groups_caches
           (quota_name, browser_group, cache_id)
       VALUES
           (
               "default",
               "desktop-linux",
               2457109879
           ),
           (
               "default",
               "android",
               2658152554
           );
        ```
- загрузить образы (полный список доступных браузеров и их версий указан в [таблице](https://ydb.yandex-team.ru/db/ydb-ru/surfwax/production/surfwax/browser/supported_browsers) продовой базы):
  - `docker pull registry.yandex.net/selenium/chrome:85.0`
  - `docker pull registry.yandex.net/selenium/firefox:79.0`
  - `docker pull registry.yandex.net/selenium/chrome:phone-73.0`,
  - `docker pull registry.yandex.net/selenium/android-phone:searchapp-8.80-light`
  - `docker pull registry.yandex.net/selenium/video-recorder:latest-release` (образ для записи видео; запись видео включается добавлением `enableVideo: true` в capabilities браузера; директория, в которую сохраняется видео, указана в [docker-compose.yml](https://a.yandex-team.ru/arc/trunk/arcadia/frontend/projects/infratest/services/surfwax/docker-compose.yml))

- вписать нужные образы в `selenoid/browsers.json`.

### Запуск сервиса без ординатора

> ⚠️ Подходит для тестирования, если правки не затрагивают код ординатора

Из корня `surfwax`:
- `npm run up -- webdriverproxy coordinator selenoid agent`, после чего в логах должно появиться примерно следующее:
  ```bash
  coordinator_1     | {"level":20,"time":1620920565675,"pid":20,"hostname":"gavryushin-dev.sas.yp-c.yandex.net","msg":"Acquired session ydb://session/3?node_id=17985&id=MTkzNjUwODQtNzk0ODg3YjgtNDMyOTc3YTEtMTg3M2UzYTc= on endpoint ydb-ru-sas-1028.search.yandex.net:31021."}
  ```

### Запуск сервиса с ординатором

Предварительно нужно обеспечить доступ от Sandbox-машин до вашей QYP-машины, это делается через [puncher](https://puncher.yandex-team.ru/?rules=exclude_rejected&values=all&sort=creation_time), где необходимо создать правило от источника `_CMSEARCHNETS_` до сети, в которой находится ваша QYP-машина, протокол `TCP`, порт `10000` (если ваша машина находится в сети `_FEI_DEV_NETS_`, то ничего делать не нужно, так как доступ уже [есть](https://puncher.yandex-team.ru/?id=608a908ccf1f7b8525778d7e)).

Если разработка ведётся на локальной машине, то необходимо проложить туннель от QYP-машины до локального координатора:
- на QYP-машине добавить строку `GatewayPorts yes` в файл `/etc/ssh/sshd_config` и перезапустить ssh-сессию через команду `sudo service ssh restart`
- на локальной машине в отдельной вкладке терминала выполнить:
  ```bash
  $ ssh -R 10000:localhost:10000 -N {user}@{hostname} -v
  ```
  где `user` - логин на staff, `hostname` - адрес QYP-машины

В корне `surfwax`:
- указать в `./config/ordinator/development.json`:
  ```json
  {
      "taskReleaseType": "stable",
      "coordinatorAddress": {
          "type": "endpoint",
          "endpoint": "<HOSTNAME>:10000"
      },
      "taskSearchTag": "<TAG>"
  }
  ```
  где
  - `<HOSTNAME>` - адрес QYP-машины
  - `<TAG>` - тег, с которым будут создаваться задачи в Sandbox (лучше использовать теги вида `DEVELOPMENT-<USERNAME>`)
- `npm run up -- webdriverproxy coordinator ordinator`, после чего в логах должно появиться примерно следующее:
  ```bash
  webdriverproxy_1  | {"level":20,"time":1620920384142,"pid":20,"hostname":"gavryushin-dev.sas.yp-c.yandex.net","msg":"Released session ydb://session/3?node_id=17985&id=N2VjOGI3ZTktZDgzN2U4NGYtNmNkNzY4Y2UtYjI5ODNjYzY= on endpoint ydb-ru-sas-1028.search.yandex.net:31021."}
  coordinator_1     | {"level":20,"time":1620920401922,"pid":20,"hostname":"gavryushin-dev.sas.yp-c.yandex.net","msg":"Acquired session ydb://session/3?node_id=17985&id=YmRhYjNiZGEtZDFkZjA1MTYtODVjZmUwYi05NTViYmM0Ng== on endpoint ydb-ru-sas-1028.search.yandex.net:31021."}
  ```

### Тест работоспособности

После запуска сервиса необходимо запустить проверочные hermione-тесты на версии hermione@3 и hermione@4:
- `cd hermione`
- `npm ci`
- `npm run hermione-v3` (запуск тестов на версии hermione@3)
- `npm run hermione` (запуск тестов на версии hermione@4)
- тесты в обоих версиях должны пройти успешно

### Завершение работы

- `npm run down` - остановить сервисы
- `npm run cleanup` - удалить контейнеры, сети и тома сервисов

## Релиз новой версии

### Пререквизиты

- запросить роль [разработчика](https://abc.yandex-team.ru/services/surfwax/?scope=development) SurfWax с помощью [IDM](https://idm.yandex-team.ru)
- если необходимо накатить изменения в базу, запросить роль [администратора](https://abc.yandex-team.ru/services/surfwax/?scope=administration) SurfWax с помощью [IDM](https://idm.yandex-team.ru)
- [установить](https://docs.docker.com/engine/install/ubuntu/) docker
- [установить](https://docs.yandex-team.ru/devtools/intro/quick-start-guide#ya-setup) ya

### Раскатка сервиса

В корне `surfwax`:
- `arc checkout trunk && arc pull trunk`
- `npm run build`

#### Раскатка в staging

- проверить, что [surfwax-agent](https://a.yandex-team.ru/arc/trunk/arcadia/frontend/projects/infratest/packages/surfwax-agent) уже выложен как докер-образ
  - взять токен от docker registry [по инструкции](https://wiki.yandex-team.ru/docker-registry/#authorization)
  - выполнить `curl -H "Authorization: OAuth <TOKEN>" -v https://registry.yandex.net/v2/search-interfaces/surfwax-agent/tags/list`
  - пример ответа: `{"name":"search-interfaces/surfwax-agent","tags":["0.8.4-mcheshkov"]}`
  - в списке тэгов должна быть версия, совпадающая с версией пакета `@yandex-int/surfwax-agent` из [package.json](https://a.yandex-team.ru/arc/trunk/arcadia/frontend/projects/infratest/services/surfwax/package.json)
  - если нужного тэга нет, то необходимо опубликовать образ `surfwax-agent` по [документации](https://a.yandex-team.ru/arc/trunk/arcadia/frontend/projects/infratest/packages/surfwax-agent#sborka-obraza)
  - добавить id ресурса, полученный на предыдущем шаге, в [дефолтное значение](https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/projects/surfwax/selenoid/__init__.py) параметра `surfwax_layers_cache_resources` задачи `SURFWAX_SELENOID`
- если необходимо накатить архитектурные изменения в базу:
  - выполнить:
    ```bash
    YDB_TOKEN=<token> SURFWAX_ENV=staging node ./build/bin/migrator.js -- migrate
    ```
    где `YDB_TOKEN` находится [тут](https://yql.yandex-team.ru/oauth)
  - собрать и выполнить код, запускающий тестирование на staging, чтобы убедиться, что новые изменения в базу являются обратно совместимыми, то есть не будет даунтайма сервиса:
    ```bash
    $ npm run build-spec && node ./build-spec/__helpers__/staging.js
    ```
  - в логах предыдущей команды появится id-задачи в Sandbox, которая запускает hermione-тесты в web4 и должна завершиться успешно
- удалить tar-файл, созданный при выкатке предыдущей версии:
    ```bash
    $ rm -f *.tgz
    ```
- опубликовать новые образы:
    ```bash
    $ make docker-publish
    ```
- cтриггерить релиз в [Deploy](https://deploy.yandex-team.ru), что создаст релизные тикеты (версия берётся из `package.json`):
    ```bash
    $ ya tool dctl release docker search-interfaces/surfwax-coordinator -t `node -e 'console.log(require("./package.json").version)'`
    $ ya tool dctl release docker search-interfaces/surfwax-ordinator -t `node -e 'console.log(require("./package.json").version)'`
    $ ya tool dctl release docker search-interfaces/surfwax-webdriverproxy -t `node -e 'console.log(require("./package.json").version)'`
    ```
- выполнить коммит релизных тикетов в [staging](https://deploy.yandex-team.ru/stages/surfwax-staging/deploy-tickets)
- подождать деплоя на вкладке [status](https://deploy.yandex-team.ru/stages/surfwax-staging)
- собрать и выполнить код, запускающий тестирование на staging:
  ```bash
  $ npm run build-spec && node ./build-spec/__helpers__/staging.js
  ```
- в логах предыдущей команды появится id-задачи в Sandbox, которая запускает hermione-тесты в web4 и должна завершиться успешно

#### Раскатка в production

- изменения в sandbox-задачах раскатываются автоматически только в staging, для раскатки в production надо найти запуск Flow на [странице проекта](https://a.yandex-team.ru/projects/surfwax/ci/actions/launches?dir=sandbox%2Fprojects%2Fsurfwax&id=surfwax_selenoid) в New CI, открыть его кнопкой `Open flow` и прожать ручное подтверждение у кубика деплоя в прод
- если необходимо накатить изменения в базу, выполнить:
  ```bash
  YDB_TOKEN=<token> SURFWAX_ENV=production node ./build/bin/migrator.js -- migrate
  ```
  где `YDB_TOKEN` находится [тут](https://yql.yandex-team.ru/oauth)
- выполнить коммит релизных тикетов в [production](https://deploy.yandex-team.ru/stages/surfwax-production/deploy-tickets) и подождать деплоя на вкладке [status](https://deploy.yandex-team.ru/stages/surfwax-production)
- убедиться, что в проде всё работает корректно
- если при раскатке на staging в параметр `surfwax_layers_cache_resources` задачи `SURFWAX_SELENOID` были добавлены новые значения, то в этот момент можно удалить неактуальные ресурсы (например, ресурсы с предыдущей версией `surfwax-agent`)
