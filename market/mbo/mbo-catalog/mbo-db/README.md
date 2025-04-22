## Оглавление
- [Что такое liquibase](#what-is-liquibase)
- [Иерархия скриптов](#hierarchia)
- [Общие принципы changeset-ов](#main-principles)
- [Как накатывать изменения вручную](#manual-update)
- [Как liquibase используется в функциональных/интеграционных тестах](#usage-in-tests)
- [Как у нас автоматически накатываются изменения](#automatic-updates)
- [Изменения в clickhouse для аудита в МТ](#mt-clickhouse-audit)
- [Обработка ошибок](#error-handling)
- [Проблемы и решения](#problems-and-solutions)
- [Релиз в artifactory](#release-to-artifactory)
- [Интересные ссылки](#links)

_Дисклеймер  
Инструкция нагло воровалось у [баланса](https://wiki.yandex-team.ru/Balance/liquibase/) и [mbi](https://wiki.yandex-team.ru/mbi/development/liquibase/) :)_

## <a name="what-is-liquibase"></a> Что такое liquibase
[Liquibase](http://www.liquibase.org/) - это система контроля версий для структуры базы. Она применяет к базе файлы с изменениями, организованные в виде набора атомарных изменений - changeset-ов. Набор changeset-ов объединяется в файлы - changelog-и. В нашем случае [changelog-и в формате sql](http://www.liquibase.org/documentation/sql_format.html).

Каждый changelog состоит из [changeset-ов](http://www.liquibase.org/documentation/changeset.html):
* Каждый changeset выполняется в отдельной транзакции (что не затрагивает DDL-операции). Можно отключить флагом **runInTransaction:false**
* Для changeset-а можно написать процедуру отката, и тогда при помощи liquibase можно будет откатить изменения
* Changeset можно отметить тегом и выполнять откат до тега
* Единожды применённый changeset больше не применяется, кроме случаев, когда для него выставлены флаги **runAlways** или **runOnChange** (Использовать их нужно очень аккуратно)
* Changeset-ы накатываются последовательно, как они записаны в корневом файле changelog. **Предупреждение**, мы не используем опцию [includeAll](http://www.liquibase.org/documentation/includeall.html).

## <a name="hierarchia"></a> Иерархия скриптов

Для каждой схемы БД у нас есть корневой changelog.xml, который использует liquibase. В нём есть include для остальных changelog-ов. Корневые changelog.xml лежат в `src/liquibase/resources/mbo-db/` и имеют названия `<schema_name>.changelog.xml` (Например, `market_content.changelog.xml`).

Все корневые changesets находятся в `src/liquibase/resources/mbo-db/`. В `src/sql/` в подпапках с названиями схем располагаются скрипты относящиеся только к этой схеме.  
![image](https://jing.yandex-team.ru/files/s-ermakov/README.md_-_mbo_-_Repositoriesmbo4_2017-09-20_14-45-04.png)


## <a name="main-principles"></a> Общие принципы changeset-ов

### Как писать скрипт файл
Каждый sql файл в директории БД должен удовлетворять формату.

В начале каждого файла должен быть заголовок. Если такого заголовка не будет, то весь файл будет воспринят liquibase как файл c одним большим changeset, что в свою очередь повлечет неожиданные спецэффекты. Поэтому в плагине отслеживается наличие заголовков во всех файлах. В sql-файле может быть описано несколько changeset-ов, в том числе ни одного.

```sql
--liquibase formatted sql
```

**Важно** Дальше идет область, со скриптами, которые никогда не будут применены. Сюда мы перемещам скрипты, которые уже были применены на базу.  
**Важно** мы не оставляем эту зону пустой, а обязательно заполняем данными.  
**Новое** Теперь мы оборачиваем такой блок в ченджсет с контекстом **context:tests_only**

```sql
--changeset username:MBO-66666_add_liquibase_script context:tests_only
begin
  DBMS_OUTPUT.put_line ('Never run');
end;
```

Дальше идет зона со скриптами.

```sql
--changeset username:MBO-66666_add_liquibase_test_table
CREATE TABLE BO.LIQUIBASE_TEST_TABLE(a integer);

--changeset username:MBO-66666_insert_test_values
-- если вы хотите писать свои комментарии, то они должны идти после объявления ченджсета
INSERT INTO BO.LIQUIBASE_TEST_TABLE(a) VALUES(1);
INSERT INTO BO.LIQUIBASE_TEST_TABLE(a) VALUES(2);
```

<details> 
  <summary>Разбор SQL файла</summary><p>
  
1. `username:MBO-66666` - id changeset, представляет из себя ваш ник и тикет. При необходимости допускается использовать `username:MBO-66666-2`, `username:MBO-66666-SOME-cool-script` и тому подобное.
2. `CREATE TABLE BO.LIQUIBASE_TEST_TABLE(a integer)` - собственно содержимое changeset-а.
</p></details> 

Так же можно писать PL/SQL скрипты.

```sql
--changeset username:MBO-66666_test_pl_sql stripComments:false endDelimiter:\\
declare
 p_result number;
begin
  SELECT /*+ PARALLEL(4) */ count(*)
    INTO p_result
    FROM BO.LIQUIBASE_TEST_TABLE;
  DBMS_OUTPUT.put_line ('DEBUG count=' || p_result);
end;
\\
```
<details> 
  <summary>Разбор PL/SQL скрипта</summary><p>
  
1. `username:MBO-66666` - id changeset, представляет из себя ваш ник и тикет. При необходимости допускается использовать `username:MBO-66666-2`, `username:MBO-66666-SOME-cool-script` и тому подобное.
2. `stripComments:false` - аттрибут, необходимый для сохранения комментариев в sql, включая модификаторы как `/*+ PARALLEL(4) */`
3. `endDelimiter:\\` - аттрибут, по которому liquibase разделяет changeset на statement'ы. Мы используем `\\` - это проверенный рабочий вариант. Если `endDelimiter` не указан, то используется `;`. Если один statement (например, pl/sql блок) содержит в себе `;` - нужно обязательно указывать свой endDelimiter.
   [Подробнее про endDelimiter у mbi](https://wiki.yandex-team.ru/mbi/development/liquibase/enddelimiter/)
5. `\\` - завершение changeset-а.
6. **Важно** после добавления нового файла нужно внести его имя в соответствующий chagelog.xml **Иначе он не сработает**

**Важно** отметить, что если вы используете модификаторы аля `/*+ PARALLEL(4) */`, то использовать `endDelimiter:/` категорически запрещено. MBI предлагает использовать `//`, `///` и тому подобное.
[Схема включения скриптов у MBI](https://wiki.yandex-team.ru/mbi/development/liquibase/sxema-vkljuchenija-skriptov-lqb/)
</p></details> 

<details> 
  <summary>ИТОГОВЫЙ СКРИПТ</summary><p>
  
```sql
--liquibase formatted sql

--changeset username:MBO-66666_add_liquibase_script context:tests_onl
begin
  DBMS_OUTPUT.put_line ('Never run');
end;

--changeset username:MBO-66666_add_liquibase_test_table
CREATE TABLE BO.LIQUIBASE_TEST_TABLE(a integer);

--changeset username:MBO-66666_insert_test_values
-- если вы хотите писать свои комментарии, то они должны идти после объявления ченджсета
INSERT INTO BO.LIQUIBASE_TEST_TABLE(a) VALUES(1);
INSERT INTO BO.LIQUIBASE_TEST_TABLE(a) VALUES(2);

--changeset username:MBO-66666_test_pl_sql stripComments:false endDelimiter:\\
declare
 p_result number;
begin
  SELECT /*+ PARALLEL(4) */ count(*)
    INTO p_result
    FROM BO.LIQUIBASE_TEST_TABLE;
  DBMS_OUTPUT.put_line ('DEBUG count=' || p_result);
end;
\\
```
</p></details>

### Каким образом создавать файлы со скриптами
Создаем файл: `<object>.sql`. В каждом таком файле производятся все действия с объект.
Объект - это какая-то самостоятельная сущность в БД (таблица, вьюха, последовательность и так далее).

#### Если вы создаете файл с уже существующим объектом
1. **Важно** первым делом добавляете после заголовка DDL для создания таблицы. Если таблица существует в базе, то код создания можно взять из SQLDeveloper. Далее из других мест **переносите (или удаляете)** абсолютно все скрипты, связанные в вашей таблицей. Этот блок скриптов оборачивается в changeset с **context:tests_only**.
2. Добавляете свои скрипты
3. Не забудьте добавить включение файла в корневой changelog.xml, если это не было сделано ранее
 
<details> 
  <summary>Пример changelog.xml</summary><p>
  
```xml
<?xml version="1.0" encoding="UTF-8"?>

<databaseChangeLog
  xmlns="http://www.liquibase.org/xml/ns/dbchangelog/1.9"
  xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="http://www.liquibase.org/xml/ns/dbchangelog/1.9
         http://www.liquibase.org/xml/ns/dbchangelog/dbchangelog-1.9.xsd">

    <include file="name.sql" relativeToChangelogFile="true" />
    <include file="name1.sql" relativeToChangelogFile="true" />
    <include file="name2.sql" relativeToChangelogFile="true" />
    <include file="name3.sql" relativeToChangelogFile="true" />
</databaseChangeLog>
```
</p></details>

#### Если добавляете совершенно новый объект
1. Все тоже самое, что и в предыдущем блоке, только без исторического блока

### Общие принципы работы со скриптами внутри файла
1. Любые операции с данными внутри таблицы оформляются в виде отдельный changeset-ов в этом файле.
2. Если вам нужны constraint, sequence, index и подобное, то стоит создание каждой сущности помещать в отдельный changeset. Так стоит делать, чтобы в случае ошибочных действий, не пришлось править код.
3. **Не** указывайте `endDelimiter` без крайней на то необходимости. Предпочитается использование `;` по-умолчанию.
4. Переименование таблицы должно быть последним действием с таблицей в sql-файле. Дальнейшая жизнь происходит в файле с именем новой таблицы.

**Важно** При добавлении нового changeset-а в конце файла можно случайно поломать последнее изменение, описанное в файле (например, добавив пустую строку).

## <a name="manual-update"></a> Как накатывать изменения вручную

Скрипты запускаются из папки [mbo-db](https://a.yandex-team.ru/arcadia/market/mbo/mbo-catalog/mbo-db)

Для того, чтобы самостоятельно запускать на своей машине скрипты. Достаточно сделать следующее:
- Выполнить ```ya make``` в папке модуля mbo-db
- Изменить файл [mbo-db-params.sh](https://a.yandex-team.ru/arcadia/market/mbo/mbo-catalog/mbo-db/src/script/manual/mbo-db-params.sh):
  - Добавить путь до папки bin с JDK 8 (**JAVA8_BIN**), например, ```/Users/lexhigh/Library/Java/JavaVirtualMachines/corretto-1.8.0_332/Contents/Home/bin```
  - Добавить url базы данных scat.yandex.ru (**JDBC_URL**), посмотреть можно [тут](https://bb.yandex-team.ru/projects/MARKET_SECURE/repos/datasources-ng/browse), в файле etcd.yml в зависимости от необходимого окружения
  - Добавить логины и пароли для необходимых бд, посмотреть можно в [секретнице](https://yav.yandex-team.ru/?search=mbo-common)
- Запустить скрипт ```src/script/manual/mbo-db-common.sh```

<details> 
  <summary>Старый ручной запуск</summary><p>

Для удобства liquibase скрипты запускаются через gradle таски с помощью `mbuild-liquibase` плагина.
Подробнее про него написано здесь: https://wiki.yandex-team.ru/market/development/java/mbuild/#mbuild-liquibase

Для того, чтобы самостоятельно запускать на своей машине скрипты. Достаточно сделать 2 вещи:
- Скачать файл datasources.properties, подходящий для выбранной вами среды
- Скачать tnsnames.ora для выбранной вами среды
- Запустить:
```bash
./gradlew :mbo-db:liquibaseRun --command=update \
   -Pmbuild.liquibase.datasources=<path-to-your-datasources> \
   -Poracle.net.tns_admin=<path-to-tns-!!FOLDER!!-not-file>
```
</p></details>

## <a name="usage-in-tests"></a> Как liquibase используется в функциональных/интеграционных тестах

В настоящий момент liquibase скрипты применяются на тестовые оракловые базы для:
- проверки корректности написания скриптов миграции
- для того, чтобы создать готовую базу для функциональных и интеграционных тестов

По-умолчанию, все скрипты накатываются на тестовые базы, но если вы по каким-то причинам хотите ограничить применение, вы можете воспользоваться контекстами:
 - tests_only - для применения ченджсета только в тестах
 - prod_only - для применения ченджсета только в деве/тестинге/проде/мт

Например. 
```
-- Этот скрипт запуститься только в тестах
--changeset s-ermakov:MBO-17763_initial_changeset context:tests_only
create table CATEGORY
...
```

```
-- Этот скрипт запуститься только в деве/тестинге/проде/мт
--changeset s-ermakov:MBO-17763_initial_changeset context:prod_only
create table CATEGORY
...
```

#### Особенности оракла для тестов:
1. В функциональных тестах будут динамически выдаваться схемы, поэтому в скриптах миграции **не** надо указывать название схемы (иначе миграция произойдет не в ту схему). Также не нужно указывать tablespace по аналогичным причинам. **UPD** уже можно указывать, [подробнее](../mbo-functional-tests-oaas#faq).
2. Раньше, если таблица в  БД уже существовала, то при создании файла миграции мы просто копипастили ее объявление в файл и не оборачивали в ченджсет. Сейчас придется оборачивать и маркировать такой ченджсет контекстом "**tests_only**".

Возможно будет дописываться...

## <a name="automatic-updates"></a> Как у нас автоматически накатываются изменения

### На тестинг и прод

Изменения накатываются автоматически с помощью rpm пакетов в [релизном](https://tsum.yandex-team.ru/pipe/projects/mbo/pipelines/mbo-cd-arc/editor/24) и [хотфиксным](https://tsum.yandex-team.ru/pipe/projects/mbo/pipelines/mbo-cd-hotfix-arc-0/editor/4) пайплайнам mbo.

#### Процесс сборки

Сборка rpm пакета осуществляется с помощью ```ya package mbo-db/package.json```, подробнее можно почитать [тут](https://wiki.yandex-team.ru/users/lexhigh/db/kak-my-pereezzhali-iz-gradle-tier1-i-teamcity-v-arcadia-tier0-i-sandbox/#vbtprode1)

<details>
   <summary>Раньше было так</summary>
   
   Сборкой rpm занимается mbuild-liquibase-rpm: https://wiki.yandex-team.ru/market/development/java/mbuild/#mbuild-liquibase-rpm  
   Выкладкой rpm занимается кондуктор: https://c.yandex-team.ru/packages/yandex-mbo-db
   
   #### Процесс сборки
   
   Сборка rpm пакета начинается с команды debuild. На самом деле это костыль, мы используем debian, чтобы удобно хранить ченджлоги, и чтобы собрать пакет (debuild собирает debian, а debian собирает rpm, потом система сборки игнорирует debian пакет и берет только rpm). Такое решение было выбрано чтобы быстро интегрироваться в существующий пайплайн, так как другие команды уже так катаются.
   
   Непосредственно сам rpm собирается командой: `./gradlew buildLiquibaseRpm`. Подробнее об ее устройстве читать здесь: https://wiki.yandex-team.ru/market/development/java/mbuild/#mbuild-liquibase-rpm

   #### Как запускается выкладка на машинках
   
   Main скрипт: `/usr/bin/ mbo-db-common.sh`  
   Classpath для запуска находится здесь: `/usr/lib/yandex/mbo-db/`  
   А сами ченджлоги располагаются здесь: `/var/lib/yandex/mbo-db`, а если конкретно, то тут: `/var/lib/yandex/mbo-db/src/liquibase/resources/mbo-db/site_catalog.changelog.xml`

   Если точкой входа из консоли является `./gradlew liquibaseRun ...`, то точкой входа для rpm пакета является `mbo-db-common.sh`. Это, и другие bash скрипты располагаются в `mbo-db/src/script`.  
   Аналогично `./gradlew liquibaseRun ...` mbo-db-common.sh тоже сначала валидирует данные на всех схемах и только потом производит выкладку скриптов.

__Приятный бонус:__ Если надо создать новый скрипт, то liquibase-rpm плагин умеет их создавать https://wiki.yandex-team.ru/market/development/java/mbuild/#mbuild-liquibase-rpm.
</details>

#### Как запускается выкладка на машинках

Main скрипт: `/usr/bin/ mbo-db-common.sh`  
Classpath для запуска находится здесь: `/usr/lib/yandex/mbo-db/`  
А сами ченджлоги располагаются здесь: `/var/lib/yandex/mbo-db`, а если конкретно, то тут: `/var/lib/yandex/mbo-db/src/liquibase/resources/mbo-db/site_catalog.changelog.xml`

#### Состав скриптов
 
<details> 
  <summary>Из чего состоит mbo-db-common.sh</summary><p>
  
Первым делом мы получаем пароль. Если скрипт возвращения пароля завершился неуспешно, то мы должны прервать выполнение, завершившись с кодом 0. Это правильное и запланированное поведение.
Далее получаем url подключения
И логин: sys as sysdba
```
#!/bin/bash
DB=scatnew
# get password
JDBC_PASSWORD="$(/opt/oracle/admin/py-scripts/get_pwd.py -d $DB)"
rc=$?
if [ $rc -ne 0 ] ; then echo "non-zero exit code when getting password: $rc"; exit 0; fi
if [ -z "$JDBC_PASSWORD" ] ; then echo "password is empty, exiting"; exit 122; fi

# fail on error
set -e

# get service name
SERVICE_NAME="$(/usr/bin/oshell $DB lsnrctl services | grep Service | grep 'has' | grep 'instance' | awk -F'"' '{print $2}' | grep -i "$DB"deploy)"
if [ -z "$SERVICE_NAME" ] ; then echo "empty service name, exiting"; exit 123; fi
echo "Using service $SERVICE_NAME"

# export params
export JDBC_URL="jdbc:oracle:thin:@$(hostname):1521/$SERVICE_NAME"
export JDBC_LOGIN="sys as sysdba"
export JDBC_PASSWORD
```

Этих трех параметров хватает, чтобы подключиться к БД.
Потом вызываем подскрипты по нужным схемам.
</p></details>
 
<details> 
  <summary>Из чего состоит mbo-db-run*.sh</summary><p>
  
Каждый скрипт обязан принять на вход название liquibase-activity и название команды.
Потом просто запускаем liquibase команду с правильными параметрами.

Например,
```
#!/bin/bash

LIQUIBASE_ACTIVITY=market_content

if [ -z "${LIQUIBASE_COMMAND}" ]; then
    echo "No liquibase command passed. Aborting."
    exit 1
fi

echo "Run '${LIQUIBASE_ACTIVITY}' activity with '${LIQUIBASE_COMMAND}' command"

java \
   -cp "/usr/lib/yandex/mbo-db/*:/var/lib/yandex/mbo-db" \
   -Dfile.encoding="UTF-8" \
   liquibase.integration.commandline.Main \
   --logLevel="info" \
   --defaultSchemaName="market_content" \
   --changeLogFile="src/liquibase/resources/mbo-db/market_content.changelog.xml" \
   --url="${JDBC_URL}" \
   --username="${JDBC_LOGIN}" \
   --password="${JDBC_PASSWORD}" \
   ${LIQUIBASE_COMMAND}

echo "Successfully run '${LIQUIBASE_ACTIVITY}' activity"
```
</p></details>

### На мультитестинг

На МТ изменения накатываются с помощью ЦУМ джобы [SandboxMarketLiquibaseJob](https://tsum.yandex-team.ru/pipe/jobs/ff18faba-726e-4ea8-ba7c-dc18bf5c7f67).
Подробнее можно почитать [тут](https://wiki.yandex-team.ru/users/lexhigh/db/kak-my-pereezzhali-iz-gradle-tier1-i-teamcity-v-arcadia-tier0-i-sandbox/#vmt1).

<details>
<summary>Как было раньше</summary><p>
С помощью тимсити джобы: https://teamcity.yandex-team.ru/viewType.html?buildTypeId=Market_Mbo_MboLiquibaseRun
Она вызывается из пайплайна в мультитестинг.
</p></details>

### На дев
Никак не накатываются

## <a name="mt-clickhouse-audit"></a>Изменения в clickhouse для аудита в МТ

Всё руками, см. mbo/mbo-db/main/mbo_audit.sql

## <a name="error-handling"></a> Обработка ошибок
1. Если во время выкладки на testing/prod произошла ошибка и изменения в транзакции не откатились (например, создание таблиц), то нужно сделать отдельный changeset, который будет исправлять сложившуюся ситуацию.
2. Если вы случайно испортили какой-то changeset и по нему не сходится md5-хеш, то стоит вернуть всё как было или применить команду liquibase `clearCheckSums` (http://www.liquibase.org/documentation/command_line.html).

### Если нужно исправить какое-то состояние БД
1. **Не исправляем БД руками**
2. Создаем liquibase скрипт
3. Проходим ревью
4. Или хотфиксом или обычным релизным пайплайном мержим в мастер

В крайних случаях, можно сразу накатить на среду **через liquibase** и убедиться, что тикет с исправлениями тут же едет хотфиксом.

## <a name="problems-and-solutions"></a> Проблемы и решения
Описано здесь: https://wiki.yandex-team.ru/mbi/development/liquibase/#problemyireshenija  
Или можно посмотреть здесь: https://wiki.yandex-team.ru/balance/liquibase/qanda/

## <a name="release-to-artifactory"></a> Релиз в artifactory
Если вы используете библиотеку mbo-db в аркадии, то сначала отправьте ресурс с jar в artifactory, задав новую версию -Pversion, используя текущую дату и время в названии:
```
export LATEST_VERSION=$(date +"%Y%m%d-%H%M%S")
./gradlew -Pversion=5.0-${LATEST_VERSION}.master  -Prelease.useAutomaticVersion=true --no-daemon --console plain --info --refresh-dependencies --rerun-tasks --recompile-scripts -s -b build.gradle clean :mbo-db:release
```
Затем для импорта новой версии артефакта из artifactory в **contib/java** используйте команду:
```
ya maven-import ru.yandex.market:mbo-db:5.0-${LATEST_VERSION}.master
```
Не забудьте оправить изменения в **contib/java** в **trunk**.

## <a name="links"></a> Интересные ссылки
Вот тут еще больше примеров как писать скрипты в формате sql: https://habrahabr.ru/post/251617/

## Локальный запуск интеграционных тестов
Для запуска интеграционных тестов используется команда:
```bash
ya make -ttt
```
