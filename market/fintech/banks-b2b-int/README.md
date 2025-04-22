## Локальный запуск
1) Запускаем pg в докере
```bash
mkdir -p $HOME/docker/volumes/postgres/banks-b2b-int
docker run --rm --name pg-banks-b2b-int-docker -e POSTGRES_PASSWORD=banks-b2b-int -e POSTGRES_USER=banks-b2b-int -d -p 5432:5432 -v $HOME/docker/volumes/postgres/banks-b2b-int:/var/lib/postgresql/data/ postgres
```
2) В VM options добавить:
```text
-Dspring.profiles.active=local,development
-Dconfigs.path=<arcadia_path>/market/fintech/banks-b2b-int/src/main/properties.d
```

3) Запуск команд:
```bash
telnet localhost <tms.port> # подключение к tms-консоли, 12346 дефолтный порт
tms-list # список команд
tms-run <command name> # запуск команды
```
4) Локальные конфиги.
Находятся в ```properties.d/local```. Если хочется локально запустить приложение с токенами/ключами, которые не хочется палить, там же можно создать ```99_local.properties``` - файл находится в ```.arcignore```

### Liquibase
P.S. В любой непонтной ситуации, проверяй, поднят ли докер
####- Создание скриптов
1) Создаем файл в директории ```src/liquibase/new```, для DDL запросов имя фала = имя таблицы (просьба все новые скрипты и альтеринг существующих таблиц создавать там, /liquibase оставим для сломанных legacy:))
2) Добавляем запись в ```new/changelog.xml```
3) Файл начинаем со строки ```--liquibase formatted sql```, чтобы чейнджсеты корректно парсились таблицу
4) каждую команду в файле предваряем записью формата
```--changeset <author>:<ticket>:<changeset name that describes change>```
####- Не запускается приложение, т.к. нет схемы
 Подключаемся к базе и создаем схемку руками
####- Не запускается приложение, т.к. не скходятся контролные суммы
1) Деликатный способ: удалаем из databasechangelog проблемные записи и накатываем заново
2) Радикальный способ: сносим databasechangelog (а с ней возможно и всю базу) и накатываем всё заново
####- Не работают локально тесты т.к. не существует чейнджлога
1) удаляем директорию со сборкой тестов ```<путь к локальному проекту>/out/test```
2) ``` Build -> Rebuild Project```

### Джобы
```text
banksint.job - пакет с джобами
banksint.config.job - пакет с конфигами джоб
```
Джобы создаем, наследуя от AbstractJob и реализуя doJob()
Делаем конфиг и создаем бин с ```@CronTrigger```

#### Отключение джоб: через common_propery, см. ```AbstractJob#getEnabledPropertyName```

*Примечание: при отправке мониторингов в Juggler, название класса конвертируется из camelCase в snake_case. Парсер ищет комбинацию <строчная/цифра><Заглавная>, поэтому названия вида myABCJob и my42CaseJob запарсятся некорретно (my_abcjob и my42_case_job), просьба в таких случаях:*
1. *писать аббревиатуры как обычные слова (Yt вместо YT)*
2. *или переопределять getJugglerServiceName() явно*
3. *улучшения в StingUtils#camelToSnake приветствуются :)*
