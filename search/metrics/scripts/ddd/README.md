# ddd

tl;dr:

![ddd demo](https://jing.yandex-team.ru/files/leshapak/ddd_demo.gif)

Утилита облегчает обновление tag'а Docker-образа компоненты в Deploy. Можно изменить один тэг. Внутри утилита вызывает [dctl](https://deploy.yandex-team.ru/docs/tools/dctl) (из `ya tool`) через shell.

Нужен Python 3.6+ и [ya](https://wiki.yandex-team.ru/yatool/), зависимости см. в `requirements.txt`.

## Использование

[Токен доступа к Docker registry](https://wiki.yandex-team.ru/qloud/docker-registry/#authorization) должен быть доступен в переменной окружения `REGISTRY_TOKEN` (также Поддерживается `.env`).

```bash
./ddd.py <stage_name>
```

Пропатченные конфигурации можно посмотреть в директории `./configs`.

По ключу `--help` доступна встроенная справка.

## TODO

* Добавить `setup.py`
* Поддержать redeploy
* Поддержать обновление нескольких box'ов (?)
* Написать тесты
