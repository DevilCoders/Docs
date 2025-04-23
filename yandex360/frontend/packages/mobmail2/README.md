# Компоненты отображения тредов и саджеста для мобильных приложений

## Разработка

```
git clone git@github.yandex-team.ru:Daria/mobmail2.git
cd mobmail2
npm install
npm start
npm test
```

## Как получить код проекта?
Пакет публикуется в локальный NPM и может быть установлен как обычная зависимость или получен по ссылке архивом
```bash
VERSION=1.1.0-beta3 # TODO: поставить настоящую версию
curl -L https://npm.yandex-team.ru/@ps-int/mobmail2/-/@ps-int/mobmail2-$VERSION.tgz | tar -xzv -C ./
mv ./package/build mobmail2@$VERSION
rm -rf ./package
```

В директории mobmail2@$VERSION появится следующая структура
```
./mobmail2@1.1.0-beta3/
├── android
│   ├── suggest/...
│   └── thread/...
└── ios
    ├── suggest/...
    └── thread/...
```


## Локализация

[Пример](https://github.yandex-team.ru/Daria/mobmail2/blob/a834c03ddf5e5081617945222b1112ca79de023e/build.dev.json#L38-L41)

## Сборка

Для ios: `npm run build-ios`

Для android: `npm run build-android`


## Треды

При разработке треды доступны по http://localhost:8080/index.html

Собираются так:

```
build
├── suggest
│   ├── index.html.mustache
│   ├── js
│   │   ├── bundle.js
│   │   └── bundle.min.js
│   └── static
│       ├── phone.css
│       └── tablet.css
└── thread
    ├── index.html.mustache
    ├── js
    │   ├── bundle.js
    │   └── bundle.min.js
    └── static
        ├── phone.css
        └── tablet.css
```


### Темная тема

Управлять глобальной темной темой:

```javascript
thread.toggleDarkTheme(
    true, // включить темную тему
    true // использовать новую тему, с выключателем и перекрашиванием писем
);
```

И включать / выключать для писем по одному:

```javascript
thread.setDarkMessage(
    '298', // message id
    true // включить / выключить
);
```

При включении / выключении темной темы в одном письме вылетает событие `message.dark.change` с двумя аргументами: `newState: "true" | "false" (это строка), mid: string`.

## Саджест

При разработке саджест доступен http://localhost:8080/suggest.html

Саджест собирается в suggest.html + suggest.js + стили, иконки

### Темная тема

```javascript
suggest.setDarkTheme(true); // или false
```

### Добавление айтемов

```javascript
suggest.setData([]);
```

В массиве все айтемы 1в1 как отвечает API. Туда можно добавить `mail-count-localized`, чтобы отображать количество писем в саджесте по темам.

Когда все айтемы с `"target": "history"` — включен zero-suggest.

### Ябблы

```javascript
thread.toggleYabbleSelection(true); // включит выбор яббла, false – выключит
```

### Добавление аватарок

Аватарки добавляются по одной:

```javascript
suggest.setAvatar('test@yandex.ru', { type: 'avatar', image: '...' });
suggest.setAvatar('test2@yandex.ru', { type: 'monogram', monogram: 'T2', color: 'ff7000' });
```

### События

По готовности принимать данные эмитится событие `DOMReady`.

По клику на саджест эмитится событие `suggest.item.click` с `id` саджеста (приходит от API).

После отрисовки саджеста эмитится событие `suggest.render.complete` с моментом получения данных реактом (ms), моментом отрисовки (ms) и диффом (ms).

По скроллу эмитится событие `suggest.scroll`.
