# Что это
Исходники телеграмм бота robot-market-io aka Ревьюшница (https://telegram.me/IOMarketBot), для работы с ним есть отдельный чатик: https://t.me/joinchat/AA0tykPCCvw_XL7B1ar5vA

# Сборка и деплой бота
Робот живет тут: deploy.yandex-team.ru/project/telegram-bots, в юните ReviewBot.

## Сборка
Робот собирается сендбокс таской YA_PACKAGE, можно скопировать например вот эту: https://sandbox.yandex-team.ru/task/540202549. Ничего менять не надо только нажать `Run` и ждать завершения.

## Деплой
Робот живет в Y.Deploy: https://deploy.yandex-team.ru/project/telegram-bots, чтобы задеплоить его нужно перейти в настройки и у бокса ReviewBot обновить ссылку на новый пакет собранный на предыдущем шаге.

> *Внимание! Attention! Achtung! Attenzione! انتباه! 注意!*
>
> Чтобы раскатывать бота нужно быть в abc группе https://abc.yandex-team.ru/services/marketslabot. Напишите текущим руководителям этой группы, чтобы они добавили вас туда.

## Иструкция с картинками
1. Копируем сендбокс таску

<img src=https://jing.yandex-team.ru/files/zaripov-kamil/bot_deploy_sandbox_step-1.png width=800/>

2. Запускаем таску

<img src=https://jing.yandex-team.ru/files/zaripov-kamil/bot_deploy_sandbox_step0.png width=800/>

3. Таска отрабатывает за минут 15 при хорошей погоде, ждем и вытаскиваем ссылку на сгенерированнный ресурс

<img src=https://jing.yandex-team.ru/files/zaripov-kamil/bot_deploy_sandbox_step1.png width=800/>

<img src=https://jing.yandex-team.ru/files/zaripov-kamil/bot_deploy_sandbox_step2.png width=800/>

4. Копируем ссылку

<img src=https://jing.yandex-team.ru/files/zaripov-kamil/bot_deploy_sandbox_step3.png width=800/>

5. Теперь нам надо обновить пакет в Y.Deploy, идем в конфиги

<img src=https://jing.yandex-team.ru/files/zaripov-kamil/bot_deploy_step1.png width=800/>

6. Редактируем их

<img src=https://jing.yandex-team.ru/files/zaripov-kamil/bot_deploy_step2.png width=800/>

7. Вставляем ссылку из шага 4

<img src=https://jing.yandex-team.ru/files/zaripov-kamil/bot_deploy_step3.png width=800/>

8. Выкатываем пакет

<img src=https://jing.yandex-team.ru/files/zaripov-kamil/bot_deploy_step4.png width=800/>

9. Если все прошло по плану, то статус будет зеленый

<img src=https://jing.yandex-team.ru/files/zaripov-kamil/bot_deploy_step5.png width=800/>

# Секреты
Секреты бота живут в двух секретницах:
* Токены телеграмма и проч: https://yav.yandex-team.ru/secret/sec-01drpn085qewqxna0hncyyp27q
* Имя юзера и пароль от БД в MDB: https://yav.yandex-team.ru/secret/sec-01drpmng6d0n23jh9mkr1j8ey3

Доступ для этих секретов открыт всем сотрудникам abc группы https://abc.yandex-team.ru/sevices/market_report/.
