## Регламент релизов Партнерского интерфейса

Релизы собираются с понедельника по четверг, при этом за сборку и выкладку отвечает:
* понедельник, среда - дежурный [бэкенда](https://abc.yandex-team.ru/services/partnjorskijjinterfejjsjandeksa/duty/?role=1535);
* вторник, четверг - дежурный [фронтенда](https://abc.yandex-team.ru/services/partnjorskijjinterfejjsjandeksa/duty/?role=2374);

В понедельник происходит встреча "передача релиза", до встречи релизом занимается старый деружный, после докатывает новый.

##### Полезные ссылки
* [релизный дашборд](https://st.yandex-team.ru/dashboard/14545)
* [инфровый дашборд](https://datalens.yandex-team.ru/g48hm8k1akmu9-infrastruktura)
* [дашборд ZBP](https://st.yandex-team.ru/dashboard/34365)
* [чат координации релизов](https://t.me/joinchat/VC24QWxj9re_zPwH) - тут бот пишет результаты шагов выкладки и тестов
* [общий чат релизов ПИ и Адфокс](https://t.me/joinchat/V8dHkAihw34o7BeT) - тут обсуждается судьба релиза
* [ссылка на регламент на вики](https://wiki.yandex-team.ru/partner/w/docs/release/tajjmingi-ezhednevnyx-relizov/)


#### Действие дежурного в течении дня

Ссылка на регламент на [вики](https://wiki.yandex-team.ru/partner/w/docs/release/tajjmingi-ezhednevnyx-relizov/).

**Первые 4 пункта необходимо выполнить до дейли (12:00)**

1. В день релиза нужно зайти на релизный [дашборд](https://st.yandex-team.ru/dashboard/14545), найти тикет `Auto release`, назначить себя исполнителей, переименовать тикет в `Релиз NNNN. Плановый релиз от dd.mm.yy`.

2. В [шедулере](https://sandbox.yandex-team.ru/scheduler/697426/tasks) найти последую таску [PARTNER_BUILD_ALL](https://sandbox.yandex-team.ru/tasks?children=false&hidden=false&status=SUCCESS&type=PARTNER_BUILD_ALL&created=14_days) и среди ее `Child tasks` найти таски [PARTNER_DOCKER_HERMIONE](https://sandbox.yandex-team.ru/tasks?children=false&hidden=false&status=SUCCESS&type=PARTNER_DOCKER_HERMIONE&created=14_days) и [PARTNER_SCREENSHOOTER](https://sandbox.yandex-team.ru/tasks?children=false&hidden=false&status=SUCCESS&type=PARTNER_SCREENSHOOTER&created=14_days) и отсмотреть тесты. (Альтернативный способ найти таски тестов - по ссылке из [чата](https://t.me/joinchat/VC24QWxj9re_zPwH) Координации релизов).

3. После просмотра тестов дежурный отписывается в [чат](https://t.me/joinchat/V8dHkAihw34o7BeT) по состоянию релиза, есть ли баги, блокеры и тд. 
    * **Тесты прогоняются и в ПИ и в Адфокс, потому что у нас много связанного. Если упали только тесты Адфокс - это тоже блокер. Необходимо сообщить дежурному Адфокс**
    * **Если у нас есть связанные релизы (Адфокс + ПИ) - необходимо координироваться с деружрый Адфокс для синхронной выкладки**

    [Как отсмотеть тесты.](#как-отсмотреть-тесты)

4. Если тесты не обнаружили баги, переходим к пункту 6. Если есть подозрение на проблемы в релизе, то деружный должен разобраться так ли это. (При необходимости можно налить тестовый стенд таской [PARTNER_DEPLOY_RELEASE](https://sandbox.yandex-team.ru/tasks?children=false&hidden=false&type=PARTNER_DEPLOY_RELEASE&created=6_months) с тегом `TEST` и проверить на стенде). Если подтверждается наличие бага - об этом сообщается в чат релизов, выкатка релиза ставится на паузу.

5. На дейли дежурный сообщает команде статус релиза и решается, как поступить с баговаными задачами в релизе. По возможности, багованые задачи вымерживаются из релизной ветки и запускается пересборка релиза.
**Пересборка релиза запускается один раз, не позже 14:00**

6. После проверки всех тестов 
   - запускается выкладка на тестовый стенд (если не было сделано в пункте 4).

   - Далее, на ТС [команда тестирования](https://abc.yandex-team.ru/services/partnjorskijjinterfejjsjandeksa/?scope=testing) проводит необходимые ручные проверки, если необходимо, и проверяют регистрацию в ПИ. Текущий статус по тестам можно посмотреть на [дашборде](https://datalens.yandex-team.ru/g48hm8k1akmu9-infrastruktura).

    * При уровне стабильных тестов больше 90%, за тестирование заскипаных тестов отвечает команда тестирования, при уровне **мнеьше 90% - ответственность делится** между командой тестирования и командой разработки. Их можно прокликать на https://partner2-preprod.yandex.ru или на https://partner2-test.yandex.ru (ТС автоматически не выкладывается, см. 4)

    * При уровне стабильных тестов **меньше 80% - рилиз не выкатывается**

    * Далее нужно дождаться аврува на выкладку в прод от [команда тестирования](https://abc.yandex-team.ru/services/partnjorskijjinterfejjsjandeksa/?scope=testing)

      {% note warning %}

      До 17:00 принимается решение о выкладке релиза в прод

      О решении сообщается в чат релиза.

      {% endnote %}

7. Выкладка в прод
    * перед выкладкой, попросить деружного бэка [накатить](https://wiki.yandex-team.ru/partner/w/docs/release/automigrations/) before-миграции
    * отписться в чат, что собираешься выкатывать прод
    * запустить таску [PARTNER_DEPLOY_RELEASE](https://sandbox.yandex-team.ru/tasks?children=false&hidden=false&type=PARTNER_DEPLOY_RELEASE&created=6_months) с тегом `PROD`
    * после выкладки, попросить деружрого бэка [накатить](https://wiki.yandex-team.ru/partner/w/docs/release/automigrations/) after-миграции
    * убеждаемся что релиз живой, следим за мониторингами ([500-ки](https://grafana.yandex-team.ru/d/4crVowfWz/pi2-mon-web-logs?orgId=1&refresh=10s), [ErroBooster](https://error.yandex-team.ru/projects/partner?filter=environment%20%3D%3D%20production), etc)
    * закрываем релизный тикет

После выкладки в прод, дежурный смотрит за графиками в [error](https://error.yandex-team.ru/projects/partner/projectDashboard?filter=environment%20==%20production%20AND%20(service%20==%20perl_backend%20OR%20service%20==%20java_backend)) и [графане](https://grafana.yandex-team.ru/d/4crVowfWz/pi2-mon-web-logs?orgId=1&refresh=10s). При появлении подозрительного всплеска ошибок, в чате релизов координируются действия по спасению прода.

{% note alert %}

При **отклонении релиза**, важно не просто закрыть релизный тикет, а именно "Отменить"

Чтобы при сборке хотфикса случайно не собрать ветку от отмененного релиза

{% endnote %}



#### Как отсмотреть тесты

Нас инересуют таски [PARTNER_SCREENSHOOTER](https://sandbox.yandex-team.ru/tasks?children=false&hidden=false&type=PARTNER_SCREENSHOOTER&created=1_month) и [PARTNER_DOCKER_HERMIONE](https://sandbox.yandex-team.ru/tasks?children=false&hidden=false&status=SUCCESS&type=PARTNER_DOCKER_HERMIONE&created=3_days).

Таска [PARTNER_SCREENSHOOTER](https://sandbox.yandex-team.ru/tasks?children=false&hidden=false&type=PARTNER_SCREENSHOOTER&created=1_month) сравнивает постранично два стенда - то, что в проде и то, что катится в прод.
Нужно пробежаться по всем расхождениям и убедиться, что они ожидаемые. Например, если меняется логотип в ПИ, то это будет расхождение почти на всех тестах - не надо пугаться, нужно лишь убедиться, что это ожидаемо.

Таска [PARTNER_DOCKER_HERMIONE](https://sandbox.yandex-team.ru/tasks?children=false&hidden=false&status=SUCCESS&type=PARTNER_DOCKER_HERMIONE&created=3_days) проверяет конкретные пользовательские сценарии на новой версии релиза. При наличии расхождений следует убедиться, что они ожидаемы и не являются блокером релиза. Также нужно обновить эталоны.

В обоих тасках могут происходить сетевые и инфраструктурные флапы, обычно это решается ретраями, но может помочь не всегда. Если тест упал из-за инфраструктурной проблемы, то следует проверить этот тест на тестовом стейдже (пункт 6). При возникновении вопросов можно и нужно обращаться к дежурному, катившему релиз вчера или искать помощь в чате.

#### Как пересобрать релиз без изменений

Иногда в процессе сборки релиза могут возникнуть сложности со сборкой (что-то флапнуло, что-то упало, нашли проблему и т.п.).
В этих случаях может потребоваться пересборка релиза.
Для пересборки лучше использовать клонирование оригинальной таски с проставлением в зависимости от необходимости параметров вида `inherit`. При наличии такого параметра результат сборки соответствующего компонента будет взят из оригинальной таски без пересборки, если он там завершился успешно.

#### Как собрать хотфикс



Нужно 
- найти последний выкатившийся релиз (см [дашборд](https://st.yandex-team.ru/dashboard/14545) )

  {% note warning %}

  Нужно убедится что последний релиз **не был отменен**

   <details>

   Чтобы найти предыдущий выехавший неотмененный релиз, нужно

  - в Deploy [history](https://deploy.yandex-team.ru/stages/partner-production-stage/history) найти выкладки от `robot-yd-committer`
  - причем по истории выше не должно быть откатов `Revert to changes`
  - потом найти в спеке соответствующий tag
  - потом в коментариях тикетов прошлых релизов найти этот же таг
  - тогда найденый тикет и будет последним не отмененым релизом

</details>

  {% endnote %}



- сообщить в чатик релизов что будет собираться хотфикс
  чтобы не было рейса при выкладке на ТС и пр
- потом завести тикет с дашборда релизов вида `Релиз NNNN. Хотфикс от dd.mm.yy`.
- отвести новую ветку 

<blockquote>

<details>
<summary>Пример отвода ветки</summary>

В зависимости от того, какой катится хотфикс (перл, ява и фронт) - нужно взять соответствующий релизный тег и отвести от него новую ветку вида `PI-NNNN-hotfix-yymmdd`. 

  ```
arc fetch tags/releases/partner/...
arc checkout -b PI-NNNN-hotfix-yymmdd  tags/releases/partner/...
arc cherry-pick ...
arc cherry-pick ...
arc push -u users/.../PI-NNNN-hotfix-yymmdd
```
</details>

</blockquote>

- Потом черрипикнуть в ветку фиксы 
- и запустить таску [PARTNER_BUILD_ALL](https://sandbox.yandex-team.ru/tasks?children=false&hidden=false&type=PARTNER_BUILD_ALL&status=SUCCESS&created=14_days) с указанием этой ветки в соответствующем разделе perl/java/frontend.

<blockquote>

<details>
<summary>Параметры для таски:</summary>

* `Description` - Хотфикс: PI-NNN
* `Auto build` - убрать
* `Build from trunk` - убрать
* `Release ticket` - указать тикет хотфикса
* `Hotfix = yes` - говорит что данный релиз является хотфиксом
* `Regression = no` - не катить на препрод
* `Patch incomplete release` - убрать
* `ADFOX source = blank` - оставляем пустым
* `Backend source`, `Java source type`, `Frontend source`:
    * `inherit from original task` - если ее не фиксили и предыдущий релиз прошел стандартно
    * `build new from arc branch` + `Custom perl/java/frontend branch = users/.../PI-NNNN-hotfix-yymmdd`

</details>
</blockquote>

#### Дополнительные действия дежурного

В течении деружства, к вам могут обратиться коллеги из других сервисом, сязанный с ПИ. Например, МСФ раскатил релиз на тестовый стенд, и просит вас прогнать тесты ПИ с тестовым стендом. 
Для этого через интерфейс SB необходимо создать задачу `PARTNER_DOCKER_HERMIONE` и выставить следующие параметры:
* `Partner tests options` - выбрать `Run only pcode tests`
* `Use production MSF` - снять галочку

Остальные параметры оставляем по-умолчанию. (Важно, что тесты должны выполняться на продовых версиях фронта/перла/явы)

После прогона тестов нужно отсмотреть отчет и понять, сломали ли что-то изменения МСФ. О результатах отписаться дежурному МСФ, который и попросил вас прогнать тесты.

{% note warning %}

Если изменения в тестах ожидаемы и необходимо обновить скриншоты - нужно создать ветку от `trunk` с названием `MSF_update_screens` в которую добавить новые скриншоты. 
Когда дежурный МСФ напишет в саппорт чат, что МСФ в проде, то эту ветку необходимо влить в `trunk`.

{% endnote %}

#### Что-то пошло не так...

Будет дополняться
