# islands

Данная версия временно зафрижена для сервиса Вебмастер

Общая библиотека блоков [Лего](https://lego.yandex-team.ru/).


## Обратная связь

  * Клуб: https://clubs.at.yandex-team.ru/lego/
  * Трекер: [https://st.yandex-team.ru/ISL](https://st.yandex-team.ru/createTicket?queue=ISL)
  * Рассылка: [lego@yandex-team.ru](http://ml.yandex-team.ru/lists/lego/)


## Организационное

  * [Contribution Guide](https://lego.yandex-team.ru/doc/guidelines/contribute/)
  * [Оформление кода](https://lego.yandex-team.ru/doc/codestyle/)
  * [Оформление unit-тестов](https://lego.yandex-team.ru/doc/practics/unit-tests/)


## Документация

  * Документация, примеры и changelog:
  <br> https://lego.yandex-team.ru/libs/islands/
  * Свежая сборка ветки __dev__:
  <br> https://lego-staging.dev.yandex-team.ru/islands/dev/

## Миграция

Руководство по миграции [islands 3.х → 4.х](https://github.yandex-team.ru/lego/islands/blob/dev/releases/4.0.0-migration.md)


## Надежность

Мы уделяем огромное внимание вопросам надежности библиотеки `islands`.
Для этого каждое изменение кода оформляется как Pull Request, который проходит:
- Обязательное code review со стороны других разработчиков.
- Полный цикл проверок автоматическими тестами, которые включают в себя:
  - Unit-тесты на JS
  - Тесты шаблонов
  - Функциональное тестирование верстки скриншотами ([gemini])
- Ручное тестирование.

Особое внимание мы уделяем тестированию релизов.

В библиотеке ведется подробный changelog, а примечания к релизу готовятся инкрементально.
Это означает, что примечание к релизу в отношении конкретной задачи составляется непосредственно
в процессе работы, их пишет тот кто вносил изменения и лучше понимает смысл произошедшего.

Использование блоков из библиотеки `islands` позволяет минимальными усилиями повысить
надежность кодовой базы сервиса.

[gemini]: https://github.com/gemini-testing/gemini

### Периодичность выпуска версий

Минорные версии библиотеки `islands` выпускаются __1 раз в две недели__, по пятницам.
Мажорные версии библиотеки `islands` выпускаются __1 раз в полгода__, весной и осенью.


## Подключение и обновление

### Через `npm` (рекомендуемый способ)
Укажите внутренний npm-репозиторий `https://npm.yandex-team.ru` в файле `.npmrc` в корне проекта, для сокращения команды установки библиотеки:
```
registry=http://npm.yandex-team.ru
```

Чтобы подключить или обновить библиотеку на проекте, выполните команду в его корневой директории:

```sh
npm install --save "islands@5.0.0"
```

**NB** Обратите внимание, что в npm-пакет библиотеки `islands` не входит `tableau-iframe`, который необходим для работы `tableau-node` и `header2_tableau_yes`.

Пример реального проекта: [staff-www](https://github.yandex-team.ru/tools/staff-www).

### Через `bower` (устаревший способ)
Укажите внутренний npm-репозиторий `https://npm.yandex-team.ru` в файле `.bowerrc` в корне проекта, для сокращения команды установки библиотеки:

```json
{
  "shorthand-resolver": "git://github.yandex-team.ru/{{owner}}/{{package}}.git"
}
```

Чтобы подключить или обновить библиотеку `islands` на проекте, выполните команду в его корневой директории:

```sh
bower install --save "lego/islands#v5.0.0"
```

### Примечания
Если для установки библиотеки `github.yandex-team.ru` недоступен, то можно использовать [зеркало репозитория](https://git.yandex-team.ru/gitweb/lego/islands.git), расположенное на хосте `git.yandex-team.ru`.

### Настройка фриза статических файлов

Для преобразования ссылок (`background-image: url("path/to/file")`) на статические ресурсы из CSS,
вы можете использовать утилиту [borschik](https://github.com/borschik/borschik) (как отдельно, так и в составе [enb-borschik](https://github.com/enb/enb-borschik)).

Библиотека `islands` не содержит конфигурационных файлов сборки `.borschik`, предназначенных для использования на сервисе.
Но все статические файлы библиотеки, кроме CSS и JS, при каждом релизе [замораживаются](https://github.com/bem/bem-method/blob/bem-info-data/articles/borschik/borschik.ru.md#css-freeze)
и копируются на статический кластер. Файлы доступны по URL вида https://yastatic.net/islands/_/4me0iliC4OKERBOBlRoFzs6cj2k.png

В конфигурационном файле `.borschik`, расположенном в корне проекта,
можно описать следующие специфические правила преобразования относительных ссылок на статические ресурсы:
* В абсолютные или другие относительные (`image.png` → `https://service.yastatic.net/islands/`).
* В data URI с содержимым файла.
* В хеши (фризовые имена) от содержимого файла.
Алгоритм хеширования можно посмотреть [в исходных файлах](https://github.com/borschik/borschik/blob/v1.6.0/lib/freeze.js#L70-L94).

Пример конфигурационного файла `.borschik`:

```json
{
  "freeze_paths": {
    "*.blocks/**/*.{png,gif,ttf,eot,woff,woff2,swf}": ":base64:",
    "*.blocks/**/*.svg": ":encodeURIComponent:",
    "libs/islands/**": "islands_freeze"
  },
  "paths": {
    "islands_freeze": "https://yastatic.net/islands/_/"
  }
}
```

Приведенный пример выполняет следующие настройки:
* Ссылки на бинарные файлы (изображения, шрифты, flash) преобразуются в data URI с использованием base64.
* Ссылки на изображения SVG преобразуются в data URI с использованием `encodeURIComponent()`.
* Файлы из `islands`, на которые есть ссылки, копируются с фризовыми именами в папку islands_freeze.
* Ссылки на файлы с фризовыми именами указываются относительно пути `/islands/_/` на статическом кластере.

Если вы используете `borschik`, мы рекомендуем использовать фриз статических файлов `islands` (последние два пункта).
Это позволит более эффективно использовать клиентское кэширование (общий кэш между разными проектами использующими `islands`).

Другие примеры:
[islands-components](https://github.yandex-team.ru/lego/islands-components/blob/v3.10.0/.borschik),
[brickbox](https://github.yandex-team.ru/lego/brickbox/blob/master/.borschik),
[web4](https://github.yandex-team.ru/serp/web4/blob/44c08abe3250cdb304c7de6797dfec19f47d0199/configs/production/borschik.json).

Подробнее про [borschik] и [enb-borschik] можно почитать в документации соответствующих пакетов и в
[статье](https://github.com/bem/bem-method/blob/bem-info-data/articles/borschik/borschik.ru.md) со старой версии сайта bem.info.

[borschik]: https://github.com/borschik/borschik
[enb-borschik]: https://github.com/enb/enb-borschik

### Настройка .enb/make.js

* Замените `enb-bemhtml` на [enb-bemxjst](https://github.com/enb/enb-bemxjst) версии не ниже версии `6.5.3`.
* Обновите `enb` до версии не ниже версии `0.15.0`.
* Настройте `config.nodes()`, указав уровни переопределения библиотек. См. ниже. [Документация enb](https://github.com/enb/enb/blob/master/README.md).

>NB: Обратите внимание, что в данный момент библиотека не поддерживает `bem-xjst` версии `8.0.0` и выше.

### Установка tanker-kit

`tanker-kit` — это утилита для работы с сервисом переводов [Яндекс.Танкер](https://doc.yandex-team.ru/Tanker/tech-dscr/concepts/tanker-description.xml). Она позволяет:

- выгрузить локализационные ключи из исходных файлов;
- загрузить, выгрузить данные в/из Танкера;
- синхронизировать данные с Танкером.

Установите пакет:

```
npm i tanker-kit
```

Чтобы выгрузить переводы из Танкера в корне проекта, выполните команду:

```
./node_modules/.bin/tanker pull
```

Подробнее об использовании `tanker-kit` читайте в [документации](https://github.yandex-team.ru/lego/tanker-kit/blob/dev/doc/overview.md).

### Уровни переопределения

Платформа **desktop**:
* `libs/islands/common.blocks`
* `libs/islands/desktop.blocks`

Платформа **touch-pad**:
* `libs/islands/common.blocks`
* `libs/islands/touch.blocks`
* `libs/islands/touch-pad.blocks`

Платформа **touch-phone**:
* `libs/islands/common.blocks`
* `libs/islands/touch.blocks`
* `libs/islands/touch-phone.blocks`

Пример использования в конфигурации `enb` на сервисе:
```js
var islands = require('./libs/islands');

module.exports = function(config) {
    config.nodes('*.bundles/*', function(nodeConfig) {
        var projectLevels = ['common.blocks', 'desktop.blocks'];
        nodeConfig.addTech([
            require('enb/techs/levels'),
            {levels: islands.getPlatformLevels('desktop').concat(projectLevels)}
        ]);
    });
};
```

См. [конфигурацию проектов Картинки и Видео](https://github.yandex-team.ru/mm-interfaces/fiji/blob/dev/.enb/levels.js).


## Работа с событиями

Один из принципов разработки блоков в библиотеке `islands` – __кроссплатформенность__.

Чтобы следовать этому принципу, для работы с событиями мы используем унифицированную модель [Pointer Events].
Реализация pointer-событий находится в блоке `pointerevents` и представляет из себя
существенно переработанный полифилл [PEP], работающий поверх событийной модели jQuery.

[PEP]: https://github.com/jquery/PEP
[Pointer Events]: http://www.w3.org/TR/pointerevents/

## Сообщения об ошибках

Чтобы упростить обновление библиотеки `islands`, начиная с версии 4.6.0, в код шаблонов и клиентского JS мы стали добавлять конструкции вида `/*%%%ISLDEBUG%%%*/0 && console.assert(...)`. Они предоставляют возможность вывести в консоль следующие сообщения об ошибках:

* про использование устаревших или приватных методов;
* о неправильном использовании [контракта метода](https://ru.wikipedia.org/wiki/%D0%9A%D0%BE%D0%BD%D1%82%D1%80%D0%B0%D0%BA%D1%82%D0%BD%D0%BE%D0%B5_%D0%BF%D1%80%D0%BE%D0%B3%D1%80%D0%B0%D0%BC%D0%BC%D0%B8%D1%80%D0%BE%D0%B2%D0%B0%D0%BD%D0%B8%D0%B5#.D0.9E.D0.BF.D0.B8.D1.81.D0.B0.D0.BD.D0.B8.D0.B5);
* про изменения в API, которые ожидаются в следующей мажорной версии.

По умолчанию эти конструкции не отображают сообщения и вырезаются при оптимизации JS. Чтобы «включить» вывод сообщений, нужно для сборки в режиме development инвертировать условие конструкции (заменить `/*%%%ISLDEBUG%%%*/0` на `!0`). Например, это можно сделать с помощью пакета [enb-define](https://github.com/tadatuta/enb-define) из `enb` следующим образом:

```javascript
nodeConfig.addTechs([
  [require('enb-define/techs/define'), {
    target: '?.js',
    source: ['?.pre.js'],
    variables: {
      ISLDEBUG: '*/!/*'
    }
  }]
]);
```

Обратите внимание, что `console.assert()` в node.js завершает сборку с ошибкой. Если вас это не устраивает, [подмените](https://github.com/zxqfox/console-assert) `console.assert` .

## Прочее

Различные инструкции и руководства можно найти на [сайте Лего](https://lego.yandex-team.ru/doc/guidelines/).
В частности, там доступны [инструкции по сборке примеров, документации и запуску тестов](https://lego.yandex-team.ru/doc/guidelines/islands-readme/).
