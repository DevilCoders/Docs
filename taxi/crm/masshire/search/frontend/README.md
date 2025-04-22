# Тестовый UI для модуля поиска

## Особенности работы с TVM

### Общие ссылки

Про [User-тикеты][link1].

Про [`tvmtool`][link2].

Про [отладку и `tvmknife`][link3].

[link1]: https://wiki.yandex-team.ru/passport/tvm2/user-ticket/
[link2]: https://wiki.yandex-team.ru/passport/tvm2/tvm-daemon
[link3]: https://wiki.yandex-team.ru/passport/tvm2/debug/

### Особенности работы

Для локальной разработки:

* поднимаем `tvmtool` с флагом `--unittest`
* в IDEA в переменные окружения прописываем `TVMTOOL_LOCAL_AUTHTOKEN` из предыдущего шага
* выписываем "вечный" User-тикет через `tvmknife` и его режим `unittest`
* в `envoy.yaml` прописываем тикет в секцию с [добавлением заголовка][tvm1] `x-ya-user-ticket`
* аналогично добавляем "вечный" Service-тикет
* поднимаем локальный UI, который смотрит в локальный `envoy`

После этого всё должно заработать.

Для работы UI с тестингом/продом схема примерно та же самая, но есть особенность выписывания тикетов:

* выписывать "честные" User-тикеты с походом в blackbox мы не можем, нам это не нужно в проде, поэтому у нас нет нужных грантов
* User-тикеты могут выписывать только TVM ssh-пользователи в [ABC][tvm2]
* выписывать UserTicket можно или в обмен на SSH (нужно быть залогиненным), либо в обмен на OAuth (действует сутки)
* User-тикет выписываются через `tvmknife`
* User-тикет живёт пять минут, вечный выписать не получится

Поэтому схему для локальной разработки нужно модифицировать так, чтобы раз в несколько минут получать настоящий User-тикет/Service-тикет через `tvmknife`, прописывать его в `envoy.yaml` и перезапускать `envoy`.

[tvm1]: https://www.envoyproxy.io/docs/envoy/latest/configuration/http/http_conn_man/headers#custom-request-response-headers
[tvm2]: https://abc.yandex-team.ru/services/taxisupportmasshiresearch/

### Получение tvmtool

Для Mac OS X можно взять `tvmtool` из pip:

```
pip install --user tvmtool-bin -i https://pypi.yandex-team.ru/simple
```

Для Linux можно взять бинарник по [инструкции][tvmtool1].

[tvmtool1]: https://wiki.yandex-team.ru/passport/tvm2/tvm-daemon/#gdeskachatbinarnik

## Available Scripts

In the project directory, you can run:

### `npm start`

Runs the app in the development mode.\
Open [http://localhost:3000](http://localhost:3000) to view it in the browser.

The page will reload if you make edits.\
You will also see any lint errors in the console.

### `npm test`

Launches the test runner in the interactive watch mode.\
See the section about [running tests](https://facebook.github.io/create-react-app/docs/running-tests) for more information.

### `npm run build`

Builds the app for production to the `build` folder.\
It correctly bundles React in production mode and optimizes the build for the best performance.

The build is minified and the filenames include the hashes.\
Your app is ready to be deployed!

See the section about [deployment](https://facebook.github.io/create-react-app/docs/deployment) for more information.
