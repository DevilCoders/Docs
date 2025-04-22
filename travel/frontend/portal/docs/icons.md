# Синхронизация иконок с Travel.Styles

Для обновления иконок и иллюстраций запустите action [Update icons and illustrations](https://a.yandex-team.ru/projects/portalvteam/ci/actions/launches?dir=travel%2Ffrontend%2Fportal&id=update-icons-and-illustrations) в CI.

Нажмите `Run action`, в модальномм окне ничего не меняйте и подтвердите действие.

Этот билд подготовит PR в trunk с обновлением иконок и иллюстраций. Внутри запуска, внутри flow появится ссылка на PR.

![img.png](img/frigga-update.png)

### Как всё работает

Ссылка на страницу иконок в фигме выглядит так
`//https://www.figma.com/file/I8EBpOVkBHKTHVrDyWuaaIhI/Travel.Styles?node-id=9294%3A1052`
В ней:

-   `I8EBpOVkBHKTHVrDyWuaaIhI` — это ключ файла (file key)

Весь процесс примерно такой, на примере иконок:

-   Получаем все опубликованные компоненты файла с названием вида `Icons / {size} / {name}` и фильтруем только изменившиеся относительно meta.json файла.
-   Отрисовываем и скачиваем каждый такой компонент в формате svg с помощью Figma API
-   Прогоняем каждый svg компонент, через утилиту [SVGR](https://github.com/smooth-code/svgr), с плагинами svgo, jsx, prettier и TypeScript шаблон иконок (смотри [файл конфигурации](/frigga-icons.config.ts))
-   Сохраняем на диск по пути `src/icons/{size}/{name}`

Соответственно мы завязаны на несколько вещей:

-   все иконки должны быть опубликованными компонентами в фигме
-   все иконки должны быть в одном и том же файле
-   имя иконок должно быть в формате `Icons / {size} / {name}`
-   имя векторных иллюстраций `Illustrations / {name} / {size}`
-   имя растровых иллюстраций `RasterIllustration / {name} / {size}`

> NB
> Чтобы насильно перезаписать компонент текущей версией из Figma нужно удалить запись о нем в файле `meta.json` и запустить Frigga.

## Illustrations

Векторные иллюстрации живут в папке `src/icons/illustrations`.

В каждой папке с именем компонента может быть несколько иллюстраций разных размеров.

Пример:

`src/icons/illustrations/SubscribeHotels/SubscribeHotelsS.tsx`
`src/icons/illustrations/SubscribeHotels/SubscribeHotelsM.tsx`

Остальные параметры выгрузки можно посмотреть в [файле конфигурации](/frigga-illustrations.config.ts)

## RasterIllustrations

Растровые иллюстрации живут в папке `src/icons/rastter-illustrations`.

Все иллюстрации разбиты по папкам для каждого размера

Пример:

`src/icons/raster-illustrations/M/Komod3D.tsx`
`src/icons/raster-illustrations/M/BusTicket3D.tsx`
`src/icons/raster-illustrations/L/BusTicket3D.tsx`

#### Что нужно, чтобы заработала загрузка иллюстраций:

-   Иллюстрация опубликована в Figma в виде компонента с именем в формате `Illustrations / MyIllustrationName / M`

```
npm run frigga:ills
```
