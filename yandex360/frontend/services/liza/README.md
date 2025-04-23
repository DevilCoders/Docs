[![oko health](https://oko.yandex-team.ru/badges/repo.svg?repoName=yandex360/frontend/services/liza&vcs=arc)](https://oko.yandex-team.ru/arc/yandex360/frontend/services/liza)
[![oko health](https://oko.yandex-team.ru/badges/repoSecurity.svg?repoName=yandex360/frontend/services/liza&vcs=arc)](https://oko.yandex-team.ru/arc/yandex360/frontend/services/liza)

# Liza

Репозиторий интерфейса - https://mail.yandex.ru/u2709/
Очередь в стартреке - https://st.yandex-team.ru/DARIA/

![Liza](https://avatars.mds.yandex.net/get-bunker/61205/ebe4e3c1966cbf13161c7d17b2de80297ac81abd/orig)

## Разработка

Используй qyp (см. [dev-playbooks](../../tools/qyp)).

Для установки зависимостей нужен `npm@6.9.0` или выше.
```sh
git clone git@github.yandex-team.ru:personal-services/frontend.git ~/www
cd ~/www/services/liza
npm run prepare-dev
npm start
```

**Важное замечание:**
Если первый запуск команды `npm start` упал (сервер отдаёт 5xx ошибку), нужно запустить эту команду ещё раз. Проблема состоит в том, что, из-за ассинхронной сборки сервера и клиента, что-то где-то внутри не смогло корректно прорасти. При втором запуске, такой проблемы не будет.

Для запуска в корп-режиме можно использовать
```sh
npm run start-corp
```

Если возникают ошибки, связанные с SSH Agent, можно попробовать:
```sh
eval `ssh-agent -s`
```

Подробно про запуск можно почитать [здесь](https://wiki.yandex-team.ru/users/cosmopanda/HowToMakeLiza/).

## Debug
Для отладки рендера компонентов подключен [Why did you render](https://github.com/welldone-software/why-did-you-render)

По-умолчанию ничего не логируется.
Для управления логированием конкретного компонента, нужно указать ему свойство `whyDidYouRender` [инструкция](https://github.com/welldone-software/why-did-you-render#tracking-components)
Чтобы включить логирование всех pure/memo компонентов, достаточно добавить url-параметр `?trackAllPureComponents=1`


```js
class ClassComponent extends React.Component {
  static whyDidYouRender = true
  // ...
}

const FunctionComponent = props => <div/>;
FunctionComponent.whyDidYouRender = true
```


## Документация
 0. [Правила создания релиза в Лизе](https://github.yandex-team.ru/Daria/liza/wiki/Правила-выкатки-релизов-в-Лизе)
 1. [Codestyle](docs/codestyle.md)
 2. [Модули или как у нас разделен код](docs/modules.md)
 2. [Про ревью](docs/review.md)
 3. [Как грепать ошибки после релиза](docs/duty-release-errors.md)
 4. [Миграция на web-api](docs/web-api-migration.md)
 5. [Соглашения по разработке](docs/code-liza-convention.md)
 6. [Сборка релиза и выкатка](docs/release.md)
 7. [Локализация](docs/l10n.md)

### Советы
 3. [Полезные советы про yate](https://github.yandex-team.ru/Daria/codestyle/blob/master/yate.md)
 5. [Что надо знать про mid и tid](docs/mid-tid.md)
 5. [Как подготавливать данные для браузера](docs/data-prepare.md)

### Компоненты
 1. [Состояние композа](mail/modules/compose2/models/doc/compose-fsm.md)
 2. [Единый скроллер](mail/modules/mail/models/scroller-common.md)
 3. [Тулбар](docs/toolbar.md)
 3. [Список yate-функций](docs/yate-functions.md)

### Тестирование
 1. [Тесты](docs/testing.md)

## Технологии и плагины

Общие плагины:
 1. [es5-shim](https://github.com/es-shims/es5-shim). Чтобы свободно использовать все методы стандартных объектов.
 2. [Lo-Dash](http://lodash.com/). Набор полезных функций.
 3. [Modernizr](http://modernizr.com/). Для определения возможностей браузера.

Технологии, фреймворки:
 1. [vow @0.4](https://github.com/dfilatov/vow/blob/master/README.md). Реализация Promise.
 Они приезжают из noscript и имеено их стоит использовать (не надо использовать `jQuery.Deferred`), т.к. более точно реализует стандарт. В исключительных случаях (например, если нужен `abort` - прерывание ожидания промиса из вне) допускается использование `vow.Deferred`.
 В будущем, когда будет переезд на нативные [Promise](https://developer.mozilla.org/cs/docs/Web/JavaScript/Reference/Global_Objects/Promise), это нам поможет.
 1. [yate](https://github.com/pasaran/yate). Шаблонизация в браузере.
 2. [noscript](https://github.com/yandex-ui/noscript). MVC фреймворк.

Для noscript:
 1. [noscript-bosphorus](https://github.com/yandex-ui/noscript-bosphorus). Позволяет из yate вызывать методы вида.
 1. [noscript-hash](https://github.com/yandex-ui/noscript-hash). Позволяет работать с хеш-урлами, вместо стандартного обработчика History API из ns.
 3. [ns-view-edefine](https://github.com/doochik/noscript-view-edefine) Расширенный define для ns.View

Для yate:
 1. [yate-stdlib](https://github.com/yandex-ui/yate-stdlib). Реализация общих external-функция в yate.

## Ссылка на внутрение API
 1. [Новый wmi на порту 9090](https://wiki.yandex-team.ru/users/jkennedy/ywmiapi)
 2. [Коды wmi-ошибок](https://wiki.yandex-team.ru/Pochta/ErrorCodes)
 3. [Типы писем](https://wiki.yandex-team.ru/pochta/types/status)
 4. [Битовые флаги IS_MIXED](https://wiki.yandex-team.ru/%D0%91%D0%B8%D1%82%D0%BE%D0%B2%D1%8B%D0%B5%D0%A4%D0%BB%D0%B0%D0%B3%D0%B8ISMIXED)

## Структура репозитария

* `mail` - статика. Раскатывается на кластер (оно же CDN) `yastatic.net` и отвечает по урлу `yastatic.net/mail/u2709/`
* `u2709` - динамика. Раскатывается на кластер `%mail_web` и отвечает по урлу `mail.yandex.ru/u2709/`
  * в корне хранится все куда может прийти пользователь
  * в `/api` хранится все, куда мы ходим AJAX'ом
