# vertis-frontend
Репа для общих библиотек фронтенда, 1 папка - 1 пакет

## lerna

В монорепе ипользовалась [lerna](https://lerna.js.org), но с аркадией она не ужилась 💀

## как опубликовать пакет

* Для начала надо убедится, что мы залогинены в яндексовом npm  
    * команда `npm whoami --registry https://npm.yandex-team.ru`
    * если мы не залогинены, то логинемся по этой [доке](https://doc.yandex-team.ru/si-infra/npm/npm.html#autentifikatsiia-cherez-pasport)
* Не забываем в `package.json` у пакета апнуть версию, делаем PR
* Запрашиваем права на публикацию пакета, [пример](https://idm.yandex-team.ru/user/stormtrooper/roles?page=8#rf=1,rf-role=nW0wNMAW#user:stormtrooper@npm/packages/vertis/ads/maintainer(fields:();params:()),f-status=all,sort-by=-updated,f-ownership=personal,rf-expanded=nW0wNMAW) 
* Ждем зеленый CI
* Делаем `npm publish <package-path>`
