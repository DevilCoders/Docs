# Ванильный колокольчик
> Глобальный центр уведомлений сервисов Яндекса

<img src='https://jing.yandex-team.ru/files/axaxaman/notifier.png' height='400'>

## Описание

Это специальным образом собранный колокольчик. который можно использовать у себя на сервисе.
Он представляет собой набор HTML и script.

Нужная верстка просто вставляется в указанное место, а script подключает со статики необходимый файл, который нужен для взаимодействия (обработчики кликов и так далее).

Компонент можно использовать как самостоятельно, так и как часть `YandexHeader`.

## Подключение
Надо поставить зависимости
```bash
npm i -PE @yandex-lego/serp-header
```
### SSR
Рекомендуемый способ подключения

#### 1. В нужном месте сервера вставить компонент в разметку
```ts
// @ts-ignore
// вместо base – можно использовать проект {disk, mail, web4, etc}
// вместо desktop – можно использовать touch-phone
import * as NotifierHTML from '@yandex-lego/serp-header/dist/base/notifier.desktop';

// получаем HTML, (список всех параметров перечислен внизу)
const notifier = NotifierHTML.getContent({tld: 'ru', lang: 'ru'});

// Рендерим HTML компонента
<div dangerouslySetInnerHTML={{ __html: notifier }}></div>
```

#### 2. Подключаем `<script>` для работы компонента
```ts
import { getStaticPath } from '@yandex-lego/serp-header/StaticPath';


const staticPropsNotifier = {
    key: 'base', // Вариант сборки блока, по умолчанию base, есть еще white
    platform: 'desktop',
    block: 'notifier',
    service: 'base'
};

<script type="text/javascript" src={getStaticPath(staticPropsNotifier)}></script>
```

Если у вас Next.js приложение вам нужен Custom Document: https://nextjs.org/docs/advanced-features/custom-document
### Рендреринг на клиенте
> Надо быть готовым к тому, что клиентский бандл вырастет

Подключить компонент.
Он внутри себя:
- вызывает функцию, которая отдает HTML
- вставляет этот html в div через `dangerouslySetInnerHTML`
- после монтирования компонента вставляет в конец body ссылку на клиентский код компонента
И подключить компонент
```ts
import { NotifierVanilla } from '@yandex-lego/serp-header/Notifier/desktop';

// Рендерим в нужном месте приложения
<>
    <NotifierVanilla
        {...notifierProps}
    />
</>
```

### Props

| Props      | Значение default*        | Описание                                          |
|------------|--------------------------|---------------------------------------------------|
| tld        | string                   | Язык сборки                                       |
| lang       | string                   | Язык интерфейса колокольчика                      |
| theme?     | string                   | Тема (бывает white для темных и прозрачных шапок) |
| bundleKey? | 'base', 'white'          | Какую сборку подключить                           |
| iframeUrl? | string                   | Передать свою ссылку на iframe                    |
| client?    | string (serp_gnc*)       | Path для запроса за уведомлениями                 |
| source?    | string (lego*)           | Источник запросов                                 |
| service?   | string (base*)           | Сборка для определенного сервиса                  |
| key?       | string                   | Ключ определенной сборки компонента               |
