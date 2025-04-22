# Webpack

Под капотом [@realty-front/webpack-utils](../packages/utils/webpack-utils).

Полная сборка конкретного проекта:
```
cd <project_name>
make webpack
```

Полная сборка и вотчинг конкретного проекта:
```
cd <project_name>
make webpack-watch
```

Сборка конкретного бандла, конкретного проекта:
```
cd <project_name>
make webpack bundle=<bundle-name>
```

Сборка и вотчинг конкретного бандла, конкретного проекта:
```
cd <project_name>
make webpack-watch bundle=<bundle-name>
```

Также, можно указать несколько бандлов через запятую:
```
cd <project_name>
make webpack bundle=<bundle-name-A>,<bundle-name-B>
```

Сборка без стилей:
```
DISCARD_CSS=1 make webpack
```

Сборка без картинок:
```
DISCARD_IMG=1 make webpack
```

Сборка без шрифтов:
```
DISCARD_FONTS=1 make webpack
```

**Q:** Как узнать `bundle-name` чтобы собрать конкретный бандл?<br>
**A:** Возможны две ситуации:
1. Если проект не разбит на бандлы (в папке `entries` нет подпапок),
то доступна только полная сборка.
2. Если проект разбит на бандлы, то имя бандла формируется из имен подпапок:
```
entries/desktop/common/ -> desktop-common
entries/common/ -> common
```
