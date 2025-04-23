## Сборка и выкладка новой версии образа
### С помощью Sandbox
Версию образа именуем в формате `{PUPPETEER_VERSIN}-{NODE_VERSION}-{UBUNTU_VERSION}-{COMMIT_HASH}`, например `metrika/frontend/puppeteer:1.3.0-12.19.0-bionic-d80b869`

Клонировать [`задачу`](https://sandbox.yandex-team.ru/task/819990434/view) и подправить параметры:
- `Description` - исправить версию puppeteer, nodejs и хеш коммита
- `Commit` - хеш коммита
- `Tags to publish image with` - исправить версию puppeteer, nodejs и хеш коммита. можно целиком скопировать из `Description`

### Сборка локально
```(bash)
$ docker build --network=host -t puppeteer_test -f nodejs.dockerfile .
```
