## Статус

Занесена в Аркадию в Tier1 (аркадийная сборка и CI не поддерживаются)

## Словарь проекта

*Namespace* &mdash; проект, сервис.

*Environment* &mdash; множество машин. Например, testing, production, stress.

*Grant* &mdash; грант для множества операций.

*Action* &mdash; грант для конкретной операции

## Как сделать окружение для работы

1.  `./Utils init`
2.  `. env/bin/activate`
3.  [Настраиваем сеттинги](https://a.yandex-team.ru/arc/trunk/arcadia/passport/backend/grants_configurator/README.md#kak-nastroitь-settingi)
4.  [Настраиваем базу данных](https://a.yandex-team.ru/arc/trunk/arcadia/passport/backend/grants_configurator/README.md#kak-sozdatь-bazu-dlya-dev)
5.  [Настраиваем конфиг nginx](https://a.yandex-team.ru/arc/trunk/arcadia/passport/backend/grants_configurator/README.md#kak-sozdatь-konfig-nginx)
6.  `./manage.py syncdb --migrate`
7.  `./manage.py collectstatic`

## Как запускать dev версию из рабочей копии

```
. env/bin/activate
./manage.py runserver 0.0.0.0:<port>
```

## Как создать базу для dev

1.  Создать БД с названием `имяпроекта_имяпользователя`:
`passport_grants_configurator_%username%` на `python-dev1.passport.yandex.net`
2.  Дать на нее права пользователю `grantr_user` с паролем `grantrpass`:
```
create database passport_grants_configurator_%username%  charset utf8;
grant all on passport_grants_configurator_%username%.* to `grantr_user`@`%` identified by 'grantrpass';
```
3. Дать пользователю `grantr_user` права на создание тестовой БД:
```
grant all on test_passport_grants_configurator_%username%.* to `grantr_user`@`%` identified by 'grantrpass';
```

## Как создать конфиг nginx

1.  Взять файл за основу `configs/nginx/userdev.conf.tpl` и вместо
%username% и %port% вписать свой логин и порт, на котором будет
запускаться runserver

## Как настроить сеттинги

Создать файл `passport_grants_configurator/settings/user_%username%.py`,
положить туда конфиги для Грантушки или для приложения, провязывающегося с IDM.

## Как собрать deb-пакет

1. Любым способом собрать и закоммитить ченжлог: вручную или через [утилиту ci](https://a.yandex-team.ru/arc/trunk/arcadia/passport/backend/ci) (например, `ci release -ni -nc -nsb`)
2. Запустить `fab build` (потребуется [GPG-ключ](https://doc.yandex-team.ru/Debian/deb-pckg-guide/concepts/GPG.html))

## Как импортировать гранты из json файла

Для json файла grants.json:
```
/usr/lib/yandex/passport-grants-configurator/env/passport-grants-configurator/bin/manage.py
import_grants_list -f grants.json
```

## Как импортировать гранты из старых грантов в формате конфигурационного файла апача

1.  Выполняется из-под пользователя www-data
```
/usr/lib/yandex/passport-grants-configurator/env/passport-grants-configurator/bin/manage.py passport_import_perl_grants -f someconfig.tt -n имя_окружения -t тип_окружения
```
2.  C грантами для паспорта и копалки
```
/usr/lib/yandex/passport-grants-configurator/env/passport-grants-configurator/bin/manage.py passport_import_perl_grants --add_dev_grants --add_kopalka_grants -f someconfig.tt -n имя_окружения -t тип_окружения
```

## Как экспортировать гранты для паспорта в sql файл

```
/usr/lib/yandex/passport-grants-configurator/env/passport-grants-configurator/bin/manage.py passport_export_consumer_grants -f somefile.sql -n имя_окружения -t тип_окружения
```

## Тестовый IDM для выдачи прав

**https://idm.test.yandex-team.ru/**

1.  Используется в деве, то есть на `python-dev1.passport.yandex.net`
2.  Роли собственно Грантушки можно потестировать в системе под названием "Грантушка".
3.  Роли Паспортной админки можно потестировать в системе под названием "Паспорт, административный интерфейс".

## Провязка с IDM для Паспортной админки

1.  В [деве](http://dev.grantushka.passportdev-python.yandex-team.ru/passport_admin_roles_admin/)
и [проде](http://grantushka.yandex-team.ru/passport_admin_roles_admin/)
есть админка, в которой можно добавить новые роли (вкладка Группы,
после добавления новой роли надо связываться с idm@yandex-team.ru), выдать
новые права (вкладка Права) и присвоить их ролям (вкладка
Группы). Чтобы иметь доступ к этой админке, надо запросить роль Суперпользователь через IDM.
2.  Создавая новое право всегда выбирай Content type = pa_permission!
Name, codename имеют ограничение в 255 символов. Codename - это
короткий слаг права, name - описание права.
