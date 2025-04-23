# Logistics order management service (LOM)

## Где живут параметры конфигураций
Значения для плейсхолдеров в конфигурациях стоит искать в папке ```lom-app/src/main/properties.d/<environment>``` 

Ее содержимое становится доступно в контексте приложения через
[AppPropertyScanner](https://a.yandex-team.ru/arc/trunk/arcadia/market/infra/java-application/core/src/main/java/ru/yandex/market/application/properties/AppPropertyScanner.java)

Секреты приложения (пароли от баз и тп) и хосты для зависимостей (по окружениям) живут в [yav](https://yav.yandex-team.ru)
с тегом "lom"

[Пример секрета для тестинга](https://yav.yandex-team.ru/secret/sec-01d71tfdp47frp9vd4x3xs2b2f/explore/versions)

**Локальные настройки (dev)** находятся в файле src/main/properties.d/local/application-local.properties.dist, который нужно
_скопировать_ в application-local.properties, рядом. Копию можно реадктировать по своему желанию, не добавляя в репозиторий.

_Новые настройки конфигураций (помимо yav) нужно не забывать добавлять в dist._

## Локальный запуск

### Общее

LOM запускается обычным стартом psvm в классе LogisticsLom. 
Перед этим необходимо убедиться, что все проперти, описанные выше, установлены.

Параметры запуска в Идее должны быть следующими:
- **VM Options:** ``-Djava.library.path=/usr/local/lib`` (для TVM, см. ниже)
- **Environment variables:** ``PROPERTIES_DIR=/path_to_your_arcadia_or_svn_repo/market/logistics/lom/lom-app/src/main/properties.d`` 
- **Active profiles**: ``local``

### Зависимости

####Развертка локальной бд (dev)

**NB:** Если вы пользуетесь Арком, папка должна быть смонтирована с параметром --allow-other, иначе ни docker ни liquibase не стартуют

Запустить контейнер с локальной бд (будет создана без миграций)
```
docker-compose up -d -f lom-app/dependency-stubs/docker-compose.yml
```

Миграции накатятся автоматически при запуске приложения

#### Настройка БД в Idea
Пререквизитом является наличие роли "разработчик" в сервисе https://abc.yandex-team.ru/services/lom/

Пойти в yav.yandex-team.ru
Найти секреты ЛОМ-а для нужного окружения (нп market-delivery-lom-testing)
Запомнить значения spring.datasource.username, spring.datasource.password внутри lom-secrets.properties

jdbc-url взять из properties.d соотв. окружения

Создаем в IDEA новый датасурс, вписываем в URL jdbc: урл целиком.
Никаких тунелей не нужно, базы доступны из дев сети.

##### The hostname localhost could not be verified by hostnameverifier PgjdbcHostnameVerifier
Выставить опции драйвера pg:
```
sslmode=verify-ca
sslfactory=org.postgresql.ssl.NonValidatingFactory
```

#### TVM
Настраивается аналогично LGW, если у вас уже есть эта библиотека, достаточно прописать параметр запуска.
Используется TVM-библиотека tvmauth. 

Для параметров ``lom.tvm.id`` и ``lom.tvm.secret`` данные можно взять от тестовой среды. 

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
// ru.yandex.market.logistics.lom.AbstractContextualTest.TUPLE_PARAMETRIZED_DISPLAY_NAME
// {0} - первый аргумент из сорса
// TUPLE_PARAMETRIZED_DISPLAY_NAME = " " + DISPLAY_NAME_PLACEHOLDER + " [" + INDEX_PLACEHOLDER + "] {0}";
```

Если вам нужно запустить один тест, этого можно добиться ключом -F:
```bash
ya make -tttF'*OrderCreateTest*'
```

Чтобы запустить тесты YDB в IntellijIdea, нужно запустить Docker и авторизоваться в ```docker registry```.
[Инструкция по авторизации](https://wiki.yandex-team.ru/docker-registry/#authorization)

## Отладка MarketId по GRPC
(за основу взята [инструкция MBI](https://a.yandex-team.ru/arc/trunk/arcadia/market/mbi/marketId#как-сделать-запрос-к-grpc-ручкам))

1. для mac можно установить GRPC CLI через homebrew (brew install grpc). далее шаги для этой утилиты
2. скачать корневой сертификат (если еще нет) https://crls.yandex.net/YandexInternalRootCA.crt

**листинг методов эндпоинта**

```GRPC_DEFAULT_SSL_ROOTS_FILE_PATH=<путь до>/YandexInternalRootCA.crt grpc_cli --channel_creds_type=ssl ls marketid.tst.vs.market.yandex.net:8443 ru.yandex.market.id.MarketIdService```

**получение данных по market_id**

```GRPC_DEFAULT_SSL_ROOTS_FILE_PATH=<путь до>/YandexInternalRootCA.crt  grpc_cli --channel_creds_type=ssl call marketid.vs.market.yandex.net:8443 ru.yandex.market.id.MarketIdService.getById --json-input --json-output '{"marketId": 2000004}'```

адреса балансеров:
 - прод marketid.vs.market.yandex.net:8443
 - тест marketid.vs.tst.market.yandex.net:8443
