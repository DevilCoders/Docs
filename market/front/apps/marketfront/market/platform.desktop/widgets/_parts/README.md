## Создание виджета

### Структура файлов

**Минимально необходимая структура катологов**

```sh
widgets/_parts/Widget
├── index.js # Серверный код виджета, нормализация данных
└── view.js # Подключение виджета к стору при помощи connectWidget
```

**Структура каталогов**

```sh
widgets/_parts/Widget
├── SomeContainer # Дополнительный контейнер который используется только в виджете
│   ├── SomeContainer.js
│   ├── index.js
│   ├── selectors.js
│   └── styles.styl
├── SomeComponent # Вспомогательный компонент который используется только в виджете
│   ├── index.js
│   ├── lookup.js
│   └── styles.styl
├── Widget.js # Основной код компонента виджета
├── actions.js
├── index.js
├── lookup.js # Тут перечислены какие сущности виджет может отображать
├── reducers.js
├── selectors.js
├── styles.styl
├── types.js # flow types
└── view.js
```

### Как добавить виджет в страницу

* Скопируйте и переименнуйте [widgets/_parts/Example](Example)

```sh
cp -R widgets/_parts/Example widgets/_parts/Widget
# brew install rename
rename -S Example Widget widgets/_parts/Widget/**/*
```

[*Подробнее про rename*](http://plasmasturm.org/code/rename)

* Подключить клиентский код (`widgets/_parts/Widget/view.js`) в
  [containers/CmsRow/index.js](../../containers/CmsRow/index.js)
* Подключить серверный код (`widgets/_parts/Widget/idnex.js`) в
  [app/widgets/data/cms/ReactRow.js](../../app/widgets/data/cms/ReactRow.js)
* Добавить редьюсер в страницу, **даже если его нет!** Например,
  можно посмотреть как сделано в [pages/bvl/index.js](pages/bvl/index.js)
