# Разработка /canary.

## Устройство

В `index.js` мы указываем, какие запросы мы обрабатываем.
Далее используем обработчик из папки `/routes/`.

## Подготовка
Чтобы собрать версию с вашими изменениями, необходим [docker](https://store.docker.com/editions/community/docker-ce-desktop-mac).

## Разработка

## Тестирование
### Unit тесты

Мы использует mocha и пишем тесты на все важные изменения.
Можно подглядывать в любой доступный тест, например, мне нравится вот [этот](./lib/create-release-task.test.js).

Мокаем модули через proxyquire.

### Тестирование контейнера

1. Соберите и опубликуйте тестовый образ.
1. Загрузите в тестовое [окружение](https://qloud.yandex-team.ru/projects/lego/hoolistener/testing)
1. У компонента `canary-listener` надо нажать `update`
1. В модальном окне выбрать нужный тег
1. Опубликовать
1. Дождаться деплоя
1. Начать тестировать.

Ручки будут доступы по адресу: `https://hoolistener.testing.common-int.yandex-team.ru/v1/`
Можно дергать нужные запросы через CURL, или подключить этот хук в тестовый репозиторий и работать через Github.

## Дебаг

Большинство проблем видно на радарах [логов](https://qloud.yandex-team.ru/projects/lego/hoolistener/production?tab=logs-beta&tz=-180)
Если известен номер ПР, то можно написать его в поле ввода и получить нужную информацию.
Как правило, будет выведено сообщение об ошибке с нужным стектрейсом и дальше можно уже понять, где и что чинить.

## Публикация
Перед публикацией:
- Обновите `package.json` (руками или `npm version <patch|minor|major>`)
- `npm i` для того, чтобы обновить `package-lock`

Основные команды:

```
npm run docker-build # собирает образ
npm run docker-push # пушит образ в яндексовый реестр

npm run docker-test-build # собирает тестовый образ
npm run docker-test-push # пушит тестовый образ в яндексовый реестр
```

После публикации необходимо обновить контейнер в [`qloud`](https://qloud.yandex-team.ru/projects/lego/hoolistener).


## Другое
[Про `docker` на `Wiki`](https://wiki.yandex-team.ru/qloud/docker-registry/)

[Видео с Лего воркшопа](https://s82myt.storage.yandex.net/rvideo-nda/U2FsdGVkX18lslgPVREJLifr46eRwVtfC8vpuOem3-pmZnJSLdYmYOXZtA-0ll7t2xRkEJLChAtgjYA2uEFcvQtHnBTOgVFvyhRKQcacTwE?ts=000597567daad357&sign=b81baa4b4276d994c4acdbd3b99089edf3df246c7613ff20ea29176a402c36bd)