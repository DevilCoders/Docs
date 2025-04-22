# Выпустить релиз

1. Убедиться, что все ожидаемые в релизе задачи смержены в `master` ветку.

1. Обновить unstable стенд для проверки, что всё работает как надо и ничего не сломалось. Здесь можно будет попросить помощи у команды тестирования. Также, предварительно, можно убрать `deploy:unstable` лейблы у всех не закрытых пулл реквестов, чтобы сделать проверку более честной.

   Для запуска обновления unstable стенда переходим в teamcity на [страницу unstable задач](https://teamcity.taxi.yandex-team.ru/viewType.html?buildTypeId=YandexTaxiProjects_Infranaim_Frontend_NewFlowTest&branch_YandexTaxiProjects_Infranaim_Frontend=lavka-yango-deli-website&tab=buildTypeStatusDiv). Убеждаемся, что выбран `lavka-yango-deli-website` бранч и нажимаем `Run`.

   ![teamcity-unstable-run](images/teamcity-unstable-run.jpg)

   В открывшемся диалоге нажимаем `Run Build`.

   ![teamcity-unstable-run-dialog](images/teamcity-unstable-run-dialog.png)

1. Запустить создание релиза. Переходим в teamcity на [страницу stable задач](https://teamcity.taxi.yandex-team.ru/viewType.html?buildTypeId=YandexTaxiProjects_FrontendMonorepo_Stable&branch_YandexTaxiProjects_Infranaim_Frontend=lavka-yango-deli-website&tab=buildTypeStatusDiv).

   Убеждаемся, что выбран наш бранч и нажимаем `Run`. В открывшемся диалоге нажимаем `Run Build`.

   ![teamcity-stable-run-dialog](images/teamcity-stable-run-dialog.png)

1. В процессе выполнения этой задачи в teamcity будет собран релиз в виде docker образа, залита статика на S3 и создан релизный тикет в TAXIREL очереди куда тебя призовет робот. Ждем призыва и переходим в тикет.

1. Проверяем, что к релизному тикету прилинковались все задачи которые мы ожидаем увидеть в проде.

1. Вместе с созданием релизного тикета запускается обновление [тестинга](https://yango-deli-website.lavka.tst.yandex.net). Переходим в [няню](https://nanny.yandex-team.ru/ui/#/services/catalog/lavka_yango-deli-website_testing/) и следим за обновлением инстансов. 

   Находим новую задачу и ждем пока она перейдет в `active` статус.

   ![nanny-testing](images/nanny-testing.png)

   Также после успешного деплоя тестинга робот напишет в релизный тикет.

   ![](images/taxirel-testing.png)

1. Проверяем работоспособность тестинга и корректно ли работает сервис. Здесь можно попросить помощи у команды тестирования.

1. Если тестинг выглядит хорошо, то можно начинать раскатывать релиз в продакшн. Для этого надо дать команду в релизном тикете на раскатку релиза на престейбл.

   Престейбл – один из трех датацентров куда будет выкачен релиз. Выкатываем релиз в этот дата центр, то есть на 1/3 трафика, и смотрим по графикам всё ли идет хорошо.

   Чтобы начать выкатку на престейбл пишем в комментариях к релизному тикету команду вида `PRESTABLE OK for release:{number}`, где `{number}` внутренний номер релиза. Всю команду целиком можно скопировать там же в комментариях. 

   ![taxirel-prestable](images/taxirel-prestable.png)

   За деплоем на престейбл также следим в [няне](https://nanny.yandex-team.ru/ui/#/services/catalog/lavka_yango-deli-website_pre_stable/) и мониторим графики в графане и логи в кибане.

1. После того как релиз выкатился на престейбл и всё хорошо, чтобы выкатить в остальные два дата центра нам потребуется ОК от менеджера. Для этого необходимо явно попросить его прийти в тикет и подтвердить релиз. 

1. После получения ОКа от менеджера останется только написать в комментариях команду запуска раскатки релиза. Взять ее можно также в комментариях.

   ![taxirel-release](images/taxirel-release.png)

   Следим за деплоем в няне, графане и кибане.

1. Лично убеждаемся, что на проде всё хорошо.

1. Переводим тикет в статус `deployed`, для этого есть кнопка «Выложен в прод (для RTC)».

## Как откатить релиз

_TODO: дописать_

- Если выкатился на престейбл
- Если выкатился полностью
