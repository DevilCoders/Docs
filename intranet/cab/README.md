Общее описание
================

В [кабинете](https://cab.yandex-team.ru/) показываются данные про сотрудников, 
собранные из разных источников (ревью, голс, оебс, стартрек, вики, календарь, 
наниматор и тд).  

Кабинет не хранит у себя никаких данных и получает все из 
api сервисов в рантайме (исключение — запомненные значения в селектах таблицы 
с сотрудниками, а также актуальный курс доллара и акций YNDX с морды). 

Общий доступ к кабинету 
[выдан на @allstaff@](https://puncher.yandex-team.ru/?id=59084c300d0795b000537a14), 
но части подразделений запрещен доступ на уровне приложения переменной 
окружения `FORBIDDEN_SLUGS`.

Кабинет не имеет никакой системы прав, все проверки прав 
лежат на стороне сервисов, в которые кабинет ходит с кукой или токеном 
пользователя. Обычно сервисы отдают информацию, которая либо публична, либо
доступна сотруднику и его руководителю или hr-партнеру.

Для тестирования можно прикидываться другим сотрудником. 
Подбробности [на вики](https://wiki.yandex-team.ru/cia/revju-2.0/testing/)


Виджет «Карточка сотрудника»
----------------------------

  * Запланировано: ищем все отпуска, которые пересекаются с 
    интервалом `[сегодня; сегодня + год вперед]`. 
    Если отпуск пересекается с диапазоном частично — берем все дни отпуска 
    (кроме тех, что в прошлом).
  * Отгуляно с начала года: сумма дней отпусков, которые пересекаются 
    с интервалом `[начало этого года; сегодня]`. 
    Если отпуск пересекается с диапазоном частично — 
    берем число пересекающихся дней.
  * Последний отпуск ищем как отпуск с максимальной датой начала, 
    входящей в интервал `[сегодня - год назад; сегодня]`. 
  * котировки берем из api морды YNDX@NASDAQ и USD@ЦБРФ, проверить можно в 
    ручке `/debug/data/`.
  * Расчеты зарплат/премий/прогнозы опционов считаем с точностью, которую 
    имеем, а на фронтенд отдаем округленное до рублей для читаемости
  * Прогноз премий на год считаем так: для каждой премии, полученной 
    сотрудником за предыдущий год считаем ее долю по отношению к зарплате на 
    день получения, доли складываем и эту сумму умножаем на текущую зарплату.
    Если сотрудник работает меньше года, то посчитанную долю премий делим на 
    долю года, которую сотрудник проработал (это все сомнительные прогнозы, 
    я бы не особо на них смотрел). 
  * Годовую зарплату считаем так: `date_to = сегодня`, 
    `date_from = сегодня - 12 месяцев`. Находим ближайшее к `date_from` 
    событие изменения зарплаты и считаем это значением зарплаты на начало 
    диапазона. После этого итерируемся из прошлого в будущее по соыбтиям 
    изменения зарплаты и как только находим следующее событие, считаем число 
    дней между ним и предыдущим (ориентируемся на `dateFrom` данных оебс). 
    Разницу дней делим на среднее число дней в месяце (`365.25 / 12`) и 
    умножаем на зарплату в этом промежутке. Участок от последнего изменения 
    зарплаты до `date_to` считаем аналогично и добавляем к сумме.

Виджет «Цели сотрудника»
-----------------------
Показываются цели, где
  * сотрудник: в исполнителях|ответственный|ответственный за критерий|заказчик
  * важность: обычные|ключевые подразделения|ключевые компании
  * статус: новые|по плану|есть риски|заблокирована

Соответствует выборке
https://goals.test.yandex-team.ru/filter?user=5853&status=0,1,5,2&importance=1,2,0

Виджет «Действия»
---------------
  * `salary` — тикеты по фильтру `queue: SALARY and resolution: empty() and assignee: me()`.
    * в тестинге очередь `TSALARY`
    * в кружочке — создатель тикета
  * `job` — тикеты по фильтру `queue: JOB and resolution: empty() and assignee: me()`.
    * в тестинге очередь `TJOB`
    * в кружочке — создатель тикета
  * `conference_trip`/`conference` — тикеты по фильтру 
     `queue: INTERCONF and status: open and assignee: me()`. 
    * в кружочке — сотрудник из поля `employee`
    * если есть поле `cities`, то это `conference_trip`, иначе `conference`
  * `trip` — тикеты по фильтру `queue: TRAVEL and status: open and assignee: me()`.
    * в кружочке — сотрудник из поля `employee`

Если в тикете заполнены поля `startDate` и `endDate` — они отображаются
Если в тикете заполнены города (`cities`) — они отображаются
Если в тикете есть маршрут (`itinerary`) — он отображается
(я точно не помню какие поля в каких очередях заполняются)

  * `offer` — показываем список **доступных** офферов в статусе **заполнена рекрутером**
  * `gap` — показываем неподтвержденные отпуски, которые релевантны смотрящему по мнению гэпа

Виджет «Список сотрудников»
---------------
  * Должны быть фильтры: 
    * непосредственные подчиненные (мое подразделение для неруководителей)
    * по каждому подраздлению, где пользователь руководит
    * сохраненные фильтры со стаффа
    * команда v-team, у которых смотрящий — owner

Виджет «История»
---------------
  * Премии и повышения прикрепляются к событию «Озвучены результаты ревью», если они попали в интервал `[review_finish_date - 30, review_finish_date + 30]`. Не попавшие в интервал отображаются отдельным событием. Это эвристика, здесь могут быть ложные срабатывания.

Техническое описание
=====

Разработка
----------
Нужен [fabric](http://www.fabfile.org/) и 
[robe](https://github.yandex-team.ru/common-python/robe)

```(bash)
# Создание виртуального окружения с зависимостями из deps
fab venv

# Активация
source .robe/dev/cab/bin/activate
(или автоматически через https://github.com/kennethreitz/env)

# Запуск разработческого сервера Django
cab runserver_plus
http://127.0.0.1:9100/werewolf/volozh
(аутентификация в девелопменте не замокана, 
нужно либо использовать werewolf, либо настроить что-то похожее на
https://github.yandex-team.ru/tools/review-draft/blob/c454eb193953c14157e0cd9dff90eb6b44a2b3be/review/settings/021-auth.conf)
```

Тесты
-----
Нужен [fabric](http://www.fabfile.org/) и 
[robe](https://github.yandex-team.ru/common-python/robe)

```(bash)
# Создание виртуального окружения с зависимостями из deps
fab venv

# Активация
source .robe/dev/cab/bin/activate

# Запуск тестов
py.test
```

В пуллреквестах тесты 
[запускаются на тимсити](https://teamcity.yandex-team.ru/viewType.html?buildTypeId=Tools_Applications_Cab_BackendTests).

Сборка и деплой
------
Деплой в qloud одинаков для всех сервисов и описан [на вики](https://wiki.yandex-team.ru/tools/dev/qloud/#deplojj).

По умолчанию деплоим в анстейбл — окружение используется для 
локальной разработки фронтенда.

Также есть репозиторий с [моками ответов бэкенда](https://github.yandex-team.ru/tools/cab-mock) — 
фронтенд использует ее для написания тестов и для разработки.

Команде разработки сервиса 
[выданы доступы](https://idm.yandex-team.ru/system/docker#role=2577028) 
на docker-образ `tools/cab`.

[Окружение в qloud](https://platform.yandex-team.ru/projects/tools/cab-back).

Сети и дырки
----
https://qloud-ext.yandex-team.ru/networks/CAB_PROD_NETS  
https://qloud-ext.yandex-team.ru/networks/CAB_TEST_NETS

Балансер  
[облачный в qloud](https://platform.yandex-team.ru/balancers/tools-cia)  
[racktables](https://racktables.yandex-team.ru/index.php?page=ipvs&tab=default&vs_id=3348)  
[racktables:доступы](https://racktables.yandex-team.ru/index.php?page=services&tab=vperms#vs-3348)  

Продакшн `_CAB_PROD_NETS_`
  * blackbox.yandex-team.ru 80
  * oauth.yandex-team.ru 443
  * calendar-api.tools.yandex.net 80
  * staff.yandex-team.ru 443
  * goals.yandex-team.ru 443
  * newhire.yandex-team.ru 443
  * review.yandex-team.ru 443
  * fb.yandex-team.ru 443
  * staff-api.yandex-team.ru 443
  * abc-back.test.yandex-team.ru 443
  * st-api.yandex-team.ru 443
  * wiki-api.yandex-team.ru 443
  * wf.yandex-team.ru 443
  * pgaas.mail.yandex.net 12000
  * vs-logstash.yandex.net 5544
  * stocks.yandex.net 80

Тестинг `_CAB_TEST_NETS_`
  * blackbox.yandex-team.ru 80
  * oauth.yandex-team.ru 443
  * calendar-api.calcorp-test-back.cmail.yandex.net 80
  * staff.test.yandex-team.ru 443
  * goals.test.yandex-team.ru 443
  * newhire.test.yandex-team.ru 443
  * review.test.yandex-team.ru 443
  * fb.test.yandex-team.ru 443
  * staff-api.test.yandex-team.ru 443
  * abc-back.yandex-team.ru 443
  * st-api.test.yandex-team.ru 443
  * wiki-api.test.yandex-team.ru 443
  * wf.test.yandex-team.ru 443
  * pgaas.mail.yandex.net 12000
  * staff01.dev.yandex-team.ru 3306 (для анстейбла)
  * vs-logstash-testing.yandex.net 5544
  * stocks.yandex.net 80
  
[ssh-дырка до сети](https://puncher.yandex-team.ru/?id=5791f172d5626d8701a1c7f4)

Базы
----
База — [PGaaS](https://wiki.yandex-team.ru/dbaas/faq/), 
квота выдана на [сервис 1664](https://abc.yandex-team.ru/services/cab/) в abc.

[базы в api](https://api.db.yandex-team.ru/api/v1.0/project/1664/cluster)

[pgaas api charts url prod](https://api.db.yandex-team.ru/api/v1.0/project/1664/cluster/bff30ca5-abaa-49dd-aed7-1a116ef770a0/charts)  
[yasm prod](https://yasm.yandex-team.ru/template/panel/dbaas_postgres_metrics/cid=bff30ca5-abaa-49dd-aed7-1a116ef770a0;dbname=cab)

[pgaas api charts url test](https://api.db.yandex-team.ru/api/v1.0/project/1664/cluster/8c7289a4-7993-40d6-bcf6-a3e62738d92e/charts)  
[yasm test](https://yasm.yandex-team.ru/template/panel/dbaas_postgres_metrics/cid=8c7289a4-7993-40d6-bcf6-a3e62738d92e;dbname=cabdb_test)

Для разработки можно использовать рекомендованный PGAAS образ
https://github.yandex-team.ru/mdb/minipgaas
запускаем в фоне и ничего не настраиваем
```(bash)
docker run -d -p 12002:12000 registry.yandex.net/dbaas/minipgaas
```

Секреты
-------
В [секретах qloud](https://platform.yandex-team.ru/secrets), 
доступ на команду разработки сервиса. 
