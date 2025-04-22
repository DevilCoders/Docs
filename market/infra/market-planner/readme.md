
## Планнер
[Testing](https://planner-test.market.yandex-team.ru)\
[Production](http://planner.market.yandex-team.ru)

---

### Документация

[Вики](https://wiki.yandex-team.ru/Market/projects/marketstat/support/mstat-planner/)\
[Релизный процесс](https://wiki.yandex-team.ru/users/rainur/reliznyjj-process-planner/)\
[Вики фронт](https://wiki.yandex-team.ru/users/myhellsing/sistema-planirovanija-resursov/planner-frontend/)\
[API Планера](https://a.yandex-team.ru/arc_vcs/market/infra/market-planner/planner-api.md)

---

### Мониторинги и графики

Postgresql testing: [mdb](https://yc.yandex-team.ru/folders/fooiglq05bsfrq012h1k/managed-postgresql/cluster/mdb3mh9mgris73qn6fja), [memory usage](https://solomon.yandex-team.ru/?project=internal-mdb&service=dom0&cluster=internal-mdb_dom0&graph=mdb-prod-hosts-memory-bytes-stacked&l.cid=mdb3mh9mgris73qn6fja&b=1d&e=)\
Postgresql prod: [mdb](https://yc.yandex-team.ru/folders/fooiglq05bsfrq012h1k/managed-postgresql/cluster/mdbsi1jfcj98uvpri6mv), [memory usage](https://solomon.yandex-team.ru/?project=internal-mdb&service=dom0&cluster=internal-mdb_dom0&graph=mdb-prod-hosts-memory-bytes-stacked&l.cid=mdbsi1jfcj98uvpri6mv&b=1d&e=) \
Мониторинги: [все](https://juggler.yandex-team.ru/aggregate_checks/?query=tag%3Dmarket_planner&view=tiles), [testing](https://juggler.yandex-team.ru/aggregate_checks/?query=tag%3Dmarket_planner%26tag%3Dtesting&view=tiles), [production](https://juggler.yandex-team.ru/aggregate_checks/?query=tag%3Dmarket_planner%26tag%3Dproduction&view=tiles)\
Графики porto: [testing](https://yasm.yandex-team.ru/template/panel/market-porto/itype=marketmstatplanner;ctype=testing;prj=market/), [production](https://yasm.yandex-team.ru/template/panel/market-porto/itype=marketmstatplanner;ctype=production;prj=market/)\
Графики nginx: [testing](https://yasm.yandex-team.ru/template/panel/market-nginx/itype=marketmstatplanner;ctype=testing;prj=market/), [production](https://yasm.yandex-team.ru/template/panel/market-nginx/itype=marketmstatplanner;ctype=production;prj=market/)\
[Дашборд в Solomon](https://solomon.yandex-team.ru/?project=market-planner&cluster=PRODUCTION&service=market-planner&dashboard=market-planner-monitorings-prod)
[Дашборд в графане](https://graf.yandex-team.ru/d/1h0NeY6Mk/market-planner?orgId=1)

---

### Для разработчиков

[Nanny сервисы](https://nanny.yandex-team.ru/ui/#/services/dashboards/catalog/market_mstat_planner/)\
[Релизная машина в ЦУМе](https://tsum.yandex-team.ru/pipe/projects/market-planner/delivery-dashboard/market-planner-2)\
Секреты: [testing](https://yav.yandex-team.ru/edit/secret/sec-01d190b7r9myne599hahdah52e/explore/versions),
[multitesting](https://yav.yandex-team.ru/secret/sec-01es0q05f65r09jbnc7c7xrtbp/explore/versions),
[production](https://yav.yandex-team.ru/secret/sec-01d190rytb2h855hbsrg5593jx/explore/versions),
[ТВМ тест](https://yav.yandex-team.ru/secret/sec-01d9qhfd7qt6zjb4cx98ksrts5/explore/versions),
[ТВМ прод](https://yav.yandex-team.ru/secret/sec-01d9qvez3wfxpzjvekmhawa03a/explore/versions).\
Робот Маркетпланнер:
@robot-market-planner,
[доменный пароль](https://yav.yandex-team.ru/secret/sec-01d1brc8ed6v7kajp8hd763gve/explore/version/ver-01d1brc8gx9evcvz9es25b4w8s).\
Sandbox группа [MARKET-PLANNER](https://sandbox.yandex-team.ru/admin/groups/MARKET-PLANNER) где хранятся [токены](https://sandbox.yandex-team.ru/admin/vault?owner=MARKET-PLANNER) для запуска интеграционных тестов.

---

## Сборка и запуск
Есть некоторые особенности сборки.

Старый фронт был написан с помощью шаблонизатора twig. Внедряется новый фронт на React ( лежит в папке webapp).

CI не поддерживает доступ к внешней сети, а это нужно для скачивания node_modules и сборки нового фронта.
Поэтому, при сборке в CI фронт и его зависимости игнорируется.

Фронт и бек отдельно собираются в двух разных кубиках в пайплайне ЦУМа и приезжают вместе в контейнер nanny.
Бекенд запускается скриптом, сделанным по шаблону start-with-front.sh, в котором заранее прописан jar с фронтом в classpath.

## Локальный запуск через IDEA

#### Сгенерировать проект для IDEA
Не забудьте проверить, что аркадии вмонтирована ``arc mount ~/arcadia``.
```
cd ./<путь до arc>/market/infra/market-planner
./generate_project.sh -i <папка куда сгенерировать проект (idea_projects если не указать параметр)>
```

Открыть проект в IDEA и изменить автосгенерированную конфигурацию ``Run Service (generated)``:\
заменить в Environment variables строчку ``environment=local`` на ``environment=development;front.jar.exclude=true``

``environment=development`` запустит Планнер локально с embedded базой (как в мультитестинге).\
Можно запустить с подключением к базе в тестинге (не рекомендуется) используя ключ ``environment=local``

#### Добавить необходимые секреты

Все секреты можно прописывать в ``Enviroment variables``, или создать отдельный файл в `src/main/properties.d/10_application.properties` и добавлять секреты туда (не стоит добавлять этот файл в vcs arc).\
Нужны следующие проперти: ``DB_PASSWORD``, ``STAFFAPI_TOKEN``, ``ABCAPI_TOKEN``, ``STARTREK_TOKEN`` и ``TRACKER_TOKEN``.
Прописывать их надо именно с такими именами. В конечном итоге, они прорастут в нужные значения, например ``DB_PASSWORD`` -> ``mstat_planner.jdbc.password``

Только ``DB_PASSWORD`` обязательный для запуска приложения. Остальные серкреты можно заполнить случайными значеними, если вы их не используете.

При локальном запуске подключаемся к базе testing'а.\
Нужно взять из [секрета для тестинга](https://yav.yandex-team.ru/edit/secret/sec-01d190b7r9myne599hahdah52e/explore/versions) значение ``mstat_planner.jdbc.password`` и прописать его в ``DB_PASSWORD``.
Аналогично поступить с другими секретами.

#### Установить плагины
1. lombok - аннотации заменяют методы getter setter и т.д https://plugins.jetbrains.com/plugin/6317-lombok

    !! Уже несколько человек сталкивались с этим и потратили на это несколько часов. Скорее всего лучше сразу ставить эту настройку [После обновления IDEA слмался lombok](https://a.yandex-team.ru/arc/trunk/arcadia/market/infra/market-planner#posle-obnovleniya-idea-slmalsya-lombok)
2. Twig - поддержка шаблонизатора twig

#### Подключение нового фронта

[wiki-Дока по фронту](https://wiki.yandex-team.ru/users/myhellsing/sistema-planirovanija-resursov/planner-frontend/#kakzapustitfront)

На проде/тестинге/мультитестинге фронт подключается добавлением собранного в jar файл фронта в classpath.\
Это контролиуется [HtmlWebappController](https://a.yandex-team.ru/arc_vcs/market/infra/market-planner/src/main/java/ru/yandex/market/mstat/planner/controller/HtmlWebappController.java).
`@Profile({"development", "testing", "production"})` указывает в каких окружениях спринга планер будет искать фронт в jar файле.
Окружение контролируется пропертей `-Denvironment`.\
Фронт будет доступен тут: http://localhost:8080

Чтобы не собирать фронт в jar файл, а запускать локально рядом через `npm start` и ходить на фронт по адресу: http://localhost:3000,
необходимо добавить в конфигурацию запуска приложения в IDE в строку VM options дополнительный параметр `front.jar.exclude`.

Примеры, когда будет искаться фронт в jar:
1) Параметр не был передан
2) `-Dfront.jar.exclude=false`

Во всех остальных случаях фронт искаться не будет:
1) `-Dfront.jar.exclude=true`
2) `-Dfront.jar.exclude`
3) `-Dfront.jar.exclude=efsdtdrte`\
...

##### Вариант 1: как на проде/тестинге/мультитестинге

Если front.jar.exclude=false,

Собрать фронт в jar
```
cd webapp
npm i
ya make
```
Добавить jar с фронтом в classpath в IDEA
```
Project Structure -> Librares -> + -> Java -> выбрать jar webapp/mstat-planner-webapp.jar -> Classes
```

##### Вариант 2: компиляция нового фронта на лету
1. Запустить заранее подготовленную конфигурацию MstatPlanner
2. Запустить новый фронт
```
cd webapp
nvm use 12
npm i
npm start
```

Старый тут: http://localhost:8080\
Новый фронт тут: http://localhost:3000

### Возможные ошибки

* **не подключен новый фронт**\
``Error creating bean with name 'htmlWebappController': Invocation of init method failed; nested exception is java.lang.NullPointerException``\
https://paste.yandex-team.ru/1768033\
Не подключен новый фронт в IDEA. Нужно собрать jar и подключить его в classpath по инструкции выше. Либо запускать новый фронт с компиляцией на лету.

* **проблемы с зависимостями**\
Если открывать в IDEA через planner.ipr, возможны проблемы с зависимостями.
Чинится сохранением в другом формате:
![формат](https://jing.yandex-team.ru/files/pavellysenko/photo_2020-10-20_12-44-30.jpg)


## Подключение к базе через IDEA

Для подключения к postgres через IDEA может потребоваться отключить ipv4
``Help -> Edit custom VM options -> -Djava.net.preferIPv4Stack=false``

Connection type: URL only

![Пример](https://jing.yandex-team.ru/files/pavellysenko/Screenshot_20201020_162851.png)

**Тестинг**
```
marketstat_planner_testing
jdbc:postgresql://sas-u8hswp6zrpoo5cvo.db.yandex.net:6432,vla-zowqsp0dbsfvvuhc.db.yandex.net:6432/marketstat_planner_testing?sslmode=require&sslmode=require&targetServerType=master&prepareThreshold=0&connectTimeout=1
```
пароль ``mstat_planner.jdbc.password`` из [секретницы](https://yav.yandex-team.ru/edit/secret/sec-01d190b7r9myne599hahdah52e/explore/versions)


**Прод**
```
marketstat_planner_prod
jdbc:postgresql://man-kbnw555agjpte3bs.db.yandex.net:6432,sas-8h60lfxooffsyaut.db.yandex.net:6432,vla-2rn8fvqad74o6q89.db.yandex.net:6432/marketstat_planner_prod?sslmode=require&sslmode=require&targetServerType=master&prepareThreshold=0&connectTimeout=1
```
пароль ``mstat_planner.jdbc.password`` из [секретницы](https://yav.yandex-team.ru/secret/sec-01d190rytb2h855hbsrg5593jx/explore/versions)

**Embedded**

```
логин\пароль postgres\postgres
jdbc:postgresql://localhost:44627/postgres
```
где 44627 это порт из VM options в конфиге локального запуска ``-Dpostgres.embedded.port=44627``



## Тестирование
Локально запускаем интеграционные тесты, но бывает что какой-то фунуционал можно протестить как минимум в тестинге (в embedded базе почти нет данных или отправка писем локально не предусмотренна).

### Как выкататься в тестинг из ветки
В тестинг можно выкатится из дев ветки без мерджа в trunk.
[Вот тут](https://tsum.yandex-team.ru/pipe/projects/market-planner/release/new/market-planner-build-front-2), с таким синтаксисом: `arcadia-arc:/#users/nishinkarenko/MARKETQPLANNER-1425`.

### Как тестировать нотификации (письма на почту).
Письма отправляются только в проде. Даже в [тестинге они заглушены](https://a.yandex-team.ru/arc/trunk/arcadia/market/infra/market-planner/src/main/properties.d/testing/00_application.properties?rev=r8439399#L21).

Локально при запуске интеграционных-тестов можно размокать [NotificationService](https://a.yandex-team.ru/arc/trunk/arcadia/market/infra/market-planner/src/integration-test/java/ru/yandex/market/mstat/planner/config/ServicesAndDaoConfig.java?rev=r8439399#L172). Отправки письма не случится, но можно будет проверить что содержание письма собирается правильно.

Чтоб получить честное письмо для тестирования нужно временно менять пропертю. Или в коде отключать [проверку](https://a.yandex-team.ru/arc/trunk/arcadia/market/infra/market-planner/src/main/java/ru/yandex/market/mstat/planner/util/EmailSender.java?rev=r8439399#L48). Это допустимо если мы выкатываемся в тестинг без мерджа в trunk как описано [выше](https://a.yandex-team.ru/arc/trunk/arcadia/market/infra/market-planner/readme.md?edit=true#kak-vykatatsya-v-testing-iz-vetki). Если всё хорошо - возвращаем всё как было и мерджимся в транк.

## How to fix

### ERROR:  canceling statement due to lock timeout

#### Способ 1

https://wiki.yandex-team.ru/artemstraxov/manyhintspostgresql/#kaknajjtiktolochitzapros

```
-- открываем 2 сессии к базе
-- узнаем свой пид
SELECT pg_backend_pid();
-- убираем таймаут, чтоб запрос повис
SET lock_timeout TO 0;
-- выполняем запрос, он должен зависнуть
select * from employees;

-- во второй сессии узнаем кто блочит наш запрос по пиду первой сессии
select pg_blocking_pids(457042);
-- вернется пид того кто нас блокирует, узнаем подробнее про этот процесс
select * from pg_stat_activity where pid=308723;
-- убиваем если мешает
SELECT pg_terminate_backend(308723);
```

#### Способ 2
```
SELECT pl.pid, pc.relname, query FROM pg_locks pl
    LEFT JOIN pg_stat_activity psa ON pl.pid = psa.pid
    LEFT JOIN pg_class pc on pl.relation = pc.OID
where state = 'idle in transaction'
order by pl.pid;
```
1) Строк может быть много, но pid-ов на самом деле не много (по ним отсортировано).\
Держим в голове какая операция у нас не проходит и блокируется.\
Смотрим на столбец ``relname`` и ищем какие отношения могут нас блочить.\
Также понять блочит или нет может помочь столбец ``query`` с выполняемым запросом.\
По ситуации можно вывести и другие столбцы, но обычно должно хватить и этих.\
   \
_Например,_ если мы хотим выполнить ``truncate table employees;`` и у нас блочится запрос,\
то ищем среди ``relname`` ``employees`` или производные (``_idx``, ``_pk``).
   ####
2) Если считаем, что какое-то отношение нас блочит, то берем ``pid`` из соседнего столбца и подставляем сюда:
```
SELECT pg_terminate_backend(pid);
```


### ERROR: ...liquibase.exception.LockException: Could not acquire change log lock
Выкладка в тестинг залипла. Ошибка видна в логах хоста.
Решение: хакнуть лок в базе
`UPDATE DATABASECHANGELOGLOCK SET LOCKED=false, LOCKGRANTED=null, LOCKEDBY=null where ID=1;`

### FileNotFoundError: [Errno 2] No such file or directory: 'openapi-generator'
`pip3 install openapi-generator-cli`

### После обновления IDEA слмался lombok
[Решение со stackoverflow](https://stackoverflow.com/questions/65128763/java-you-arent-using-a-compiler-supported-by-lombok-so-lombok-will-not-work-a)\
настройки -> build, execution, deployment -> compiler, в Shared build process VM options прописать -Djps.track.ap.dependencies=false

## Как писать новые ручки на mj-framework

В файле ```market/infra/market-planner/src/main/resources/openapi/api/api.yaml```
добавить новые ручки (по аналогии или воспользовавшись ручкой ```http://localhost:8080/v2/api-docs?group=Frontend API```)

Перегенерировать проект через Regenerate project (там же где и конфигурация запуска)

Перезапустить idea ```File -> Invalidate Caches / Restart ... ```

Убедится, что сгенерировались нужные контроллеры ```/market/infra/market-planner/generated/server/server-generated/ru/yandex/market/javaframework/generated/server/api/```
и заглушки ```market/infra/market-planner/src/main/java/ru/yandex/market/market/planner/api/```

Дописать недостающие методы в классах заглушках. Те dto объекты, которые сгенерировал фреймворк в коде лучше не использовать.
Лучше конвертировать их в наши собственные объекты для работы с ними (в них можно добавлять методы, если надо, и писать доп логику).
А при выдаче из заглушки конвертировать обратно в dto класс, который ожидает фреймворк.
