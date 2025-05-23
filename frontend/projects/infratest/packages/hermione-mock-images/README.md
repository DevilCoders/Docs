# @yandex-int/hermione-mock-images

Модуль для работы с изображениями. Позволяем перехватывать все внешние запросы и подменять их фикстурами (шахматка, размер ячеек которой зависит от общего размера изображения).

## Подключение плагина

```sh
npm i @yandex-int/hermione-mock-images --registry https://npm.yandex-team.ru
```

```js
plugins: {
    '@yandex-int/hermione-mock-images': {
        enabled: true,

        // Array<string>
        // Список glob-выражений, определяющий, какие хосты нужно перехватывать.
        // По умолчанию - ["*"] (все хосты)
        hostsPatterns: ["https://ya.ru/images/**"],

        // Array<RegExp>
        // Возможность запуска для определенных браузеров.
        // По-умолчанию - [] (все браузеры).
        browsers: [/chrome-desktop/],

        // Путь к файлу с кэшем.
        // По-умолчанию - "./hermione-mock-images-cache.json"
        cacheFilePath: "./some.json",

        // Плагин может работать в двух режимах "gather" и "load".
        // По-умолчанию "load"
        mode: "gather",
    },
},
```

## Работа с плагином

### Режим сбора данных

Выполняются все реальные запросы за изображениями, из которых извлекается информация - **формат, высота, ширина.** и сохраняется в файл кеша. При этом, все изображения, которые попали под glob-выражения будут подменены моками, чтобы у разработчика сразу было представление о том, включено изображение или нет. На данный момент весь кеш хранится в одном файле.

```sh
npx hermione --hermione-mock-images-mode=gather
```

### Режим загрузки данных

В этом режиме не выполняются реальные запросы изображений, а генерируются моки на лету, основываясь на размерах и формате изображений, полученных на предыдущем шаге сбора кэша.

```sh
npx hermione --hermione-mock-images-mode=load
```
