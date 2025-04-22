# Loadable components
Мы используем библиотеку [loadable-components](https://loadable-components.com/).
Она разбивает реакт-бандл на отдельные чанки, содержащие асинхронно подгружаемые компоненты.

Эта дока нужна, чтобы описать кейсы использования и, что более важно, сохранить знание о костылях.

## Кейсы использования
Суть пунктов ниже одна: асинхронно загрузить код какого-либо компонента.

1. Разбиение бандла на чанки по страницам.
Например, [страницы тача](../realty-mobile-www/view/routes/common.js).
2. Подгрузка какого-либо тяжёлого компонента параллельно с основным чанком страницы для ускорения этой страницы.
Например, [страница поиска на карте в таче](../realty-mobile-www/view/components/pages/SearchMapPage/index.js) - тут карта подгружается параллельно с остальным кодом.
3. Условный рендеринг какого-либо тяжёлого компонента.
Например, [карта выбора области на странице фильтров в таче](../realty-mobile-www/view/components/FiltersForm/fields/MapAreaFiltersFormField/index.js), которая подгружается только после нажатия пользователем на "нарисовать область".
4. Рендеринг по доскроллу до какого-то места с помощью [withVisibilityRender](../realty-core/view/react/common/enhancers/withVisibilityRender)
Например, [главная в таче](../realty-mobile-www/view/components/pages/IndexPage/IndexPageContent/index.js), где SEO-ссылки, находящиеся под фильтрами, подгружаются только когда пользователь до них доскроллил.

## Костыли

----------------------------------------

### Несовместимость `loadable-components` с `react-router v3`

#### **Решение**:
Убираем ref-forwarding при передаче роута в функцию `loadable`.

#### **Где лежит**:
[loadable-route.js](../realty-core/view/react/libs/loadable-route.js)

#### **Как использовать**:
При оборачивании _компонента страницы_ использовать функцию `loadable`,импортируемую не из `@loadable/component`, а из [realty-core/view/react/libs/loadable-route.ts](../realty-core/view/react/libs/loadable-route.js).

#### **Пример**:
[Роуты тача](../realty-mobile-www/view/routes/common.js).

----------------------------------------

### Чанки, которые должны загружаться по доскроллу, загружаются вместе со страницей

#### **Решение**:
Добавляем в оригинальную библиотеку `@loadable/component` опцию `excludeChunkFromExtractor`, с помощью которой можно явно исключать чанки из списка подгружаемых при загрузке страницы.
Это решение взято из [PR в оригинальную библиотеку](https://github.com/gregberge/loadable-components/pull/749), который ещё не влит и вряд ли будет в ближайшее время (если будет влит, то нужно убрать наш костыль).

Используем эту опцию на загружаемых по доскроллу компонентах.

#### **Где лежит**:
Форк пакета `@loadable/component` лежит в яндексовом `npm` под именем [@vertis/temp-loadable-component](https://npm.yandex-team.ru/-/ui/?text=@vertis/temp-loadable-component). 

В [package.json](../package.json) он загружается под именем оригинальной библиотеки. 

#### **Как использовать**:
При оборачивании компонента, загружаемого по доскроллу (обычно, при помощи [withVisibilityRender](../realty-core/view/react/common/enhancers/withVisibilityRender)), в функцию `loadable` добавлять опцию `excludeChunkFromExtractor: true`.

#### **Пример**:
Компонент `LoadableIndexPageBottomContent` в коде [главной страницы в таче](../realty-mobile-www/view/components/pages/IndexPage/IndexPageContent/index.js).