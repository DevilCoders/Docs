# Ванильный пользователь
> Блок пользователя User2

<img src='https://jing.yandex-team.ru/files/axaxaman/user2.png' height='400'>

## Описание

Это специальным образом собранный блок пользователя. который можно использовать у себя на сервисе.
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
import * as UserHTML from '@yandex-lego/serp-header/dist/base/user2.desktop';

// получаем HTML, (список всех параметров перечислен внизу)
const user = UserHTML.getContent({tld: 'ru', lang: 'ru'});

// Рендерим HTML компонента
<div dangerouslySetInnerHTML={{ __html: user }}></div>
```

#### 2. Подключаем `<script>` для работы компонента
```ts
import { getStaticPath } from '@yandex-lego/serp-header/StaticPath';


const staticPropsUser = {
    key: 'base', // Вариант сборки блока, по умолчанию base
    platform: 'desktop',
    block: 'user2',
    service: 'base'
};

// Вставляем в своем приложении скрипт в конце body
<>
    <script type="text/javascript" src={getStaticPath(staticPropsUser)}></script>
<>

```
Если у вас Next.js приложение вам нужен Custom Document: https://nextjs.org/docs/advanced-features/custom-document


### Рендреринг на клиенте
> Надо быть готовым к тому, что клиентский бандл вырастет

Подключить компонент.
Он внутри себя:
- вызывает функцию, которая отдает HTML
- вставляет этот html в div через `dangerouslySetInnerHTML`
- после монтирования компонента вставляет в конец body ссылку на клиентский код компонента
```ts
import { User2Vanilla } from '@yandex-lego/serp-header/User2/desktop';

// Рендерим в нужном месте приложения
<>
    <User2Vanilla
        {...userProps}
    />
</>
```

### Props

| Props               | Значение default*                | Описание                                                 |
|---------------------|----------------------------------|----------------------------------------------------------|
| uid                 | number, string                   | Уникальный идентификатор пользователя                    |
| yu                  | number, string                   | Cookie-файлы `yandexuid`                                 |
| retpath?            | number, string                   | URL страницы                                             |
| tld                 | string                           | Язык сборки                                              |
| lang                | string                           | Язык интерфейса колокольчика                             |
| theme?              | string                           | Тема (бывает white для темных и прозрачных шапок)        |
| bundleKey?          | 'base', 'move-to-header'         | Какую сборку подключить                                  |
| iframeUrl?          | string                           | Передать свою ссылку на iframe                           |
| client?             | string (serp_gnc*)               | Path для запроса за уведомлениями                        |
| source?             | string (lego*)                   | Источник запросов                                        |
| service?            | string (base*)                   | Сборка для определенного сервиса                         |
| platform?           | *desktop или touch-phone         | Платформа                                                |
| key?                | 'base', 'move-to-header'         | Ключ определенной сборки компонента                      |
| noCounter?          | boolean    false*                | Не показывать счетчик уведомлений                        |
| avatarId?           | string                           | Идентификатор аватарки пользователя                      |
| avatarUrl?          | IUserAvatarUrlProps              | Ссылки на аватар пользователя                            |
| name?               | string                           | Имя пользователя                                         |
| hasPlus?            | boolean                          | Есть ли Плюс у пользователя                              |
| yaplusAvailable?    | boolean                          | Доступен ли Плюс                                         |
| customMenuItems?    | IUserCustomMenuItem              | Список своих полей в меню                                |
| accountsUrl?        | string  api.passport.yandex.tld* | Ссылка для подтягивания мультиаккаунтов  (по умолчанию ) |
| helpUrl?            | string                           | Ссылка на помощь                                         |
| secretKey?          | string                           | Секретный ключ (для организаций)                         |
| organizationsUrl?   | string                           | Ссылка на организации                                    |
| contextSwitchUrl?   | string                           | Ссылка на переключение контекста организаций             |
| addOrganizationUrl? | string                           | Ссылка на добавление организации                         |
| loggedByLinkRetpath?| string                           | Retpath в ссылке на залогин аккаунта. Если есть, значит по клику на аккаунт в выпадушке юзера будет проходить залогин через get-запрос.|
| loggedByLink?       | boolean                          | Флаг залогин аккаунтом из попапа юзера через get-запрос. Можно задать свой retpath. Если его не будет, возьмется из параметра retpath       |
| noUserPopup?        | boolean                          | Флаг, что попап пользователя по клику не открывать (использовать вместе с userClickLink |
| userClickLink?      | string                           | Ссылка, на которую ведем по клику на блок юзера (использовать вместе с noUserPopup|
