# Скрипты для заполнения таблиц

Данные выгружаются в инстанс [fei.infra](https://wiki.yandex-team.ru/search-interfaces/infra/charts/#obshhajainformacija)

Все скрипты используют переменные среды `CH_USER` и `CH_PASSWD`. Логин и пароль для доступа можно взять в [секретнице](https://yav.yandex-team.ru/secret/sec-01dn2bvx4303h4h8azp3evfzh7/explore/versions)

Более детальная инфа по каждому скрипту в самом скрипте в `src`.

## Install & Run

1. `npm i`
2. `npm run build`
3. `node ./build/<script>.js`
