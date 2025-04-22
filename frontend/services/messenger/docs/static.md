# Статика в Коннекте

## Как работает раздача статики

Статика собирается вместе с докер образом.
Для раздачи статики поднято отдельное окружение в [Qloud](https://qloud-ext.yandex-team.ru/projects/workspace/yamb-web/static).
Статика выкладывается с помощью утилиты [just-static](https://wiki.yandex-team.ru/users/unikoid/just-static/).

## Настройка just-static

Вначале нужно получить токены для [QLOUD](https://oauth.yandex-team.ru/authorize?response_type=token&client_id=75ce16e5643a43feb5d1b1d6f82c2e45)
и [SANDBOX](https://oauth.yandex-team.ru/authorize?response_type=token&client_id=b662b483feff40c1832e42cc1fcbc500).
Затем добавляем полученные значения в переменные окружения QLOUD_TOKEN и SANDBOX_TOKEN.
Например можно добавить их в `.bash_profile` для мака или в `.bashrc` для убунту или дебиана.
```
export QLOUD_TOKEN=<token>
export SANDBOX_TOKEN=<token>
```
Потом нужно глобально поставить npm пакет
```
npm i -g --registry http://npm.yandex-team.ru just-static
```
