
# Шторка обратной связи `drawer-support`

**Оглавление**
- [Шторка обратной связи `drawer-support`](#шторка-обратной-связи-drawer-support)
  - [Ссылки](#ссылки)
  - [Фронтенд](#фронтенд)
    - [Компоненты](#компоненты)
    - [Хелперы](#хелперы)
  - [Сансара](#сансара)
  - [Алгоритм подключения шторки](#алгоритм-подключения-шторки)
    - [Пример отправляемых данных:](#пример-отправляемых-данных)
  - [Бэкенд](#бэкенд)
  - [Создание тикета в тестовой очереди](#создание-тикета-в-тестовой-очереди)

## Ссылки
- Сансара:
  - Боевая очередь: [101827](https://samsara.yandex-team.ru/search?statuses=NEW&statuses=OPEN&queues=101827)
  - Тестовая очередь: [100983](https://red-test.samsara.yandex-team.ru/search?statuses=NEW&statuses=OPEN&queues=100983)
- Бекенды:
    - Боевой бекенд доступен по `yandex.ru/drawer-support`
    - Тестовый бекенд: `l7test.yandex.ru/drawer-support`
    - [Бекенды в YandexDeploy](https://deploy.yandex-team.ru/projects/drawer-support)

## Фронтенд
### Компоненты
Компонента шторки позволяет быстро и просто встроить кастомизированную шторку обратной связи для пользователя. Есть определенный набор маленьких компонентов из которых ее можно собирать. Они лежат здесь: [FeedbackDrawer](https://a.yandex-team.ru/arc_vcs/frontend/projects/web4/src/components/FeedbackDrawer?from_pr=2014714&rev=r8753495).

Шторка на десктопе используется леговский [Modal](https://lego.yandex-team.ru/lego-components/components/modal/examples), а на тачах представлена в виде компонента [Drawer](https://lego.yandex-team.ru/lego-components/components/drawer/examples). Все элементы шторки имеют одинаковый внешний вид что на десктопе, что на тачах, это очень сильно упрощает интеграцию.

### Хелперы
Есть различные хелперы, которые помогают встраивать шторку:
- `helper.ts` – [хелпер](https://a.yandex-team.ru/arc_vcs/frontend/projects/web4/src/features/EntityFeedback/EntityFeedback.components/helpers.ts?rev=users%2Flikipiki%2FSERP-143486) с проверкой email адреса на валидность
- `FeedbackDialog.tsx` - [Компонент](https://a.yandex-team.ru/arc_vcs/frontend/projects/web4/src/components/FeedbackDrawer/Dialog/FeedbackDialog.tsx) для переключения различных view шторки. Он делает простым смену контента внутри шторки.
- `AjaxWrapper.ts` - [обертка](https://a.yandex-team.ru/arc_vcs/frontend/projects/web4/src/features/EntityFeedback/AjaxWrapper.ts?rev=users%2Flikipiki%2FSERP-143486) с различными методами для похода в ручки бэкенда.

## Сансара
Пример собранной шторки можно найти и посмотреть в storybook (FeedbackDrawer).

Тикеты в очереди Сансары обычно создаются через 3-4 минуты после отправки.

У создаваемого тикета есть несколько основных полей:
- `message` – основное поле тикета, его можно использовать для передачи различных данных. При создании тикета Сансара санитайзит весь текст (вычищает html разметку), который туда передается. Отдельно санитайзить это поле перед отправкой не нужно.
- `email` – пользовательский email. Отображается в поле "от кого" в тикете, а так же прорастает в кастомное поле Email.
- `attachments` – прилагаемые к тикету файлы, добавляются в массива объектов после загрузки через `/upload/multipart`.
- `feedback` – поле для передачи пользовательского фидбэка.
- `fields` – через это поле можно передавать свои собственные поля, которые будут размещены в теле тикета. Оно представляет из себя массив объектов: ключ - значение. Ключом будет название поля, его значение будет располагаться под ним в тикете.
```typescript
fields: [{ name: "Название", value: 'Значение' }]
```
- `metaFields` - поле отправки данных для отладки. Будет отображаться в конце тикета, в разделе "Информация для отладки". Оно имеет поле `fields`, аналогичное полю выше. Все что создается в этом поле будет доступно только асессорам, оно не пойдет в ответное письмо пользователям.

## Алгоритм подключения шторки
1. Посмотреть как реализован [боевой пример](https://a.yandex-team.ru/arc_vcs/frontend/projects/web4/src/features/EntityFeedback) шторки для карточки Объектного ответа
2. Собрать шторку из необходимых компонентов
3. Реализовать ajax запросы с помощью хелперов/оберток
   1. Получить `CSRF` токен при первом открытии шторки (токен действует 3 часа с момента получения)
   2. Собрать данные для отладки `metaFields`. Пример можно найти [тут](https://a.yandex-team.ru/arc_vcs/frontend/projects/web4/src/features/EntityFeedback/EntityFeedback@common.server.tsx).
   3. Прикрепить нужные медиафайлы (если это необходимо). Для этого используется хелпер `uploadFile`.
   4. Используя хелпер `createTicket` создать тикет в Сансаре

### Пример отправляемых данных:
```typescript
  const drawerFeedback = {
    message: 'Текст тикета',
    fields: [{
        /**
         * Кастомные поля для тикета:
         *
         * Например, можно передать название карточки объектного ответа,
         * которая была на странице по этому запросу
         *
         * Эти поля будут отправлены пользователю в письме на тикет от асессоров
         * (Не записывайте в них то, что не надо видеть пользователю)
         */
        name: 'Название карточки ОО',
        value: 'Владимир Ильич Ленин'
    }],
    /**
     * Обязательные поля с метаинформацией для отладки
     * Все поля metaFields, видят только асессоры, они не идут в ответное письмо пользователю
     */
    metaFields: {
        // Название фичи, откуда вызвался жалобщик
        feature: 'Объектный ответ',
        // Пользовательский email, если его оставили
        email: 'my_cool_mail@yandex.ru',
        pageUrl: 'https://yandex.ru/search/?text=Владимир+Ленин',
        // Текст запроса
        queryText: 'Владимир Ленин',
        userAgent: 'Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/94.0.4606.85 YaBrowser/21.11.0.2054 Yowser/2.5 Safari/537.36',
        yandexuid: '9847287161633017918',
        // Номер документа на выдаче
        docId: '14',
        uid: '0',
        /**
         * Кастомные поля для метаинформации:
         *
         * Например, можно передать ентушку с которой показывается карточка
         */
        fields: [{
            name: 'entref',
            value: '0oCghydXc1Mjg1NRgCZCoFiA'
        }]
    }
}
```

 В Сансаре это будет выглядеть вот так: [ссылка](https://red-test.samsara.yandex-team.ru/ticket/150024678/articles)

## Бэкенд

Боевой бекенд шторки находится [services/drawer-support](https://a.yandex-team.ru/arc/trunk/arcadia/frontend/services/drawer-support). Он доступен по урлу `drawer-support`. Тестовый бекенд работает с тестовой очередь Сансары и доступен в ручке `l7.test.tld/drawer-support`. Его можно использовать для проверки, что тикеты отправляются.

Доступные ручки, поддерживаемые бекендом:
- `/drawer-support/`
  - `GET /ping` – Readness Probe, дергается Яндекс деплоем раз в 15 минут, чтобы проверить состояние бекенда.
  - `POST /token` – получение `CSRF` токена аутентификации. Для похода в остальные ручки обязательно нужно указывать `CSRF token` для аутентификации в заголовке `x-csrf-token`. Время действия токена 3 часа с момента создания.
  - `POST /tickets/`– все что связано с созданием тикетов в Сансаре.
    - `POST /tickets/validate` – валидация email средствами Сансары.
    - `POST /tickets/new` – создание нового тикета в Сансаре
    - `POST FORM-DATA /upload/multipart` – загрузка медиафайлов в Сансару
        - Аттач для файлов поддерживает следующие типы файлов для загрузки:
            - Картинки: `jpg, jpeg, png`
            - Видео: `'mp4', 'avi', 'gif', 'mov', 'wmv', 'mov'`

Для мониторингов за состояние бекендов используется Juggler, настроены нотификации через Email и Телеграм. Если вы хотите тоже получать уведомления о падениях бекендов, пожалуйста, не добавляйте себя самостоятельно в конфиг, можно приходить в слак [@likipiki](https://staff.yandex-team.ru/likipiki) с этим вопросом.

## Создание тикета в тестовой очереди

У kotikа настроена конфигурация на стабы для всех ручек, которые поддерживает бекенд drawer-support. Чтобы ходить локально в тестовую очередь, нужно изменить [middleware](https://a.yandex-team.ru/arc_vcs/frontend/projects/web4/.config/kotik/middlewares/controllers/stubs/feedback-drawer/index.js?from_pr=2014714&rev=r8753495) koticа на следующий. Это бывает полезно, если хочется проверить что тикеты действительно создаются. Но на бете в пулл реквесте запросы будут ходить через апстрим в балансере hamstera в боевую очередь.
```javascript
'use strict';

const createProxyMiddleware = require('http-proxy-middleware');

let proxy;

function drawerSupportStubController(req, res, next) {
    if (!proxy) {
        proxy = createProxyMiddleware({
            target: 'http://l7test.yandex.ru/drawer-support',
            changeOrigin: true,
            secure: false
        });
    }

    return proxy(req, res, next);
}

module.exports = {
    drawerSupportStubController
};
```
