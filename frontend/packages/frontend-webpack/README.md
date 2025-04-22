#frontend-webpack - Общая конфигурация сборки для frontend сервисов

### Ключевые особенности
- Сборка серверного и клиентского кода, с возможность собрать клиентские бандлы отдельно для каждой платформы 
- Сборка `ts`/`tsx` кода с помощью `babel` с возможность указать range поддерживаемых браузеров
- Сборка `pcss` стилей с помощью `postcss`
- Преобразование импортируемых `svg` файлов в `React` компонент ([`@svgr/webpack`](https://www.npmjs.com/package/@svgr/webpack))
- Реализация `lazy loading` на базе [`@loadable/component`](https://loadable-components.com/docs/getting-started/)
- Анализатор бандлов с помощью [`Statoscope`](https://statoscope.tech)
- Инлайн критичного кода в HTML шаблон

### Подключение
[Пример подключения](https://a.yandex-team.ru/arc_vcs/frontend/services/stub/.config/webpack/?rev=637fff7f17)

```
getClientConfig = (params: IClientParams): webpack.Configuration[]

interface IClientParams {
    platforms?: string[]; // Список всех поддерживаемых платформ
    buildPathRoot?: string; // Путь до сборочной директории
    buildPathStatic?: string; // Путь до директории с собранной статикой
    entries?: { // Список entry point'ов приложения
        main?: string;
        inline?: string;
        logger?: string;
    },
    htmlTemplatePath?: string; // Путь до исходного HTML шаблона
    supportedBrowsers: string[]; // Список поддерживаемых браузеров, по формату https://github.com/browserslist/browserslist
}
```

```
getServerConfig = (params: IServerParams = {}): webpack.Configuration

interface IServerParams {
    entry?: string; // Entry point серверного кода
    buildPath?: string; // Путь до сборочной директории
}
```


### Переменные окружения
- `YENV` (`production`/`testing`/`development`) - влияет на режим сборки и на формирование пути `publicPath`
- `ENABLE_STATOSCOPE` (`1`/`0`) - включает сборку отчета анализатора бандлов 
