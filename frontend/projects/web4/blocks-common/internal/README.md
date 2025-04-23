# Кука релевантности
#### Ответственный: -
##### Знатоки: [Сергей Сергеев](https://staff.yandex-team.ru/gurugray), [Леонид Федоров](https://staff.yandex-team.ru/lagrunge)

#### Тестирование

Локальное тестирование на живых данных:

```bash
RELEV_COOKIE=XXX PLATFORM=desktop ./node_modules/.bin/hermione features/common/relev-cookie/relev-cookie.hermione.js
```

Сбор свежих  дампов:
```bash
RELEV_COOKIE=XXX PLATFORM=desktop ./node_modules/.bin/hermione features/common/relev-cookie/relev-cookie.hermione.js --save
```

Где `XXX` содержимое куки `yp`. У вас должна быть включена кука релевантности с помощью одного из сервисов, указанных на [вики](https://wiki.yandex-team.ru/jandekspoisk/panelupravlenija/pravilakuki/#vjuerykukirelevantnosti), например [cookie.serp.yandex.ru](https://cookie.serp.yandex.ru/superman_cookie/)

Для доступа достаточно запросить роль в https://idm.yandex-team.ru  роль «Управление группами / Kuka / Участник»

Для прогона тестов локально на текущих стабах достаточно такого запуска:

```bash
PLATFORM=desktop ./node_modules/.bin/hermione features/common/relev-cookie/relev-cookie.hermione.js --play
```
