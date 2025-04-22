# passport-pocket-service

Сервис для обработки вебхуков для релизных процессов в Паспорте.
## Userscripts

Также здесь хранятся [юзерскрипты](https://en.wikipedia.org/wiki/Userscript), облегчающие доступ к отдельным командам. Чтобы ими воспользоваться, нужно:
1) Установите `Tampermonkey` ([Firefox](https://addons.mozilla.org/ru/firefox/addon/tampermonkey/), [Chrome](https://chrome.google.com/webstore/detail/tampermonkey/dhdgffkkebhmkfjojejmpbldmpobfkfo), [Safari](https://safari-extensions.apple.com/details/?id=net.tampermonkey.safari-G3XV72R5TC), другие браузеры тоже поддерживаются), `Greasemonkey` ([Firefox](https://addons.mozilla.org/ru/firefox/addon/greasemonkey/)) или другое расширение для поддержки юзерскриптов
2) Добавьте в браузер нужный юзерскрипт из [имеющихся](https://github.yandex-team.ru/passport/pocket-service/tree/master/userscripts)

### Описание скриптов:
1) [conductor_deployment_ticket.user.js](https://github.yandex-team.ru/passport/pocket-service/raw/master/userscripts/conductor_deployment_ticket.user.js) - добавляет в [Кондуктор](https://c.yandex-team.ru/tickets/all) (в тикеты в нетерминальном состоянии) кнопку-ссылку "создать тикет админам". При её нажатии создастся ST-тикет на выкладку.

## Сборка и выкладка

### Сборка
``` ya package ./deb/yandex-passport-pocket-service.json```

### Выкладка
Настроены релизы [stage](https://deploy.yandex-team.ru/stage/passport-pocket-service-stable) в Deploy
через [CI процесс](https://a.yandex-team.ru/ci/passp/releases/timeline?dir=passport%2Fpython%2Fpocket_service&id=passport-pocket-service-release).

Параметры процесса выкладки описаны в `a.yaml`.
