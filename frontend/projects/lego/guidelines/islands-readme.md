## Содержание документа

  - [Документация, Changelog, Staging](#%D0%94%D0%BE%D0%BA%D1%83%D0%BC%D0%B5%D0%BD%D1%82%D0%B0%D1%86%D0%B8%D1%8F-changelog-staging)
  - [Локализация](#%D0%9B%D0%BE%D0%BA%D0%B0%D0%BB%D0%B8%D0%B7%D0%B0%D1%86%D0%B8%D1%8F)
  - [Сборка](#%D0%A1%D0%B1%D0%BE%D1%80%D0%BA%D0%B0)
    - [Установка зависимостей](#%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%BA%D0%B0-%D0%B7%D0%B0%D0%B2%D0%B8%D1%81%D0%B8%D0%BC%D0%BE%D1%81%D1%82%D0%B5%D0%B9)
    - [Сборка примеров](#%D0%A1%D0%B1%D0%BE%D1%80%D0%BA%D0%B0-%D0%BF%D1%80%D0%B8%D0%BC%D0%B5%D1%80%D0%BE%D0%B2)
    - [Сборка документации](#%D0%A1%D0%B1%D0%BE%D1%80%D0%BA%D0%B0-%D0%B4%D0%BE%D0%BA%D1%83%D0%BC%D0%B5%D0%BD%D1%82%D0%B0%D1%86%D0%B8%D0%B8)
    - [Сборка и запуск unit-тестов](#%D0%A1%D0%B1%D0%BE%D1%80%D0%BA%D0%B0-%D0%B8-%D0%B7%D0%B0%D0%BF%D1%83%D1%81%D0%BA-unit-%D1%82%D0%B5%D1%81%D1%82%D0%BE%D0%B2)
    - [Сборка и запуск тестов для шаблонов](#%D0%A1%D0%B1%D0%BE%D1%80%D0%BA%D0%B0-%D0%B8-%D0%B7%D0%B0%D0%BF%D1%83%D1%81%D0%BA-%D1%82%D0%B5%D1%81%D1%82%D0%BE%D0%B2-%D0%B4%D0%BB%D1%8F-%D1%88%D0%B0%D0%B1%D0%BB%D0%BE%D0%BD%D0%BE%D0%B2)
  - [Организационные вопросы](#%D0%9E%D0%B3%D1%80%D0%B0%D0%BD%D0%B8%D0%B7%D0%B0%D1%86%D0%B8%D0%BE%D0%BD%D0%BD%D1%8B%D0%B5-%D0%B2%D0%BE%D0%BF%D1%80%D0%BE%D1%81%D1%8B)
    - [Обратная связь](#%D0%9E%D0%B1%D1%80%D0%B0%D1%82%D0%BD%D0%B0%D1%8F-%D1%81%D0%B2%D1%8F%D0%B7%D1%8C)
    - [Правила оформления и контрибьюта](#%D0%9F%D1%80%D0%B0%D0%B2%D0%B8%D0%BB%D0%B0-%D0%BE%D1%84%D0%BE%D1%80%D0%BC%D0%BB%D0%B5%D0%BD%D0%B8%D1%8F-%D0%B8-%D0%BA%D0%BE%D0%BD%D1%82%D1%80%D0%B8%D0%B1%D1%8C%D1%8E%D1%82%D0%B0)

## Документация, Changelog, Staging

<table>
  <tr>
    <td align="center" width="170"><strong>Библиотека</strong></td>
    <td align="center"><strong>ChangeLog</strong></td>
    <td align="center"><strong>Документация и примеры для последнего стабильного релиза</strong></td>
    <td align="center"><strong>Свежая сборка для ветки dev</strong></td>
  </tr>
  <tr>
    <td align="left">islands-components</td>
    <td align="center"><a href="https://github.yandex-team.ru/lego/islands-components/releases/">3.x, 2.x</a></td>
    <td align="center">
      <a href="https://lego.yandex-team.ru/libs/islands-components/v2.x/">2.x</a> |
      <a href="https://lego.yandex-team.ru/libs/islands-components/v3.x/">3.x</a>
    </td>
    <td align="center"><a href="https://lego-staging.dev.yandex-team.ru/islands-components/dev/">3.x</a></td>
  </tr>
  <tr>
    <td align="left">islands-icons</td>
    <td align="center"><a href="https://github.yandex-team.ru/lego/islands-icons/releases/">3.x, 1.x</a></td>
    <td align="center">
      <a href="https://lego.yandex-team.ru/libs/islands-icons/v1.x/">1.x</a> |
      <a href="https://lego.yandex-team.ru/libs/islands-icons/v3.x/">3.x</a>
    </td>
    <td align="center"><a href="https://lego-staging.dev.yandex-team.ru/islands-icons/dev/">3.x</a></td>
  </tr>
  <tr>
    <td align="left">islands-page</td>
    <td align="center"><a href="https://github.yandex-team.ru/lego/islands-page/releases/">3.x, 2.x</a></td>
    <td align="center">
      <a href="https://lego.yandex-team.ru/libs/islands-page/v2.x/">2.x</a> |
      <a href="https://lego.yandex-team.ru/libs/islands-page/v3.x/">3.x</a>
    </td>
    <td align="center"><a href="https://lego-staging.dev.yandex-team.ru/islands-page/dev/">3.x</a></td>
  </tr>
  <tr>
    <td align="left">islands-romochka</td>
    <td align="center"><a href="https://github.yandex-team.ru/lego/islands-romochka/releases/">3.x</a></td>
    <td align="center">
      <a href="https://lego.yandex-team.ru/libs/islands-romochka/v3.x/">3.x</a>
    </td>
    <td align="center"><a href="https://lego-staging.dev.yandex-team.ru/islands-romochka/dev/">3.x</a></td>
  </tr>
  <tr>
    <td align="left">islands-search</td>
    <td align="center"><a href="https://github.yandex-team.ru/lego/islands-search/releases/">2.x</a></td>
    <td align="center">
      <a href="https://lego.yandex-team.ru/libs/islands-search/v2.x/">2.x</a>
    </td>
    <td align="center"><a href="https://lego-staging.dev.yandex-team.ru/islands-search/support-2.x/">2.x</a></td>
  </tr>
  <tr>
    <td align="left">islands-services</td>
    <td align="center"><a href="https://github.yandex-team.ru/lego/islands-services/releases/">2.x</a></td>
    <td align="center">
      <a href="https://lego.yandex-team.ru/libs/islands-services/v2.x/">2.x</a>
    </td>
    <td align="center"><a href="https://lego-staging.dev.yandex-team.ru/islands-services/support-2.x/">2.x</a></td>
  </tr>
  <tr>
    <td align="left">islands-user</td>
    <td align="center"><a href="https://github.yandex-team.ru/lego/islands-user/releases/">3.x, 2.x</a></td>
    <td align="center">
      <a href="https://lego.yandex-team.ru/libs/islands-user/v2.x/">2.x</a> |
      <a href="https://lego.yandex-team.ru/libs/islands-user/v3.x/">3.x</a>
    </td>
    <td align="center"><a href="https://lego-staging.dev.yandex-team.ru/islands-user/support-2.x/">3.x</a></td>
  </tr>
</table>

## Локализация

Для синхронизации переводов с Танкером используется [tanker-kit](https://github.yandex-team.ru/lego/tanker-kit).<br>
Ручная правка файлов вида `block.i18n/*.js` не производится.<br>
После добавления нового ключа в исходник или необходимости выгрузить свежие переводы из Танкера, в корне проекта выполняется команда:

```sh
tanker sync
```
## Сборка

###Установка зависимостей

```sh
npm i --registry="http://npm.yandex-team.ru"
npm run deps --registry="http://npm.yandex-team.ru"
```

### Сборка примеров

#### Сборка всех примеров
```sh
npm run build
```

#### Сборка всех примеров блока `block`
```sh
enb make examples desktop.examples/block/
```

#### Сборка одного примера `example-name` блока `block`
```sh
enb make examples desktop.examples/block/example-name/
```

### Сборка документации
```sh
enb make docs
```

### Сборка и запуск <a href="unit-tests.md">unit-тестов</a>
```sh
enb make specs
```

### Сборка и запуск тестов для шаблонов

Инструменты сборки библиотек **islands** позволяют собирать и запускать тесты на BEMHTML и BH
шаблоны блоков.

Чтобы добавить тест для блока, нужно в его директории на требуемом уровне переопределения создать
каталог с названием `[имя блока].tmpl-specs`, для хранения файлов тестов.

Каждый тест состоит из пары файлов в технологиях `bemjson` и `html`. Таких пар файлов у блока
может быть несколько. Имена файлов произвольные, но они (не включая расширения) для каждого теста
должны совпадать. Например, **10-simple**.bemjson.js и **10-simple**.html.

В `bemjson`-файле находится пример для блока, в `html` – эталонный HTML-код, который должен
получиться после применения шаблона блока к bemjson-у примера.

```
desktop.blocks
    └── myblocks
        ├── myblock.bemhtml.js
        ├── myblock.bh.js
        ├── ...
        └── myblock.tmpl-specs
            ├── 10-simple.bemjson.js
            ├── 10-simple.html
            ├── 20-advanced.bemjson.js
            └── 20-advanced.html
```

Команда для сборки и запуска тестов:
`enb make tmpl-specs`

Сборка тестов на нужном уровне переопределения:
`enb make tmpl-specs desktop.tmpl-specs`

Сборка тестов только для одного блока:
`enb make tmpl-specs desktop.tmpl-specs/button`

В случае успешной сборки, тесты будут запущены с последующим выводом результатов. Если результат применения
шаблона не совпадает с эталонным `html`, то в логе будет ошибка с указанием отличий от эталона.
Полученный `html` будет сохранен в файл. Полный путь к нему можно найти в логе работы тестов рядом с
сообщением об ошибке. Если отличия от эталона получились вследствие изменений шаблона, они ожидаемы
и верны, и можно заменить эталон сохраненным файлом.

## Организационные вопросы

### Обратная связь

Обо всех вопросах и предложения пишите в рассылку [lego-dev@](http://ml.yandex-team.ru/lists/lego-dev/)
или клуб [lego-dev](http://clubs.at.yandex-team.ru/lego-dev) в Этушке.

Задачи, имеющие отношение к конкретной библиотеке блоков, заводите в соответствующей очереди:

- [islands-components](https://st.yandex-team.ru/createTicket?queue=ISLCOMPONENTS)
- [islands-icons](https://st.yandex-team.ru/createTicket?queue=ISLICONS)
- [islands-page](https://st.yandex-team.ru/createTicket?queue=ISLPAGE)
- [islands-romochka](https://st.yandex-team.ru/createTicket?queue=ISLROMOCHKA)
- [islands-search](https://st.yandex-team.ru/createTicket?queue=ISLSEARCH)
- [islands-services](https://st.yandex-team.ru/createTicket?queue=ISLSERVICES)
- [islands-user](https://st.yandex-team.ru/createTicket?queue=ISLUSER)
- [bem-bl](https://st.yandex-team.ru/createTicket?queue=BEM)
- [meccano](https://st.yandex-team.ru/createTicket?queue=MECCANO)

Задачи, имеющие отношение сразу ко всем библиотекам `islands-*`, заводите в очереди [ISL](https://st.yandex-team.ru/createTicket?queue=ISL).

Задачи про инфраструктуру для разработки библиотек заводите в очереди [LEGO](https://st.yandex-team.ru/createTicket?queue=LEGO).

### Правила оформления и контрибьюта

  * [Правила контрибьюта](https://lego.yandex-team.ru/guidelines/contribute/)
  * [Правила оформления кода](https://lego.yandex-team.ru/codestyle/)
  * [Правила оформления unit-тестов](https://lego.yandex-team.ru/guidelines/unit-tests/)

Другие правила и руководства можно найти на [сайте Лего](https://lego.yandex-team.ru/guidelines/).
