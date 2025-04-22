#GEXML

## Общее описание структуры данных

основные данные модуля представляют собой дерево в формате json,
которое хранится приватно в рутовом компоненте в переменной `mainGEXMLTreeJSON`
формат каждого элемента описан в [RepresentationJSON](./types.ts)

Дерево изначально устанавливается в `<CardActions/>` при запросе новых карточек
а так же модифицируются при редактировании с помощью `GEXMLContext.dispatchChanges(currentPath, elementChanges)`

Каждый дочерний компонент отрисовывается благодаря передаче только пути до него пропсой - `currentPath`
Например карточка содержит один элемент - а значит рутовой путь равен `children[0]`
соответственно все последующие пути относительны родителя, например `'${currentPath}._children[${index}]'`

Из контектста можно получить нужный элемент с помощью `GEXMLContext.getElement(currentPath)` только там где он необходим
а так же получать новые изменения автоматически без проброса данных через всё дерево

Все свойства контекста описаны в [GEXMLContextType](./context/types.ts)

## [Составляющие рутового компонента](./components/rootParts), Контекст

[`<GEXMLContextComponent/>`](./context/GEXMLContextComponent.tsx) - обёртка контекста в которой определены все данные, передающиеся вниз через [`GEXMLContext`](./context/context.tsx)

[`<CardActions/>`](./components/rootParts/CardActions/CardActions.tsx) - кнопки выбора текущей карточки, клонирования и соответствующие запросы в ручки

[`<ExportImportButtons/>`](./components/rootParts/ExportImportButtons/ExportImportButtons.tsx) - кнопки экспорта/импорта xml карточки, и всех карточек всех метаклассов

[`<Blind/>`](./components/rootParts/Blind/Blind.tsx) - серая перекрывашка, появляющаяся при редактировании


## [Рекурсивные компоненты позиционирования](./components/tree)

![](./positioningGEXML.jpg)

рекрсивные компоненты отвечающие за проход по дереву данных и прорисовку каждого необходимого контента

[`<Root/>`](./components/tree/Root/Root.tsx) - корневой компонент, отрисовывающий либо компоненты позиционирования, либо узел

[`<Node/>`](./components/tree/Node/Node.tsx) - узел, отображающий view & edit презентации контентов, а так же дочерние компоненты с помощью ветки

[`<Branch/>`](./components/tree/Branch/Branch.tsx) - ветка, возвращает массив корней

компоненты позиционирования с кастомной логикой отображения и редактирования представляют собой расширенную версию `Node`

[`<Layout>`](components/tree/Bush/Layout/Layout.tsx) - стандартная сетка-ряд-колонка, с возможностью Drag&Drop и единственное место добавления других контентов

[`<TabBar/>`](components/tree/Bush/TabBar/TabBar.tsx) - CRUD табов, каждый внутри содержит сетку

