Общее описание
================

Этушка — это внутренняя Ярушка.
Раньше xscript-фронтенд ходил в бэкенд-CORBA-серванты на питоне и плюсах,
а контент хранился в бульке.
Сейчас xscript-фронтенд ходит в django-бэкенд по http, а контент хранится в mysql.
О старых временах напоминают только странные модули и классы в коде
и повсеместный xml (от него кажется можно избавиться только выкинув xscript).

Этушка синхронизирует сотрудников со стаффа, создает тикеты в стартреке
и ходит во внутренний поиск за рассылками.

По сети Этушка доступна
  * [@allstaff@](https://puncher.yandex-team.ru/?id=5978641bd5626ddbc11a1f4a)
  * [вики-группе atushkadostup](https://puncher.yandex-team.ru/?id=5978935ed5626ddbc11a2078)
  * [сотрудникам Яндекс.Денег](https://puncher.yandex-team.ru/?id=5ab79f67d5626d21688c6fb5)

На уровне приложения
[доступы есть](https://github.yandex-team.ru/tools/atushka-backend/blob/a4ca94b30b6d7dd223fd9901ff0ea9463847a229/at/common/ServiceAccess.py#L45)
у сотрудников yandex, yandex_money, группы atushka_dostup, и наших роботов.

Техническое описание
=====
Для работы с проектом нужно установить [Docker](https://docs.docker.com/docker-for-mac/install/)

Разработка
----------
Для сборки docker-образа:

    docker build -t mytag .

Тесты
-----
Команда для запуска тестов:

    docker-compose up


В пуллреквестах тесты [запускаются на тимсити](https://teamcity.yandex-team.ru/project.html?projectId=Tools_Applications_AtushkaBack&tab=projectOverview).

Сборка и деплой
------
Чтобы выкатить изменения из текущей ветки на тестинг:

    ya tool releaser stand -s at-back-testing

Чтобы выкатить изменения в прод:

    ya tool releaser release -e tools_at-back_production

Команде разработки сервиса
[выданы доступы](https://idm.yandex-team.ru/system/docker#role=917912)
на docker-образ `tools/at-back`.

Сети и дырки
----

Хосты в Deploy:
- [Production](https://deploy.yandex-team.ru/stages/tools_at-back_production)
- [Testing](https://deploy.yandex-team.ru/stages/at-back-testing)

Балансеры
- [Production](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/at-back-production.tools.yandex-team.ru/show)
- [Testing](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/at-back-testing.tools.yandex-team.ru/show/)


Продакшн `_AT_PROD_NETS_`
  * blackbox.yandex-team.ru 80
  * oauth.yandex-team.ru 443
  * staff-api.yandex-team.ru 443
  * st-api.yandex-team.ru 443
  * wf.yandex-team.ru 443
  * vs-mysqltools.http.yandex.net 43307
  * vs-mysqltools.http.yandex.net 43306
  * cs-mongotools02d.yandex.ru 27025
  * cs-mongotools02e.yandex.ru 27025
  * cs-mongotools02g.yandex.ru 27025
  * vs-logstash.yandex.net UDP 5544
  * avatars.yandex-team.ru 443
  * avatars-int.yandex-team.ru 12000
  * resize.yandex-team.ru 443
  * reqwizard.yandex.net 8891
  * search-back.yandex-team.ru 443

Тестинг `_AT_TEST_NETS_`
  * blackbox.yandex-team.ru 80
  * oauth.yandex-team.ru 443
  * staff-api.test.yandex-team.ru 443
  * st-api.test.yandex-team.ru 443
  * wf.test.yandex-team.ru 443
  * vs-mysqltools-testing.http.yandex.net 43307 (testing)
  * vs-mysqltools-testing.http.yandex.net 43306 (testing)
  * vs-atmysql01e.tools.os.yandex.ru 3306 (unstable)
  * cs-mongotools02dt.yandex.ru:27025 (testing)
  * cs-mongotools02et.yandex.ru:27025 (testing)
  * vs-atmongo01e.tools.os.yandex.ru:27017 (unstable)
  * vs-atmongo01e.tools.os.yandex.ru:27018 (unstable)
  * vs-logstash-testing.yandex.net UDP 5544
  * search-back.test.yandex-team.ru 80
  * avatars.pd.yandex.net 443
  * avatars-int.pd.yandex.net 12000
  * resize.yandex-team.ru 443
  * hamzard.yandex.net 8891
  * search-back.test.yandex-team.ru 443

Базы
----
Кластеры:
- MySQL
  - [Production](https://yc.yandex-team.ru/folders/footr3p3lfuushmrufps/managed-mysql/cluster/mdbtljsacga3mch8g9ar?section=overview)
  - [Testing](https://yc.yandex-team.ru/folders/footr3p3lfuushmrufps/managed-mysql/cluster/mdb9sno3qck08kidkbtm?section=overview)
- MongoDB
  - [Production](https://yc.yandex-team.ru/folders/footr3p3lfuushmrufps/managed-mongodb/cluster/432b1acb-27a8-4b25-a7c8-0bb42e898856?section=overview)
  - [Testing](https://yc.yandex-team.ru/folders/footr3p3lfuushmrufps/managed-mongodb/cluster/mdbr2k6m053q50kre0tv?section=overview)

Секреты
-------
- [Production](https://yav.yandex-team.ru/secret/sec-01e5a2mwg9sttab64wnhe0ybpg/explore/versions)
- [Testing](https://yav.yandex-team.ru/secret/sec-01e5a2fmkh812r2qgax8cwvgzr/explore/versions)

Пароль робота robot-atushka@ возможно знает ljql@
Вписать сюда https://wiki.yandex-team.ru/KirillSibirev/will/secrets-at/

База данных
-----------
```
apt-get update > /dev/null &&  apt-get install mysql-client
at dbshell
```

