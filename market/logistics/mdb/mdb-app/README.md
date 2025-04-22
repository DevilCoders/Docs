# Market Delivery Bus (MDB)

## Где живут параметры конфигураций
Значения для плейсхолдеров в конфигурациях стоит искать в папке ```mdb-app/src/main/properties.d/<environment>```

Ее содержимое становится доступно в контексте приложения через
[AppPropertyScanner](https://a.yandex-team.ru/arc/trunk/arcadia/market/infra/java-application/core/src/main/java/ru/yandex/market/application/properties/AppPropertyScanner.java)

**Локальные настройки (dev)** находятся в файле src/main/properties.d/local/application-local.properties.dist, который нужно
_скопировать_ в application-local.properties, рядом. Копию можно редактировать по своему желанию, не добавляя в репозиторий.

_Новые настройки конфигураций (помимо yav) нужно не забывать добавлять в dist._

## Локальный запуск

### Общее

MDB запускается обычным стартом psvm в классе MdbApplication.
Перед этим необходимо убедиться, что все проперти, описанные выше, установлены.

Параметры запуска в Идее должны быть следующими:
- **VM Options:** ``-Djava.library.path=/usr/local/lib`` (для TVM, см. ниже)
- **Environment variables:** ``PROPERTIES_DIR=/path_to_your_arcadia_or_svn_repo/market/logistics/mdb/mdb-app/src/main/properties.d``
- **Active profiles**: ``local``

Проверка, что приложение запустилось - GET-запрос к http://localhost:15051/ping

### Зависимости

####Развертка локальной бд (dev)

**NB:** Если вы пользуетесь Арком, папка должна быть смонтирована с параметром --allow-other, иначе ни docker ни liquibase не стартуют

Запустить контейнер с локальной бд (будет создана без миграций)
```
docker-compose up -d -f mdb-app/dependency-stubs/docker-compose.yml
```

Миграции накатятся автоматически при запуске приложения

## Тесты

### Запуск
Интеграционные тесты (LARGE-тесты) не стартуют автоматически в покомитных проверках, поэтому лучше перед пушем
прогонять их локально.
Также, flaky тесты ищутся CI ночными прогонами, и автомьютятся. Такие тесты недопустимы к контрибьюту, их нужно
отлавливать перед коммитом.

Для запуска инт-тестов необходим Docker.

```bash
ya make -ttt --retest --tests-retries=2 --test-debug --yt-store
```

* -ttt (запустить SMALL, MEDIUM, LARGE тесты)
* --retest (Выключить кеш тестов)
* --tests-retries=2 (проверка на FLAKY тесты, лучше даже 3)
* --test-debug (более детальный вывод тестов)
* --yt-store (подтягивать бинарные зависимости из YT)

Пример нестабильных тестов:

**@ParameterizedTest со стандартным displayName**

Встроенный форматтер будет генерировать для лямб аргументов разные имена для повторных прогонов. Мерджер будет считать их разными
и помечать как flaky.

Рекомендуется убрать из шаблона displayName нестабильные аргументы теста, нп
```java
// STABLE_PARAMETRIZED_DISPLAY_NAME = " " + DISPLAY_NAME_PLACEHOLDER + " [" + INDEX_PLACEHOLDER + "]";
@ParameterizedTest(name = STABLE_PARAMETRIZED_DISPLAY_NAME)
``` 

Либо одним из аргументов передавать описание кейса, и выводить только его, нп
```java
// ru.yandex.market.delivery.mdbapp.AbstractContextualTest.TUPLE_PARAMETRIZED_DISPLAY_NAME
// {0} - первый аргумент из сорса
// TUPLE_PARAMETERIZED_DISPLAY_NAME = " " + DISPLAY_NAME_PLACEHOLDER + " [" + INDEX_PLACEHOLDER + "] {0}";
```

Если вам нужно запустить один тест, этого можно добиться ключом -F:
```bash
ya make -tttF'*OrderCreateTest*'
```
