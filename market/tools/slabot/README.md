Мониторит очереди в стартреке и шлет уведомления, если видит несоблюдение внутренного SLA по активности в блокерах/критикалах.

- Ссылка на бота: https://telegram.me/MarketRoboBot
- Бот привязан к маркетному роботу https://staff.yandex-team.ru/robot-market
- ST очередь бота: https://st.yandex-team.ru/MARKETROBOT
- ABC группа бота: https://abc.yandex-team.ru/services/marketslabot/

# Настройки ботика
Если хотите, чтобы ботик:
### присылал в телеграм-чат уведомления о новых и напоминал в начале дня о старых тикетах, подходящих под st-фильтр:
  1. сделать фильтр в st.yandex-team.ru;
  2. добавить в [конфиг](https://a.yandex-team.ru/arc/trunk/arcadia/market/tools/slabot/config.txt) новую запись аналогичную [этой](https://a.yandex-team.ru/arc/trunk/arcadia/market/tools/slabot/config.txt?rev=5649749#L15);
  3. собрать и выкатить ботика (см. [Cборка и деплой бота](https://a.yandex-team.ru/arc/trunk/arcadia/market/tools/slabot/README.md#сборка-и-деплой-бота) );
  - Можно задать шаблон сообщения как [здесь](https://a.yandex-team.ru/arc/trunk/arcadia/market/tools/slabot/config.txt?rev=5649749#L177).
  - Можно задать интервал времени, когда уведомлять, с помощью параметров **startTime** и **endTime**.

### оставлял комментарии в тикетах, если, например, там давно не было уведомлений:
  1. сделать фильтр в st.yandex-team.ru, тогда ботик будет отписываться в те тикеты, которые попали под фильтр;
  2. добавить в [конфиг](https://a.yandex-team.ru/arc/trunk/arcadia/market/tools/slabot/config.txt) новую запись аналогичную [этой](https://a.yandex-team.ru/arc/trunk/arcadia/market/tools/slabot/config.txt?rev=5649749#L55);
  3. собрать и выкатить ботика (см. [Cборка и деплой бота](https://a.yandex-team.ru/arc/trunk/arcadia/market/tools/slabot/README.md#сборка-и-деплой-бота) );
  
Также можно задать время, через которой отписываться, в самом фильтре.


# Сборка и деплой бота
> *Внимание! Attention! Achtung! Attenzione! انتباه! 注意!*
>
> Чтобы раскатывать бота нужно быть в abc группе https://abc.yandex-team.ru/services/marketslabot. Напишите текущим руководителям этой группы, чтобы они добавили вас туда.

## Сборка
Робот собирается сендбокс таской YA_PACKAGE, можно скопировать например вот эту: https://sandbox.yandex-team.ru/task/540789515. Ничего менять не надо только нажать `Run` и ждать завершения.

## Деплой
Робот живет в Y.Deploy: https://deploy.yandex-team.ru/project/telegram-bots, чтобы задеплоить его нужно перейти в настройки и у бокса SlaBot обновить ссылку на новый пакет собранный на предыдущем шаге.

1. Склонируйте таску https://sandbox.yandex-team.ru/task/540789515 и запустите.
2. Дождитесь завершения, перейдите на вкладку `Resourses`. Найдите ресурс с именем `YA_PACKAGE`,зайдите в него и скопируйте значение строки с `sbr:****` в блоке `Files info`. (Строка вида `ya download sbr:3264082465`)
3. Зайдите в конфиг https://deploy.yandex-team.ru/stages/telegram-bots/edit/du-SlaBot#disks и замените значение в блоке `layer-1` -> `url` на значение `sbr` с прошлого шага.
4. Дальше синяя кнопка `Review Changes` сохраняете и ждете пока перевыкатится.

Иструкцию с картинками можно найти в инструкции по выкладке другого маркет бота: https://a.yandex-team.ru/arc/trunk/arcadia/market/tools/market_tg_bot/README.md

Есть проверка с нотификацией о падении бота в телегу, настроенная в yasm aka голован: https://yasm.yandex-team.ru/alert/sla_bot-readiness.

# Разработка
```
$ export DATABASE_USER=...
$ export DATABASE_PASSWORD=...
$ ./run_postgresql_local.sh
$ export SLABOT_DB_HOST=localhost
```
где DATABASE_USER и DATABASE_PASSWORD добывается из секрета https://yav.yandex-team.ru/secret/sec-01drpmng6d0n23jh9mkr1j8ey3, после этого можно запускать всё как обычно
```
$ ya make && ./slabot check --config=./config.txt
```

?? Кажется в доке не хватает про указание переменных `SLABOT_STARTREK_TOKEN`, `SLABOT_TELEGRAM_TOKEN` и `SLABOT_MAIL_TOKEN`

### Как узнать chatId чата в Telegram

1. Добавить ботика @TSUMYandexBot к себе в чат.
2. В чате позвать команду ботика /getchatid.
3. В переписку с ботиком придёт chatId.

### LOGS
Логи можно (и нужно, иначе никак) смотреть прямо из веб-мордочки:
https://deploy.yandex-team.ru/project/telegram-bots/logs, в выпадающем списке выбрать SlaBot

### Секреты
Секреты бота живут в двух секретницах:
* Токены телеграмма, стартрека, почты и проч: https://yav.yandex-team.ru/secret/sec-01drkryk3tn1jdsm5mhwq37j3p
* Имя юзера и пароль от БД в MDB: https://yav.yandex-team.ru/secret/sec-01drpmng6d0n23jh9mkr1j8ey3

### FAQ
##### Q. Бот не отправляет сообщения в телеграмм

- A1. Посмотрите логи приложения: https://deploy.yandex-team.ru/project/telegram-bots/logs
- A2. Если в логах все ок и бот пишет `issues: 0, time: 0`, то нужно дать доступы до очереди для робота @robot-market-st
