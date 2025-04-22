[![Build Status](https://teamcity.taxi.yandex-team.ru/app/rest/builds/buildType:(id:Ekbinfra_Taxi_AmberCheck)/statusIcon)](https://teamcity.taxi.yandex-team.ru/viewType.html?buildTypeId=Ekbinfra_Taxi_AmberCheck)
[![Build Status](https://teamcity.taxi.yandex-team.ru/app/rest/builds/buildType:(id:Ekbinfra_Taxi_AmberCheckSaveReferences)/statusIcon)](https://teamcity.taxi.yandex-team.ru/viewType.html?buildTypeId=Ekbinfra_Taxi_AmberCheckSaveReferences)

# amber-blocks

Библиотека интерфейсных компонентов

* [Элементы](https://github.yandex-team.ru/pages/Heist/TaxiSpec/Amber/)
* [Палитра](https://github.yandex-team.ru/pages/kovchiy/taxi/projects/book/pages/index.html#!/all)

## Как добавить примеры работы блока

Создаем Readme.md файл в папке блока.
Добавляем примеры в формате Markdown:

Button
```jsx
<Button theme="fill">
    Кнопка
</Button>
```

Props подтягиваются автоматически. Добавить описание для нужного props можно в формате JSdoc:
```js
/** Темы кнопок */
theme?: ButtonTheme;
```

Блоки без документации, не подтягиваются в коды примеров, их можно добавить в пример вручную:
```js
const Location = require('../icon/Location').default;
```
Например компоненты иконок не имеют документации, так как это лишь svg иконки.

## Сборка документации для gh-pages
    npm run doc
    (npx styleguidist build && cd gh-pages && git init && git checkout -b gh-pages && git add . && git commit -m \"documentation\" && git remote add origin git@github.yandex-team.ru:taxi/amber-blocks.git && git push origin gh-pages -f)

## Запуск сервера Styleguidist документации
    npm run guide

## Публикация npm пакета
    npm run release

## Подготовка к использованию
Нужно подключить сброс стилей и шрифты
```
amber-blocks/stylus/clear.styl
amber-blocks/font/font.styl
```

Так же можно подключить файл с переменными
```
amber-blocks/stylus/variables.styl
```

## Тестировние
На пулркевесты запускаются тесты. В качестве артефактов можно увидеть отчет о регрессии.

Для обновления рефернсных скриншотов запустите в CI [Ekbinfra_Taxi_AmberCheckSaveReferences](https://teamcity.taxi.yandex-team.ru/viewType.html?buildTypeId=Ekbinfra_Taxi_AmberCheckSaveReferences) билд

### Регрессия при локальной разработке
Перед началом работы, рекомендую сделать референсные скришноты текущего состояния

`npm run backstop:reference`

После этого, можете смело разрабатывать. Для проверки регрессии выполните

`npm run test:backstop` 
