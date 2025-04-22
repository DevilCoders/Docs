### Разработка
- Добавиться в [abc-группу](https://abc.yandex-team.ru/services/marketpromo/)
так появится доступ до балансеров и няни
- Запросить доступы
[к интерфейсу](https://wiki.yandex-team.ru/market/pokupka/projects/promo-actions/assortment-ki/dev/#polucheniedostupov)
и
[на релизы](https://tsum.yandex-team.ru/pipe/projects/Promo/delivery-dashboard/marketpromo-ciface-promo)

- Установите [утилиту ya](https://wiki.yandex-team.ru/yatool/distrib/).
- Для работы с репозиторием используйте [arc](https://arc-vcs.yandex-team.ru/docs/setup/arc/install.html),
 [FAQ по arc](https://wiki.yandex-team.ru/arcadia/arc/faq/)
- Используется java 11
    - Установка на macos через [brew](http://brew.sh/):
         `brew cask install homebrew/cask-versions/java11`
    - Ручная установка с сайта
      [Oracle](https://www.oracle.com/technetwork/java/javase/downloads/jdk11-downloads-5066655.html)
- Установите [Docker](https://docs.docker.com/get-docker/) для локального запуска ydb
- Установите [Docker compose](https://docs.docker.com/compose/install/)
- Авторизуйтесь во внутреннем [Docker registry](https://wiki.yandex-team.ru/docker-registry/#authorization)
- Затянуть с registry образ ydb
  `docker pull registry.yandex.net/yandex-docker-local-ydb:stable`
- Проверить доступ к [datasources-ng](https://github.yandex-team.ru/cs-admin/datasources-ng); если его нет - запросить [вот так](https://st.yandex-team.ru/CSADMIN-33887)
  
### Локальный запуск
1) Настроить недостающие проперти в файл `ciface-promo/src/main/properties.d/local/00-ciface-promo.properties`
 - прописать YT-токен можно свой ([как получить](https://wiki.yandex-team.ru/market/analytics/stackoverflow-analitiki-marketa/yt/gde-vzjat-token-dlja-yt/))
 - остальное можно забрать из [datasources-ng](https://github.yandex-team.ru/cs-admin/datasources-ng) (префикс для пропертей: `market.marketpromo.ciface-promo`). Для минимального запуска можно пропустить.

2) Запустить ydb локально
  ```
  docker run --hostname localhost -dp 2135:2135 registry.yandex.net/yandex-docker-local-ydb:stable
  ```

Теперь можно к ней делать какие-то запросы. Примеры запросов: 
```
ya ydb -e localhost:2135 -d /local scheme ls
ya ydb -e localhost:2135 -d /local table query execute -q '--!syntax_v1
  select * from directional_promo_properties;'
ya ydb -e localhost:2135 -d /local scheme describe /local/directional_promo_properties
```

3) Сгенерировать проект.
Выполнить скрипт из папки [/market/marketpromo/ciface-promo](https://arcanum.yandex-team.ru/arc/trunk/arcadia/market/marketpromo/ciface-promo) под аркадией для создания проекта для Intellij Idea. (Вместо $PROJECTS_PATH/$PROJECT_NAME указать удобную директорию для проекта вне аркадии)
```
ya ide idea \
-DUSE_PREBUILT_TOOLS \
--host-platform-flag=USE_PREBUILT_TOOLS \
--group-modules=tree \
--directory-based \
--iml-in-project-root \
--stat-dir ~/.ya/build-stat \
--stat \
--yt-store -r $PROJECTS_PATH/$PROJECT_NAME -l \
ciface-promo \
ciface-promo-common \
ciface-promo-core \
ciface-promo-db
```

4) Открыть проект в IDEA (открыть папку, указанную в `$PROJECTS_PATH/$PROJECT_NAME`)
5) Запустить `PromoInterfaceApplicationLauncher` (кнопочка запуска прямо в файле `PromoInterfaceApplicationLauncher.java` у `public static void main`)

Теперь можно потыкать в сваггер (http://localhost:8080/swagger-ui.html) или получить определение контракта для фронта (http://localhost:8080/v1/definitions.ts)

На базу изменения накатываются в `MigrationManager`.
Чтобы увидеть логи в консоли нужно добавить `-Dlog4j.configurationFile=<путь к log4j2-test.xml>`

### Чтобы запустить с тестовой базой
- Добавляем в VM Options  -Dspring.profiles.active=testing
В properties.d/testing/00-ciface-promo.properties добавляем проперти с datasource-ng
 и пропертю secret_client : $secret, значение можно найти на машинке
- Если вылетает ошибка про ticket_parser2, то можно следовать инструкции
(https://wiki.yandex-team.ru/users/mors741/tvm-ticketparser2java-lib-from-sources/)

### Полезные ссылки

#### Балансер
[тестинг](https://marketpromo-ciface-promo.tst.vs.market.yandex.net/swagger-ui.html#/)

[прод](https://marketpromo-ciface-promo.vs.market.yandex.net/swagger-ui.html#/)

#### Ссылка на ydb:
[тестинг](https://ydb.yandex-team.ru/db/ydb-ru-prestable/marketpromo/testing/cifacepromo/browser)

[прод](https://ydb.yandex-team.ru/db/ydb-ru/marketpromo/production/cifacepromo/browser)

#### И еще

[Релизный пайплайн](https://tsum.yandex-team.ru/pipe/projects/Promo/delivery-dashboard/marketpromo-ciface-promo)

[juggler-проверки](https://juggler.yandex-team.ru/aggregate_checks/?query=(host%3Dmarketpromo_ciface_promo-testing)%26)

[Nanny](https://nanny.yandex-team.ru/ui/#/services/dashboards/catalog/market_marketpromo_ciface_promo/)

#### Документация и остальное:

[В целом про бизнес задачу](https://wiki.yandex-team.ru/market/pokupka/projects/promo-actions/assortment-ki)

[В целом про техническое решение](https://wiki.yandex-team.ru/market/pokupka/projects/promo-actions/assortment-ki/dev/)

[Очередь промобекенда](https://st.yandex-team.ru/CATEGORYIFACE)

[Документация ydb](https://ydb.yandex-team.ru/docs/overview)

#### Интерфейс промо-ки:

Чтобы заработало нужно поставить куку promos = 1 (в консоли браузера `document.cookie = "promos=1";`)

[прод](https://cm.market.yandex-team.ru/#/promos)

[тестинг](https://cm-testing.market.yandex-team.ru/#/promos)
