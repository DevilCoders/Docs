_Workplace_ - инструмент для инцидент-менеджмента, а также подсчета различных статистик Search Prod Incidents и RTC-Support. Представляет также тулзы для подсчета даунтайма по инцидентам, вьюшку для передачи сведений между дежурными и некоторые другие удобства.

**Level 0.**
1. [Arcadia starter guide](https://wiki.yandex-team.ru/arcadia/starterguide/)
2. Python style guide (смотреть выше)
3. [Подготовка окружения](https://wiki.yandex-team.ru/jandekspoisk/sepe/dezhurnajasmena/workplace/Razrabotka/Podgotovka-okruzhenija/)
4. [Локальная база](https://wiki.yandex-team.ru/users/epsilond1/jandekspoisk/sepe/dezhurnajasmena/goals/rabochee-mesto/make-pg/)

**Level 1.**

Собрать Workplace локально.

`cd arcadia`

`svn up`

`ya make -j0 --checkout search/mon/workplace`

`cd search/mon/workplace`

`ya make`

**Level 2.**

Запустить Workplace локально

1. Создать переменные окружения (DB_URL, OAUTH_TOKEN). За реквизитами к БД обращаться к epsilond1@, groovik@, talion@.
2. [Склонировать Frontend](https://a.yandex-team.ru/arc/trunk/arcadia/search/mon/workplace/ui)
3. В каталоге с фронтом сделать `npm install && npm run build && npm start`
4. Настраиваем подключение к базе данных prestable.

4.1 `export DB_URL=postgresql://workplace_admin:<pass>@<masterhost>:6432/workplace_testdb_pg`

4.2 [masterhost](https://yc.yandex-team.ru/folders/foot3c8nf926p33s20gn/managed-postgresql/cluster/c499427d-eae9-4708-8b6b-421050692d20?section=hosts)

5. `export OAUTH_TOKEN=<your_token> or <token_robot-searchmon>`

6. [Запустить serval](https://a.yandex-team.ru/arc/trunk/arcadia/search/horadric2/doc/local-dev.md)
7. `cd arcadia/search/mon/workplace && ./src/bin/entrypoint/workplace_executable`
8. Если вы не хотите дебажить кортуины, надо добавить флаг `--no-coroutins`


**Level 3.**

Если изменена proto-схема, надо сгенерировать новый horadric-prj:

Детально
<details>
  
`cd search/horadric2/cli`

`./cli/horadric ~/arcadia/search/mon/workplace/inifuss.scroll`

`cd /junk/horadric-workplace/ && ./horadric-tmp`

`vim search/mon/workplace/src/frontend/package.json` -> подними версию

`npm adduser --registry=http://npm.yandex-team.ru/`

`npm publish --registry=https://npm.yandex-team.ru`
  
</details>


Быстро
<details>
    
    `ya tool horadric`
</details>

Данные способы делают одно и тоже, просто первый вариант показывает как все это работает под капотом.

**Level 4.**

Как сходить в бекендную ручку (localhost):

Описание ручек:

1. [Человеческое (тут не все!)](https://wiki.yandex-team.ru/jandekspoisk/sepe/dezhurnajasmena/workplace/catalog/) 
2. [Protobuf](https://a.yandex-team.ru/arc/trunk/arcadia/search/mon/workplace/protoc/services)

**Level 5.**

Деплоимся мы [SB-таской](https://sandbox.yandex-team.ru/task/352386586/view). Нужно склонировать таску, поменять ревизию (чаще всего достаточно просто стереть - тогда собираться будет из транка). Таска запускается нажатием кнопки RUN.
После успешного выполнения нужно нажалть Release -> stable, через пару минут сварится релиз для няни. Эфпячим страницу с таской, появляется ссылка на Nanny-релиз. Проходим, видим два тикета (`workplace_prestable` и `workplace-zephyr`) . Сначала катим на престейбл глобал-активейтом, убеждаемся, что всё ок и катим на прод.

**Level 6.**

Админка управления [базой](https://yc.yandex-team.ru/folders/foot3c8nf926p33s20gn/managed-postgresql/cluster/c499427d-eae9-4708-8b6b-421050692d20).

Реквизиты к базе: Доступ просить у talion@ или epsilond1@.

** Level 7.**

#### Конфиги
1. Конфиги и шаблоны катаются отдельной таской. Чтобы доставить конфиг или шаблон в прод, достаточно комитить их в каталог configs или templates соотвественно. Таска подтягивает все файлы из каталога.
2. Конфиг корутин лежит в /configs/coroutines_settings.yaml. Каждая верхнеуровневая секция отвечает за описание конкретной корутины. Важный момент: параметр debug должен быть в значении True везде, кроме production. Это выключает призыв/добавление каких-либо реальных людей в создавые таски, а также влияет на кастомное поведение, необходимое для отладки конкретных корутин. 
