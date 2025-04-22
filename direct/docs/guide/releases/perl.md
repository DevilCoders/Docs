# Релизы "большого Директа"

{% note warning "Важно" %}

  Если не написано отдельно иного, то все работы выполняются под screen или аналогами.

{% endnote %}

## Инструменты { #perl_inv }
История коммитов (svnlog): [https://javadirect-dev.yandex-team.ru/svnlog/?app_id=14](https://javadirect-dev.yandex-team.ru/svnlog/?app_id=14)
Метатрекер: [https://direct-dev.yandex-team.ru/metatracker/](https://direct-dev.yandex-team.ru/metatracker/)
Cветофор: [https://radar.qart.yandex-team.ru/autotests/trafficLightsMonitor.html](https://radar.qart.yandex-team.ru/autotests/trafficLightsMonitor.html)
Таймлайн: [https://direct-dev.yandex-team.ru/metatracker/releaseTimeline](https://direct-dev.yandex-team.ru/metatracker/releaseTimeline)
Выгрузка отчетов: [https://radar.qart.yandex-team.ru/autotests/taggedLaunches.html](https://radar.qart.yandex-team.ru/autotests/taggedLaunches.html)
Релизный дашборд: [https://st.yandex-team.ru/dashboard/1249](https://st.yandex-team.ru/dashboard/1249)
Таблица: [https://direct-dev.yandex-team.ru/statistics/releases_table](https://direct-dev.yandex-team.ru/statistics/releases_table)
Красивые графички: [https://direct-dev.yandex-team.ru/statistics/releases_chart](https://direct-dev.yandex-team.ru/statistics/releases_chart)
Общая страница с интересными ссылками: [https://direct-dev.yandex-team.ru/statistics/](https://direct-dev.yandex-team.ru/statistics/)
Расписание дежурства: [https://abc.yandex-team.ru/services/direct/duty/?role=2051](https://abc.yandex-team.ru/services/direct/duty/?role=2051)

## Общение { #perl_chats }
 - [канал в ТГ]({{chat-direct-release}})
 - [чат в Q]({{chat-direct-admin}})


## Подготовка { #perl_a_u_ready }
1. Проверить в [svnlog](https://javadirect-dev.yandex-team.ru/svnlog/?app_id=14&file_regexp=trunk/arcadia/direct/perl) результаты запуска юнит-тестов:
   - если тесты шумят — перезапустить их и дождаться прохождения
   - если падение стабильно с какого-то коммита: пойти к разработчику задачи с просьбой посмотреть.
1. Если есть зависимости, известные даты запусков — подготовиться к ним.
1. Перед самой сборкой предупредить в [релизный чат]({{chat-direct-release}}): `Через пять минут/полчаса минут начинаю сборку релиза perl`.
1. Начинать  собирать релиз руководствуясь здравым смыслом.

{% include [этот релиз собирается роботом](_includes/java-releases-hint-auto.md) %}

Для релиза, собранного автоматикой — переходи сразу к следующему разделу.


## После сборки релиза: { #Perl_auto1 }
Если релиз успешно собрался автоматикой он в статусе New.
1. Проверить в [svnlog](https://javadirect-dev.yandex-team.ru/svnlog/?app_id=14&file_regexp=trunk/arcadia/direct/perl) результаты запуска юнит-тестов

   {% cut "выбрать нужный релиз в выпадушке" %}

   ![alt text](https://jing.yandex-team.ru/files/sonch/browser_iTupsLleRj.png "выбрать нужный релиз в выпадушке")

   {% endcut %}

   {% cut "убедится что у верхнего коммита в релизе 14 зеленных рожиц" %}

   ![alt text](https://jing.yandex-team.ru/files/sonch/browser_XeHNGDDYV4.png "убедится что у верхнего коммита в релизе 14 зеленных рожиц")

   {% endcut %}

   Если все рожицы зеленые переходим к следущему пункту. Если нет, перезпускаем упавшие юнит-тесты.

   {% cut "выбрать тест для перезапуска" %}

   ![alt text](https://jing.yandex-team.ru/files/sonch/browser_auXB9CzpyX.png "попробовать перезапустить упавший тест")

   {% endcut %}

   Для перезапуска понадобиться авторизация. Логин: sonch Пароль: 2xscgtiv

    {% cut "перезапустить тест" %}

   ![alt text](https://jing.yandex-team.ru/files/sonch/browser_JRP3ovfkcE.png "перезапустить тест")

   {% endcut %}

   Если перезапуск не помог, несем падение автору коммита.

1. Проверить, что на стендах актуальные версии. Они должны совпадать с версией в названии релизного тикета
   - Версия ТС: [в Версионике](https://direct-dev.yandex-team.ru/versionica/property?project=prehistoric&reqid=&group=&host=&property=yandex-direct%24&host_group=zknode%3A%2Fdirect%2Fnp%2Ftest%2Fhosts%2Fperl-intapi%3Bzknode%3A%2Fdirect%2Fnp%2Ftest%2Fhosts%2Fperl-scripts%3Bzknode%3A%2Fdirect%2Fnp%2Ftest%2Fhosts%2Fperl-api%3Bzknode%3A%2Fdirect%2Fnp%2Ftest%2Fhosts%2Fdirect-web)
   - [Версия на 8999](https://8999.beta1.direct.yandex.ru/registered/main.pl?cmd=showSearchPage) - смотреть под супером, в подвале :  `svn: trunk (rВЕРСИЯ)`

{% note info "Новая информация" %}

 Версия для новых хостов может отличаться:

  - direct-testing-direct-web-3.vla.yp-c.yandex.net
  - direct-testing-perl-api-2.vla.yp-c.yandex.net
  - direct-testing-perl-intapi-3.sas.yp-c.yandex.net
  - direct-ts-1-vla-9.vla.yp-c.yandex.net

 {% endnote %}

1. Применить миграции, если они есть. Все миграции в релизе находятся в релизном тикете под словами "Инструкция к выкладке", это ссылки на тикеты в очереди DIRECTMIGR. Подробнее про perl-миграции [ниже](#perl_migration)

1. Проверить [Светофор](https://aqua.yandex-team.ru/#/launches?skip=0&limit=20&packId=53427b42e4b08984236588ab)
     - если есть проблемы разбираем их,
     - если не можем сами — обращаемся за помощью к [дежурному Релизы + ТС](https://abc.yandex-team.ru/services/direct-app-duty/duty2/30726)

1. Пишем комментарий в релизный тикет:

     `ТС, беты 8999 и 8080 обновлены, миграции применены. Светофор зеленый. Релиз готов к тестированию.`

    Если что-то из перечисленного не так, но исправить не получается — написать, что происходит и что несмотря на это релиз все-таки стоит начинать тестировать (если и это неправда, то не надо нажимать ReadyForTest).

1. Переводим релизный тикет в статус **ReadyForTest**  (в Testing его перевед робот и запустит миграцию)

1. Проверяем что сработала джоба, создающая тикеты на регрессию. В релизном тикете появятся тикеты на регрессию, [ревью непродуктовых коммитов](https://wiki.yandex-team.ru/direct/development/howto/releases-review/) и информация о зависимостях.


## Тестирование { #perl_cont }

Основные задачи:

- отслеживание текущего состояния релиза
- отслеживание своевременности работы с тикетами
- перераспределение задач при необходимости
- коммуникация со всеми участниками процесса
- принятие решений относительно актуальности/срочности/критичности релизных задач

 Подробнее:

- Перераспределение тикетов, если ответственный за него не может посмотреть сам;

- Назначить тикет Непродуктовых коммитов (если он есть) на дежурного по [дежурному Релизы + ТС](https://abc.yandex-team.ru/services/direct-app-duty/duty2/30726) (будет делаться автоматически после [тикета](https://st.yandex-team.ru/DIRECT-144568) )

- Просмотреть задачи в релизе, проставить тег **limited_by_release_regression** тикетам, которые ждут только пробега релизной регрессии (чтобы они не учитывались в статистике по таскам);

- На любую проблему (с кодом, тестами, миграцией, инфраструктурой, пониманием задач, комментариям к тестам), которая не решается за 15 минут должен быть тикет и комментарий в релизном таске. Если проблема мешает тестировать что-то, тестирование чего занимает более 30 минут — можно ставить ему приоритет __Critical__.
- На любой баг/исправление в коде и тестах, которые писал не ты — тикет тоже должен быть.

- [Хотфиксами](#perl_hot) на ТС везем только то, что критично к релизу. Запросы на хотфиксы нужно создавать на страничке с историей коммитов [тут](https://javadirect-dev.yandex-team.ru/svnlog/?app_id=14). Подробнее про [ХФ](#perl_hot)

- Разбор регрессионных автотестов веб-интерфейса назначенный на тебя:
    + В тикетах на регрессию отражаем ход процесса
    + Заводим тикеты на баги
    + Заводим тикеты на изменения автотестов по [шаблону](https://st.yandex-team.ru/createTicket?summary=Починить%20автотесты%3A&description=Причина%20падения%3A%0A%0AОтчет%20с%20ошибкой%3A&type=2&priority=2&components=39399&queue=DIRECT) c назначением на [дежурного по Регрессии веб-тестов старого интерфейса](https://radar.direct.yandex-team.ru/radar-rest/onduty/redirect-to-duty-staff/web-regression)
    + Проводим ручные проверки при необходиомсти

К окончанию тестирования релиза тикеты на миграции должны быть в правильном статусе:
  - если ок — **Ready For Production**
  - не ок — другой статус и желательно комментарий о том, что в ПРОДАКШЕНЕ НЕ ПРИМЕНЯЕМ — можно жирненьким и красненьким :)


Если после начала тестирования обнаруживается, что есть проблемы сразу по нескольким фронтам (AQUA, Биллинг, API, JAVA и интерфейс) по мере необходимости собираем брифинг из дежурных по релизу. Инициатор — ответственный за релиз тестировщик. Координация в чате.

{% note warning "Важно" %}

  Что-то произошло, и ты не знаешь, что делать? Ты знаешь, что делать: писать в чат :)

{% endnote %}

Релиз считаем протестированным, когда все прилинкованные таски закрыты, миграции готовы к проду, все возникшие вопросы решены.


## Завершение тестирования { #perl_end_ok }

 Когда релиз дотестирован:

1. Меняем статус тикета жмем __Passed__.
Оставляем комментарий по шаблону. Подключить шаблон комента можно [тут](https://st.yandex-team.ru/settings/templates/comments?name=Релизный%20коммент&owner=1120000000006354&queue=DIRECT)

1. Закрываем релиз командой
    `direct-release -a direct -s testing testing-done`

1. Отправляем сообщение в релизный чат:
    `🏁 Релиз большого Директа протестирован`

1. Выгружаем отчеты [тут](https://radar.qart.yandex-team.ru/autotests/taggedLaunches.html) / Нужно для аудита
    - указываем релизный тег (тег берем из ссылки на регрессию), формируем список отчетов

     {% cut "тег берем тут" %}

   ![alt text](https://jing.yandex-team.ru/files/sonch/browser_AdWvSWLDGZ.png "тег берем тут")

   {% endcut %}
    - указываем номер тикета релиза (в формате DIRECT-11111)
    - выбираем все завершенные с успешным прохождением запуски финансовых областей (тесты где в названии есть Finance)
    - прикрепляем отчеты к релизу (проверяем что появится в релизном тикете в прикрепленных файлах)

Посмотреть очередь релизов:
    `direct-release -a direct overview`

Проверить что в waiting нет релизов в статусе Closed
Сдвинуть выложенные релизы
    `direct-release -a direct -s stable next-waiting`

Для не выложенных релизов проверить забытые ХФ (цифра 1 возле вейтинга может быть другой, в зависимости от проверяемого релиза):
    `direct-release -a direct -s waiting-1 check`
Довезти хотфикс в нужный вейтинг:
    `direct-release -a direct -s waiting-1 hotfix NNNNNN`

## Заказ выкладки { #perl_go }

Заказ выкладки релизов [происходит автоматически роботом](../../concepts/releases/deploy-schedule.md)
в штатное время: __11.00__, __14.00__, __16.00__ (за исключением пятницы).

Проследить за выкладкой, заказать её в другое время или договорится о других ситуациях можно в [чате Q]({{chat-direct-admin}}).

## Выкладка в прод

{% note warning "Сначала принять в тикете, потом выкладывать" %}

**Проверить что релиз в Ready to Deploy, Accept должен быть нажать до того, как будет сделано direct-version-set**

{% endnote %}

Выкладка производится с продакшеновых машин, именуемых [ppcback-ами](../../jeri/things/ppcback).

Запускать команды можно без `tmux`, где надо `tmux` запустится само.

- Записать версию в ZK:

  `direct-version-set direct <версия>`

  `<версия>` берется из заголовка релизного тикета, например, для тикета [DIRECT-173645](https://st.yandex-team.ru/DIRECT-173645) она будет `1.9734444.9750899-1`.

- Сохранить предыдущую версию приложения из вывода команды на случай отката.

  Выложить нужную версию пакета:

  _откроет tmux-сессию с выкладкой на лимтест и "основной продакшен" в разных окнах_

  `direct-up-all <version>`

- После окончания выкладки убедиться, что в [версионике прописалась](https://direct-dev.yandex-team.ru/versionica/property?project=prehistoric&reqid=&group=&host=&property=yandex-direct%24&host_group=c%3Adirect_perl) новая версия для всех серверов, кроме залоченных `%limtest%`.

## Миграции { #perl_migration }

1. Определить тип миграции.

 Если это скрипт, то переводим тикет DIRECTMIGR в статус  __Ready for test__ с комментарием: "На ТС не применяю, будет применено разработчиком или QA в рамках тестирования задачи в релизе"

 Если это миграция с базой данных то переходим к следующему пункту

1. Определяем можем ли применить сами или нужна помощь

    Тип | Можем ли применять
    :---  | :---:
    create | ✅
    rename | ✅
    создание/обновление флагов _insert/update ppcdict.ppc_properties_  | ✅
    точечные исправления данных _insert/update/delete в ppc_ | ❌
    drop to_delete (_проверяем на drop if exists_) | ✅
    drop обычной таблицы | ❌
    alter легкий (dbs_sql / быстрый) | ✅
    alter тяжелый (dbs_pt-osc / время < 10мин.) | ✅
    alter тяжелый (dbs_pt-osc / время > 10мин.) | ❌



1.  Перед применением __альтеров__ проверяем изменения миграции (пример для базы ppc):
   `dbs-analyze-alter ts:ppc:1 -q -`  (жмем Enter)
   `сам альтер`  (жмем Enter)
    `ctrl+D`

1. __Важно__: для миграций с параметрами ALGORITHM и LOCK:
    - если указаны __ALGORITHM=INPLACE,LOCK=NONE__, то можно делать миграцию как обычную;
    - если указан __не__ __ALGORITHM=INPLACE,LOCK=NONE__ и при этом нет комментария о том, что применять миграцию нужно через pt-osc, то возможно это проблема в миграции. Нужно связаться с автором и ревьюверами миграции и уточнить, почему миграция именно такая

1. Для применения простых миграций на ppc:

    - `direct-sql ts:ppc:all -q -`  (жмем Enter)
    - вставляем текст миграции из тикета  (жмем Enter)
    - нажимаем Ctrl+D
    - аналогично применяем миграцию на песочнице
    `direct-sql tsb:ppc:all -q -`

    {% note info "Пример применения миграций на других схемах" %}

    * ppcdict: `direct-sql ts:ppcdict -q -`
    * песочница ppcdict: `direct-sql tsb:ppcdict -q -`

    {% endnote %}

1. Для миграций __dbs_pt-osc__:
    - в screen заходить не нужно
    - в первом окне открываем guard
    `dbs-guard --db ppc ts:ppc:all`
    - во втором окне применяем миграцию:
    `dbs-pt-osc ts:ppc:all 'alter table my_test_table_osc add column c_bigint_1 bigint'`
    - в первом окне закрываем guard. Ctrl+C завершает процесс dbs-guard, Ctrl+D выходит из окна тмукса, повторить много раз (для каждого шарда)

1. После применения миграции пишем комментарий: "Применено на ТС и ее песочнице" и переводим в статус __Deploy to testing__
1. Далее тот, чья миграция (смотри прилинкованные тикеты к DIRECTMIGR), должен посмотреть применённую миграцию на ТС, написать в тикет DIRECTMIGR коммент, что всё хорошо и поставить статус __Ready for Production__
1. Для применения миграции app-duty следуют [инструкции](https://wiki.yandex-team.ru/jeri/app-duty/releases/#primeneniemigracijj)

## ХотФиксы { #perl_hot }

{% include [примечание про ОК от Леши](_includes/new-tasks-hotfixing.md) %}

{% note info %}

Хотфиксами на ТС везем только то, что критично к релизу.

{% endnote %}


Команда привоза обновления: _(номера ревизий надо через пробел)_
    `direct-release -s testing -a direct hotfix 12345 12346`

После этого обновить ТС и беты вручную:

ТС:
     `direct-release -s testing -a direct test-update`

Беты 8999 и 9091:
    `direct-release -s testing -a direct release-beta-up 8999 9091`

{% note info %}

Если сборка ХФ упала, то можно посмотреть рекомендации по каманде `direct-release -s testing -a direct what-to-do`.

Необходимо действовать аккуратно с рекомендациями (recommended:), не стоит выполнять команду `testing-done`,т.к. данная команда завершит тестирование и отправит релиз в очередь, а не решит проблему.

Если команда из рекомендаций не помогла, то следует обратиться к дежурному разработчику.


{% endnote %}

{% note info %}

За выкладкой Хотфиксов в прод согласуем это в тикете, по аналогии с хотфиксами на ТС, ставим в исзвестность дежурного AppDuty после чего собираем хотфикс в прод, не забыть добавить хотфикс во все релизы собранные после того в который везется хотфикс.

{% endnote %}

{% note info %}

Если упало подписание пакетов и хотим продолжить сборку хотфикса на другой машине (например, с настроенным GPG), то потребуется установить состояние релиза вручную командой

    hotfix-merge-manual-complete svn+ssh://arcadia.yandex.ru/arc/branches/direct/release/perl/release-8165726 8167886

Здесь первый аргумент — это релизный бранч с хотфиксом, второй — базовая ревизия (подходит ревизия первого коммита в бранч)

Далее выполняем те команды, которые предлагает what-to-do.

{% endnote %}


## Slide { #perl_slide }

До определенной ревизии:

   `direct-release -a direct -s testing slide 12345`

До HEAD-а:

   `direct-release -a direct -s testing slide`

После слайда - обновить беты (ТС, 8999, 9091)
Для других релизов (java-web, etc.) команда точно такая-же.


## Прогон Unit тестов { #perl_unit }

1. собрать транковую бету

2. в бете запустить:

   `direct-mk test-full`

3. перейти в data3

4. запустить тесты фронта:

   `make separated-tests`

## Исторические ссылки

Страница про [выкладку релизов из wiki](https://wiki.yandex-team.ru/jeri/app-duty/releases/).

## Устаревшие данные { #perl_deprecated }
1. на этапе подготовки больше не надо выполнять "Назначить себя ответственным тестировщиком":
   - нажать кнопку "Теперь ответственным за релиз тестировщиком буду я" [тут](https://direct-dev.yandex-team.ru/rights/)
   - Проверить что так же дежурство отображено [тут](https://radar.qart.yandex-team.ru/release/directOnDuty.html)
1. Ручная сборка:
   - Начать сборку через direct-release:
    `direct-release -s testing -a direct create-release`

 	Что произойдет:
   - взвод релизного флага;
   - сборка пакетов;
   - dmove пакетов и зависимостей;
   - обновление ТС;
   - обновление релизных бет (8080 и 8999, 9090 и 9091)

  -  _Если_ create-release упал, можно попробовать ещё повторить сборку с момента падения командой continue-create-release:
  `direct-release -a direct -s testing continue-create-release`

  - После успешного create-release переименовываем релиз:
  `direct-release -s testing -a direct rename 'название релиза'`
