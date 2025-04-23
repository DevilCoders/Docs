# Синхронизация иконок с Travel.Styles

Для обновления иконок и иллюстраций запустите [билд в TC](https://teamcity.yandex-team.ru/buildConfiguration/DataUI_YaTravel_YaTravelFrontend_FriggaUpdate?branch=dev&buildTypeTab=overview&mode=builds).
Этот билд подготовит PR в dev с обновлением иконок, иллюстраций и призовет вас на ревью.

### Как всё работает

Ссылка на страницу иконок в фигме выглядит так
`//https://www.figma.com/file/I8EBpOVkBHKTHVrDyWuaaIhI/Travel.Styles?node-id=9294%3A1052`
В ней:

-   `I8EBpOVkBHKTHVrDyWuaaIhI` — это ключ файла (file key)

Весь процесс примерно такой:

-   Получаем все опубликованные компоненты файла с названием вида `Icons / {size} / {name}` и фильтруем только изменившиеся относительно meta.json файла.
-   Отрисовываем и скачиваем каждый такой компонент в формате svg с помощью Figma API
-   Прогоняем каждую svg, через утилиту [SVGR](https://github.com/smooth-code/svgr), с плагинами svgo, jsx, prettier и TypeScript шаблон иконок (смотри [файл конфигурации](/frigga-icons.config.ts))
-   Сохраняем на диск по пути `src/icons/{size}/{name}`

Соответственно мы завязаны на несколько вещей:

-   все иконки должны быть компонентами в фигме
-   все иконки должны быть в одном и том же файле
-   имя иконок должно быть в формате `Icons / {size} / {name}`

> NB
> Чтобы насильно перезаписать компонент текущей версией из Figma нужно удалить запись о нем в файле `meta.json` и запустить Frigga.

## Illustrations

Иллюстрации живут в папке `src/icons/illustrations`.

В каждой папке с именем компонента может быть несколько иллюстраций разных размеров.

Пример:

`src/icons/illustrations/SubscribeHotels/SubscribeHotelsS.tsx`
`src/icons/illustrations/SubscribeHotels/SubscribeHotelsM.tsx`

Остальные параметры выгрузки можно посмотреть в [файле конфигурации](/frigga-illustrations.config.ts)

#### Что нужно, чтобы заработала загрузка иллюстраций:

-   Иллюстрация опубликована в Figma в виде компонента с именем в формате `Illustrations / MyIllustrationName / M`

```
npm run frigga:ills
```
