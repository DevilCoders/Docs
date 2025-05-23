# Доставка секретных данных

##  Что это? {#intro}
Механизм передачи инстансам сервиса данных, доступ к которым ограничен.

##  Пререквизиты для работы секретов {#prerequisites}
Для [Секретницы](https://yav.yandex-team.ru) сетевой доступ от инстанса до `tvm-api.yandex.net` и `vault-api.passport.yandex.net` (он по умолчанию есть у всех сетевых макросов, отнаследованных от `_SEARCHPRODNETS_`).

##  Общая схема работы {#how-does-it-work}
1. Секрет сохраняется в хранилище - [Секретницу](https://yav.yandex-team.ru/) или [NannyVault](https://wiki.yandex-team.ru/jandekspoisk/sepe/vault/).
1. При настройке сервиса через Instance Spec указать хранилище секретов как источник переменных окружения или вольюмов инстанса (см. ниже).
1. На конечном хосте InstanceCtl перед запуском инстанса:

* Получает спецификацию инстанса;
* Авторизуется в хранилище секретов и получает содержимое секрета;
* При запуске секции, указанной в спецификации инстанса, передаёт ей содержимое секрета в переменной окружения или создаёт файл.
* InstanceCtl не будет стартовать секцию инстанса до тех пор, пока не сможет получить содержимое секрета.

###  Передача секрета в инстансы сервиса {#spec-for-delivery}
####  Передача секрета в переменной окружения {#deliver-as-env-var}
Чтобы принести секрет в инстансы сервиса в виде переменной окружения, нужно отредактировать их спецификацию:
![instance_spec.png](https://jing.yandex-team.ru/files/sshipkov/instance_spec.2e6fa4e.png)
![2018-12-2518-52-23.png](https://jing.yandex-team.ru/files/sshipkov/2018-12-2518-52-23.14aa638.png)

####  Передача секрета в виде файла {#deliver-as-file}
Чтобы принести секрет в инстансы сервиса в виде файла, нужно отредактировать их спецификацию:
![2018-12-2518-51-36.png](https://jing.yandex-team.ru/files/sshipkov/2018-12-2518-51-36.bddb3a3.png)

Секрет приносится с permissions `600` из-под пользователя `loadbase`.

**Замечание.** На данный момент в Runtime Cloud далеко не все сервисы живут в chroot'ах (с изоляцией по файловой системе). И в настоящий момент все инстансы запускаются из-под `loadbase`. Поэтому если принести секреты на машину в виде файла без дополнительных телодвижений, то эти секреты будут доступны для чтения всем незаизолированным инстансам, живущим на той же машине.

**Замечание 2.** В каждом секрете можно создать несколько пар "ключ-значение". В инстансе будет создана директория с именем volume'а (поле `Volume name`), внутри которой будут помещены файлы с именами, соответствующие "ключам" внутри секрета. Их содержимое будет равно "значениям":

```
volume_name
\_ key_1  # содержит value_1
\_ key_2  # содержит value_2
```

**Замечание 3.** Переменные окружения будут доступны **только** в том подконтейнере, для которого заведены. Например, посколько juggler-агент, запускающий проверки, запускается в отдельном подконтейнере, ему не будут доступны никакие секретные переменные окружения основных секций сервиса.

###  Массовое обновление ревизии секрета в нескольких сервисах {#batch-commit-yav}

Чтобы массово обновить версию yav-секрета во всех использующих его сервисах (или их подмножестве), нужно перейти на страницу с yav-секретом и нажать кнопку коммита интересующей версии в использующие сервисы:

![img](https://jing.yandex-team.ru/files/alonger/yavsec.png)

На этой же странице можно посмотреть, в каких сервисах секрет используется.

Попасть на эту страницу можно как перейдя на общий список секретов и найдя среди них нужный:

![img](https://jing.yandex-team.ru/files/alonger/services.png)

![img](https://jing.yandex-team.ru/files/alonger/all.png)

Так и со страницы, где указываешь секрет в сервисе:

![img](https://jing.yandex-team.ru/files/alonger/from-service.png)

Также массовое обновления yav-секретов работает [https://a.yandex-team.ru/arc/trunk/arcadia/infra/nanny/secrets_updater](https://a.yandex-team.ru/arc/trunk/arcadia/infra/nanny/secrets_updater)
![img](https://jing.yandex-team.ru/files/sshipkov/screenshotfrom2019-12-1018-31-26.b6c5bfc.png)

## NannyVault {#nanny-vault}

### Создание секрета {#create}
Для создания секрета необходимо завести связку секретов, или **keychain**.

Keychain содержит:

* Несколько секретов;
* Список пользователей, которые могут изменять содержимое секретов;
* Список сервисов, инстансы которых могут иметь доступ к содержимому секретов.

Создать keychain можно сделать из [панели управления](https://nanny.yandex-team.ru/ui/#/keychains/).

![keychains.png](https://jing.yandex-team.ru/files/sshipkov/keychains.9f71c52.png)

После создания keychain'а нужно добавить в него секрет:

![img](https://jing.yandex-team.ru/files/sshipkov/addsecret.2d4c05d.png)

####  Содержимое секрета {#secret-content}
Каждый секрет представляет собой набор пар "ключ-значение", которые извлекаются из хранилища одним запросом API. При доставке секретов в виде файлов, для каждой из пар будет создан файл с названием ключа, содержимое которого будет взято из соответствующего значения.

![img](https://jing.yandex-team.ru/files/sshipkov/createsecret.fd3fce2.png)

При создании секрета будет создана первая ревизия его содержимого:

![img](https://jing.yandex-team.ru/files/sshipkov/revision1.9afcf79.png)

###  Как открыть доступ сервиса к секрету {#service-access}
Для того, чтобы сервис мог получить доступ к секрету, необходимо указать его в списке разрешенных сервисов в интерфейсе keychain'а. Для этого нужно отредактировать метаинформацию keychain'а:

![img](https://jing.yandex-team.ru/files/sshipkov/editkeychain.9ce531a.png)

#####  Зачем это нужно? {#why-service-access}
Представим гипотетическую ситуацию:

1. Пользователь А завёл секрет, который должен быть использован в сервисе `good_service`;
1. Пользователь B хочет увести секрет пользователя А. Для этого он приносит секрет в инстансы своего сервиса `malicious_service`, которые пришлют содержимое секрета ему на email.
Для того, чтобы избежать такой ситуации, мы ограничиваем множество сервисов, которые могут использовать секрет, списком, указанным в keychain'е секрета.

###  Изменение секрета {#edit-secret}
Ревизии секретов неизменяемы. Чтобы обновить секрет в сервисе, нужно завести новую ревизию секрета:

![add-revision.png](https://jing.yandex-team.ru/files/sshipkov/add-revision.56ae0ac.png)

После этого новую ревизию секрета нужно указать в спецификации инстансов сервисов, которые должны на неё переехать. Если сервисов несколько, это можно сделать в батч-режиме.

###  Массовое обновление ревизии секрета в нескольких сервисах {#batch-commit}
Работает по кнопке в строке ревизии секрета:

![batch-commit.png](https://jing.yandex-team.ru/files/sshipkov/Screenshot%20from%202019-12-10%2018-31-26.b6c5bfc.png)

В диалоге нужно выбрать список сервисов, в которых хочется обновить ревизию секрета, из числа указанных в keychain'е. После этого в каждом из выбранных сервисов будет обновлена спецификация инстансов. Будут обновлены все секретные переменные окружения и секретные volume'ы, в которых указана другая ревизия того же секрета из того же keychain'а.

##  Другие способы передачи секрета приложению {#other-ways}
InstanceCtl не умеет передавать содержимое секрета в параметрах запуска для того, чтобы пользователь случайно не скомпрометировал себя открыв доступ к содержимому секрета через вызов `ps`. Однако, если пользователь всё равно хочет использовать такой небезопасный механизм, он может запускать свое приложение `application` командой вида `sh -c 'exec ./application $SECRET_CONTENT'`, где `SECRET_CONTENT` -- имя описанной в спецификации инстанса переменной окружения. Пример соответствующего конфига:

```
[test_section]
binary = /bin/sh
arguments = -c 'exec ./application $SECRET_CONTENT'
```
##  Доставка секрета {#delivery}
После указания секрета в спецификации инстансов необходимо сгенерировать и выкатить новую конфигурацию сервиса.

