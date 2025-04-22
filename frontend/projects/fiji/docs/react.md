# React
> - Документацию можно найти: (React)[https://reactjs.org/], (bem-react-core)[https://bem.gitbooks.io/bem-react-core/en/]
>
> - Распространенные паттерны react разработки: https://reactpatterns.com/
>
> - Общая страничка про разработку на React'е в Fiji: https://wiki.yandex-team.ru/search-interfaces/multimedia/react/

## Общая информация про react стек

Кроме собственно самого реакта у нас используется некоторое количество дополнительных библиотек:
* taburet - это платформа для разработки интерфейсов, позволяет структурировать серверный и клиентский код фичей в одном месте в типизированном стиле (typescript), также позволяет заводить эксперименты над фичами (над уже существующими или добавлять новые). Документация к табурету находится в монорепе фронтенда поиска: https://github.yandex-team.ru/search-interfaces/frontend/tree/master/packages/taburet
* @bem-react/di - dependency injection для реакт компонентов. С помощью di решаются 2 основные задачи: разделение кода по платформам с выделением общей платформонезависимой части и возможность проведения эксериментов с подменой реакт компонентов их экспериментальной версией. Документация: https://ru.bem.info/technologies/bem-react/di/
* Библиотеки компонентов - @yandex-lego/components, @yandex-int/images-react-components, video-components (в видео). Документацию можно найти в https://depot.yandex-team.ru/ или в соответствующих репозиториях.
* @bem-react/core - используется для декомпозиции реакт компонентов на независимые "модификаторы" и последующей композиции этих модификаторов. Документация: https://ru.bem.info/technologies/bem-react/core/
* @yandex-int/i18n - локализация/интернационализация, документация: https://github.yandex-team.ru/search-interfaces/frontend/tree/master/packages/i18n
* @bem-react/classname - используется для формирования БЭМ-like имён классов в JSX, документация: https://ru.bem.info/technologies/bem-react/classname/

## React + Webpack

Шаблоны конфигураций для сборки серверных бандлов находятся [тут](.build/webpack.server.template.js).

Сборка клиентской статики описана [тут](docs/common/webpack-client.md)

Запуск сборки встроен в `fiji build [targets]`. Так же можно отдельно собрать бандлы на react используя команду `webpack --config=.build/webpack.config.js` передав переменные окружения `YENV={development,production} PROJECT={images,video} PLATFORM={desktop,touch-phone,...}`.

Для разработки react-фичей в режиме `development` нужно запускать темплар через команду:
`npm run dev`

или с дополнительными параметрами:
`npm run dev -- -sd`

Для обеспечения работы пересборки и Hot Module Replacement (HMR) необходимо делать запуск указанной выше команды с переменной окружения WEBPACK_HMR=1

## Динамические импорты

В любом контейнерном компоненте можно использовать динамические импорты https://webpack.js.org/guides/code-splitting/#dynamic-imports.
Однако их работа гарантируется только при импорте других контейнерных компонентов.

## Когда использовать хоки, класс-компоненты, хуки?

Хоки (HOCs) сейчас обильно используются в @bem-react/core и лего в виде withBemMod. Все модификаторы для компонентов оформляются как хоки, которые потом композируются при добавлении в реестры.
Class-компоненты стоит использовать в том случае, если необходимы lifecycle методы или если нужен стейт.
На смену class-компонентам команда реакта разработала Hooks API, которое практически полностью перекрывает функционал классов. При разработке новых фич стоит отдавать предпочтение хукам.

## Фичи и их структура

Фича (feature) - это некоторый независимый кусочек страницы сервиса, который в общем случае содержит разбитые на платформы серверный код для подготовки данных и server-side рендеринга вёрстки, клиентский кода и стили. Клиентский код и стили автоматически выносятся в отдельные бандлы и поставляются в вёрстку.

Для сервиса картинок все фичи лежат в images/src/features, для видео - в video/src/features.

Общая структура папочки фичи имеет следующий вид:

```
SomeFeature
  SomeFeature.components
    SomeFeatureComponent
  SomeFeature.entries
    desktop.ts
    touch-phone.ts
  SomeFeature.i18n
    index.ts
    ru.ts
    ...
  SomeFeature.registry
    index.ts
    desktop.ts
    touch-phone.ts
  SomeFeature.scss
  SomeFeature.server.tsx
  SomeFeature.tsx
  SomeFeature@desktop.server.ts
  SomeFeature@desktop.ts
  SomeFeature@touch-phone.server.ts
  SomeFeature@touch-phone.ts
```

- `SomeFeature.components` - содержит какие-то приватные для данной фичи реакт-компоненты.
- `SomeFeature.entries` - точки входа клиентского js, в этой папочке лежат скрипты, с которых начинается выполнение реактовой фичи на клиенте. Тут должен выполняться вызов метода createApp из 'sakhalin/src/components/Root/Root'. Для каждой платформы, где должна работать фича, заводится отдельный файл.
- `SomeFeature.i18n` - переводы, формируется автоматически с помощью тасок танкера (Нужна ссылка на доку танкера).
- `SomeFeature.registry` - реестры компонентов для фичи, см. доку к @bem-react/di по ссылочке выше.
- `SomeFeature.scss` - стили для фичи
- `SomeFeature.server.tsx` - общий серверный код фичи
- `SomeFeature.tsx` - общий клиентский код фичи, обычно здесь описан полностью весь JSX фичи
- `SomeFeature@desktop.server.ts, SomeFeature@touch-phone.server.ts` - специфичный для платформ серверный код
- `SomeFeature@desktop.ts, SomeFeature@touch-phone.ts` - специфичный для платформ клиенсткий код, тут обычно с помощью withRegistry применеются реестры (см. доку к @bem-react/di по ссылочке выше)

Готовые фичи подключаются в реестры фичей в папочках images/src/features/.registry и video/src/features/.registry.

Далее в коде можно делать вызов метода Runtime.get({ type: 'SomeFeature' }), который отрендерит и вернёт вёрстку, а также запушит ассеты.

## Экспериментальные фичи

Кроме обычных фичей ещё есть экспериментальные. Они заводятся в `images/src/experiments` или в `video/src/experiments`.
Внутри этих папочек создаётся вложенная директория с именем флага, её содержимое повторяет структуру `images/src` или `video/src` с небольшими исключениями.

Подробнее про заведение экспериментальных фичей можно почитать в документации к `taburet`.

## Часто задаваемые вопросы

### Как завести новую фичу или эксперимент?

#### Вариант 1 - вручную:
1) Нужно сформировать структуру согласно описанию выше и документации к `taburet`
2) Добавить фичу в обычный или экспериментальный реестр
3) В коде `priv` добавить вызов `Runtime.get({ type: 'SomeFeature' })`, который возвращает вёрстку и пушит статику фичи

#### Вариант 2 - с помощью консольной тулзы:
Для генерации фичей написан пошаговый генератор `fiji bootstrap-react`, почитать хелп к нему можно так: `fiji bootstrap-react --help`.

Для генерации обычной фичи нужно вызвать в консоли `fiji bootstrap-react feature` и далее ответить на несколько вопросов.
Для генерации экспериментальной фичи нужно вызвать в консоли `fiji bootstrap-react exp-feature` и далее ответить на несколько вопросов.

### Чем отличается фича от компонента?
У фичи есть серверный код, в котором могут быть запилы на окружение, например могут читаться данные из `GlobalData`.
Компонент же не имеет собственного серверного кода, должен быть относительно небольшим и не должен зависеть от окружения; для разделения кода компонента на платформы должен применяться DI.

## Что почитать про реакт

* база https://reactjs.org/
* https://github.com/vasanthk/react-bits
* https://www.udemy.com/course/pro-react-redux/learn/lecture/12415242?start=315#overview
* https://egghead.io/courses/the-beginner-s-guide-to-react
* https://egghead.io/courses/advanced-react-component-patterns
* https://overreacted.io/ от Дэна Абрамова
* https://github.com/enaqx/awesome-react
