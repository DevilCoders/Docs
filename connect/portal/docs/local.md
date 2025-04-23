
## Установка Портала на локальной машине

- склонировать копию из репозитория и установить связанные пакеты

```
// $ cd /Users/<user>/<projects>/<yandex-directory>
$ git clone git@github.yandex-team.ru:yandex-directory/www.git
$ cd www
$ npm install
```

- настроить [локальный конфиг](get-local-config.md)

- запустить локальный сервер

```
$ npm start
```

- настроить авторизацию через Паспорт или локальный конфиг и открыть Портал

&nbsp;


#### Настройка локального хоста для работы с Паспортом

- добавить хост в домене `*.yandex.ru` в `/etc/hosts`, чтобы соответствовать домену кук авторизации

```
127.0.0.1 localhost dev-portal.ws.yandex.ru
```

- установить [devd](https://github.com/cortesi/devd)

```
$ brew update
$ brew install devd
```

- запустить devd

```
$ devd --tls http://localhost:3000
> Listening on https://devd.io:8001 (127.0.0.1:8001)
```

- авторизоваться в [Паспорте](https://passport-test.yandex.ru/), используя либо один из [общих тестовых аккаунтов](https://wiki.yandex-team.ru/ws/envs/testing/#testovyeorganizaciivpassport-test.yandex.ru), либо [аккаунт собственной тестовой организации](https://api.test.directory.yandex.ru/landing/)

- открыть в браузере [https://dev-portal.ws.yandex.ru:8001/](https://dev-portal.ws.yandex.ru:8001/)


#### Альтернативная настройка локального хоста для работы с Паспортом

- установить утилиту [magicdev](https://github.yandex-team.ru/toolbox/magicdev)

```
npm install -g magicdev --registry https://npm.yandex-team.ru
```

- запустить dev-сервер (возможно, попросит ввести пароль от учетной записи)

```
npm run dev
```

- зайти на https://localhost.msup.yandex.ru:8443

Также magicdev умеет работать с хостами вида `localhost.msup.yandex(-team)?.(ru|ua|kz|by|com|com.tr|com.ua|net)`.




