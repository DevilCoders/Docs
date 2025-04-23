# WMS Liquibase tasks for MSSQL

## Liquibase support

liquibase 3.7.0

## Overview
Задачи liquibase для миграции пользователей

## How to
Собрать архив и прогнать тесты
```shell
./gradlew build
```
Собрать liquibase c задачами wms 
```shell
./gradlew buildLiquibase
```
Собрать и залить liquibase как ресурс в sandbox
```shell
./gradlew publish
```

Проект содержит задачи на изменение, задачи на откат изменения и проверки (preconditions).
Задача на изменение является одновеременно задачей на откат и выполняется автоматически при запуске операции отката.

## Preconditions

Все проверки лежат в пакете ru.yandex.market.wms.liquibase.mssql.precondition

| Task        | Description | Parameters |
| -----------------------| --------| ------------ |
| AddDefaultSchemaPrecondition | Проверяет схему по умолчанию у пользователя  | username,schema |
| AddRolePrecondition | Проверяет наличие роли у пользователя  | username,role |
| AuthorizeOnDatabasePrecondition | Проверяет является ли пользователь хозяином базы данных  | databaseName,login |
| CreateDatabaseUserPrecondition | Проверяет началие пользователя в базе данных (работает на текущей базе данных)  | username |
| CreateLoginPrecondition | Проверяет началие логина для сервера  | login |
| GrantPermissionsOnDatabasePrecondition | Проверяет права на базу данных у пользователя (работает на текущей базе данных) | username, premissions[] |
| GrantPermissionsOnObjectPrecondition | Проверяет права на объект базы данных у пользователя (работает на текущей базе данных)  | username,schema, objectName, premissions[] |
| GrantPermissionsOnSchemaPrecondition | Проверяет права на схему у пользователя (работает на текущей базе данных)  | username,schema, premissions[] |


## Chagne

Все задачи лежат в пакете ru.yandex.market.wms.liquibase.mssql.change

| Task        | Description | Parameters |
| -----------------------| --------| ------------ |
| AddDefaultSchemaPrecondition | Добавляет схему по умолчанию у пользователя  | username, schema |
| AddRolePrecondition | Добавляет роль у пользователя  | username, role |
| AuthorizeOnDatabasePrecondition | Делает пользователя хозяином базы данных | databaseName, login |
| CreateDatabaseUserPrecondition | Создает пользователя в базе данных (работает на текущей базе данных)  | username |
| CreateLoginPrecondition | Создает логина для сервера  | login |
| GrantPermissionsOnDatabasePrecondition | Добавляет права на базу данных для пользователя (работает на текущей базе данных) | username, premissions[], bool withGrantOption |
| GrantPermissionsOnObjectPrecondition | Добавляет права на объект базы данных для пользователя (работает на текущей базе данных)  | username, schema, objectName, premissions[], bool withGrantOption |
| GrantPermissionsOnSchemaPrecondition | Добавялет права на схему для пользователя (работает на текущей базе данных)  | username, schema, premissions[], bool withGrantOption |

## Example 

```xml
 <databaseChangeLog
        xmlns="http://www.liquibase.org/xml/ns/dbchangelog"
        xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
        xsi:schemaLocation="http://www.liquibase.org/xml/ns/dbchangelog
            http://www.liquibase.org/xml/ns/dbchangelog/dbchangelog-3.7.xsd">

    <changeSet author="afomichev" id="1">
        <preConditions onFail="MARK_RAN">
            <customPrecondition
                    className="ru.yandex.market.wms.liquibase.mssql.precondition.CreateDatabaseUserPrecondition">
                <param name="username" value="test-user"/>
            </customPrecondition>
        </preConditions>
        <customChange class="ru.yandex.market.wms.liquibase.mssql.change.CreateDatabaseUserChange">
            <param name="login" value="test-login"/>
            <param name="username" value="test-user"/>
        </customChange>
    </changeSet>
</databaseChangeLog>
```