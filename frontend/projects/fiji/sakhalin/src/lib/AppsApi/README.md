# Yandex Applications API

В ПП API поставляется в виде объекта `window.YandexApplicationsAPIBackend`.

Наиболее полная документация к методам API доступна на wiki:
* android: https://wiki.yandex-team.ru/mobilesearch/app/android/design/jsapi/
* ios: https://wiki.yandex-team.ru/MobileSearch/iosapp/js-api/

Чтобы данный объект стал доступен, нужно подключить на странице скрипт:

```html
<script src="http://localapp/yandex-apps-api/__webview-intercepted/_api.js"></script>
```

Ниже этого элемента будет доступно полностью готовое API приложения (объект `window.YandexApplicationsAPIBackend`).

Прямая работа с этим API неудобна из-за отсутствия типизации и разнородности методов, поэтому данная библиотека добавляет тайпинги и приводит все методы API к более общему интерфейсу:
1) Асинхронные методы возвращают Promise
2) Сериализует и десериализует параметры
3) Добавляет способ удобно проверять наличие метода
4) Добавляет обёртку над методом on в виде двух методов subscribe / unsubscribe для реализации PubSub.

## Структура файлов

```
backend/
  typings.ts - Тайпинги для объекта window.YandexApplicationsAPIBackend
  supports.ts - Методы для проверки доступности API
  backend.ts - Методы для вызова API
callbackFactory/ - Фабрика колбеков для асинхронных методов API
api/ - Имплементация для всех доступных методов API
index.ts - Реэкспорт наиболее полного набора методов
serp.ts - Реэкспорт методов для серпового режима ПП
yellowSkin.ts - Реэкспорт методов для режима Yellow Skin
internal.ts - Реэкспорт методов для режима внутреннего браузера
```

## Проверка наличия методов

Для проверки наличия метода экспортируется объект `supports`, в котором для каждого метода API по его имени лежит булево значение.

Пример проверки наличия метода `openAuthDialog`:

```ts
import { supports } from 'sakhalin/src/lib/AppsApi';

if (suppots.openAuthDialog) {
    // делаем что-то полезное
}
```

Важно помнить, что при SSR все поля будут возвращать false, потому что для проверки нужен объект window, которого нет на сервере.
Поэтому все проверки должны находиться в колбеках или в "did-mount" части реакт приложения (useEffect и т.д.), чтобы гидрация на клиенте не выдавала варнингов.

## Вызов методов

Есть несколько способов импортировать методы API.

1) Импорт конкретного метода из директории `api`:

    ```ts
    import { openAuthDialog } from 'sakhalin/src/lib/AppsApi/api/openAuthDialog';

    openAuthDialog('light');
    ```

2) Импорт из набора для конкретного режима ПП: serp, yellowSkin и internal.
    Например, можно импортировать метод из набора serp:

    ```ts
    import { openAuthDialog } from 'sakhalin/src/lib/AppsApi/serp';

    openAuthDialog('light');
    ```

3) Импорт из полного набора методов:

    ```ts
    import { openAuthDialog } from 'sakhalin/src/lib/AppsApi';

    openAuthDialog('light');
    ```

Если точно известно, в каком режиме будет открываться страница (например всегда в serp), то второй способ предпочтительнее третьего, т.к. не позволяет импортировать методы, которые явно не поддерживаются в режиме.

Если страница может отображаться сразу в нескольких режимах ПП, то стоит выбрать первый или третий способ.

## Подписка на события

В ПП есть несколько видов событий, узнать полный список можно в документации на wiki или в тайпингах.

Для подписки на события экспортируется метод `subscribe`.

```ts
import { subscribe } from 'sakhalin/src/lib/AppsApi';

subscribe('EVENT_AUTH_FINISHED', () => {
    // Пользователь авторизован
});
```

Для отписки экспортируется метод `unsubscribe`. Вторым аргументом в метод `unsubscribe` нужно передать ту же самую функцию, что была передана при подписке в метод `subscribe`:

```ts
import { subscribe, unsubscribe } from 'sakhalin/src/lib/AppsApi';

const authListener = () => {
    // Пользователь авторизован
};

subscribe('EVENT_AUTH_FINISHED', authListener);

// Где-то далее

unsubscribe('EVENT_AUTH_FINISHED', authListener);
```

## Использование в React

В общем случае пример использования в реакт компонентах выглядит примерно так:

```tsx
import React, { useEffect, useCallback } from 'react';
import {
    supports,
    openAuthDialog,
    subscribe,
    unsubscribe,
} from 'sakhalin/src/lib/AppsApi/api/openAuthDialog';

const SomeComponent = () => {
    useEffect(() => {
        const onAuthFinished = () => alert('Вы авторизованы');

        // Подписываемся на событие авторизации при монтировании
        subscribe('EVENT_AUTH_FINISHED', onAuthFinished);

        // Отписываемся при анмаунте
        return () => unsubscribe('EVENT_AUTH_FINISHED', onAuthFinished);
    }, []);

    const onAuthClick = useCallback(() => {
        // Проверяем поддержку и вызываем метод API ПП
        if (supports.openAuthDialog) {
            openAuthDialog();
        } else {
            // фолбек для бро, которые не умеют в API ПП
            window.location.assign('auth_url')
        }
    }, []);

    return (
        <button type="button" onClick={onAuthClick}>
            Авторизоваться
        </button>
    );
};
```
