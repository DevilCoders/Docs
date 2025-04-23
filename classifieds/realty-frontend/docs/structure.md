# Структура репозитория

Репозиторий состоит из множества сервисов, разрабатываемых и поддерживаемых разными командами.

Помимо самих сервисов есть общий переиспользуемый между сервисами код.

## Описание переиспользуемых частей

Оглавление:
* [packages](#packages)
* [realty-core](#realty-core)
* [realty-router](#realty-router)
* [vertis-react](#vertis-react)

### packages <a name="packages"></a>

Здесь хранятся переиспользуемые между сервисами модули/библиотеки.
Например: иконки, библиотека для работы с рекламой, конфиг для dayjs.

Обращение к модулям происходит через импорт `@realty-front`

Пример:
```tsx
import closeIcon from '@realty-front/icons/common/close-24.svg';
```

[Подробнее](../packages/readme.md)

### realty-core <a name="realty-core"></a>

Здесь хранится весь переиспользуемый между сервисами код.

В папке [app](../realty-core/app) хранится код использующийся на стороне nodejs.

Например: [общие провайдеры](../realty-core/app/providers), [переиспользуемые гейты](../realty-core/app/controller/gates), [функции-хелперы](../realty-core/app/lib), какие-то общие куски на базе которых пишется специфичный код (например базовый [page](../realty-core/app/controller/pages/page.js) контроллера).

В папке [resource](../realty-core/app/resource) распложены все ресурсы, через которые мы ходим в бекенды.

[Подробнее про работу серверного кода](./server.md)

----------

В папке [view](../realty-core/view) хранится код использующийся на клиентской стороне.

Например: общие компоненты, хуки, редьюсеры ([десктоп](../realty-core/view/react/deskpad), [тач](../realty-core/view/react/touch-phone), [мультиплатформа](../realty-core/view/react/common)), [функции-хелперы](../realty-core/view/react/libs)

В папке [modules](../realty-core/view/react/modules) находится сгруппированная по бизнес-логике функциональность (редьюсеры, метрика, функции-хелперы).

------

В папке [types](../realty-core/types) хранятся общие типы.

Для обращения к коду из `realty-core` всегда используем абсолютные импорты.

Пример:
```tsx
import Rtb from 'realty-core/view/react/libs/rtb';
```

### realty-router <a name="realty-router"></a>

Пакет, использующийся для роутинга внутри сервисов.
Отвечает за матчинг роутов, а так же за построение ссылок.

* [Десктопные роуты](../realty-router/routes/desktop)
* [Тачовые роуты](../realty-router/routes/desktop)

Для обращения к коду из `realty-router` используем абсолютные импорты.

Пример:
```tsx
import realtyRouter from 'realty-router';
```

[Подробнее](../realty-router/README.md)


### vertis-react <a name="vertis-react"></a>

Библиотека базовых React-компонентов.

Содержит: [базовые компоненты](../vertis-react/components), [сторибук истории для них](../vertis-react/stories), [общие css-переменные](../vertis-react/view/vars/vars.css)

[Подробнее](../vertis-react/README.md)

## Описание сервисов, живущих в монорепе

> Разрабатывать (писать код) любой сервис может любая команда, а не только та, что поддерживает его.
> 
> Под поддержкой сервиса имеется ввиду команда, которая больше всех контрибьютит в этот сервис.
> И к которой можно приходить с проблемами или вопросами по сервису.

В основном разработкой сервисов занимаются следующие команды:
* [Arenda](https://staff.yandex-team.ru/departments/yandex_personal_vertserv_4777_5826_dep42197)
* [Classified](https://staff.yandex-team.ru/departments/yandex_personal_vertserv_interface_interfaces1)
* [VTF](https://staff.yandex-team.ru/departments/yandex_personal_vertserv_interface_2830_dep83888/)

Оглавление:
* [realty-amp-www](#realty-amp-www)
* [realty-arenda](#realty-arenda)
* [realty-chat](#realty-chat)
* [realty-cream](#realty-cream)
* [realty-data-cache-api](#realty-data-cache-api)
* [realty-data-cache-job](#realty-data-cache-job)
* [realty-journal](#realty-journal)
* [realty-lk-www](#realty-lk-www)
* [realty-mobile-www](#realty-mobile-www)
* [realty-partner](#realty-partner)
* [realty-payment](#realty-payment)
* [realty-pdf-printer](#realty-pdf-printer)
* [realty-router-api](#realty-router-api)
* [realty-search-app](#realty-search-app)
* [realty-search-app-updater](#realty-search-app-updater)
* [realty-seo-api](#realty-seo-api)
* [realty-spammer](#realty-spammer)
* [realty-www](#realty-www)
* [realty-www-nginx-static](#realty-www-nginx-static)


### realty-amp-www <a name="realty-amp-www"></a>
AMP-версия Яндекс.Недвижимости, поддержано ограниченное количество страниц сервиса.

[Подробнее](../realty-amp-www/README.md)

Поддержкой занимается команда **VTF**

### realty-arenda <a name="realty-arenda"></a>
Сервис Яндекс.Аренда: личный кабинет + лендинги.

[Подробнее](../realty-arenda/README.md)

Поддержкой занимается команда **Arenda**

### realty-chat <a name="realty-chat"></a>
Виджет чатов, использующийся для коммуникации между пользователей внутри сервисов.

[Подробнее](../realty-chat/README.md)

Поддержкой занимается команда **Classified**

### realty-cream <a name="realty-cream"></a>
CRM-система для биздева и операторов колл-центра.
Сервис на поддержке, разработка его практически не ведется.

[Подробнее](../realty-cream/README.md)

Поддержкой занимается команда **Classified**

### realty-data-cache-api <a name="realty-data-cache-api"></a>
Сервис для получения закешированных ссылок для блоков на Яндекс Недвижимости.

[Подробнее](../realty-data-cache-api/README.md)

Поддержкой занимается команда **VTF**

### realty-data-cache-job <a name="realty-data-cache-job"></a>
Сервис для кеширования ссылок для блоков на Яндекс.Недвижимости.

[Подробнее](../realty-data-cache-job/README.md)

Поддержкой занимается команда **VTF**

### realty-journal <a name="realty-journal"></a>
Журнал Недвижимости «Я так живу». 
По сути блог с набором статей и провязками на основной сервис Недвижимости.

[Подробнее](../realty-journal/README.md)

Поддержкой занимается команда **VTF**

### realty-lk-www <a name="realty-lk-www"></a>
Личный кабинет пользователей Яндекс.Недвижимости: физических и юридических лиц (агентов и агентств недвижимости).

Через него пользователи могут публиковать и управлять своими объявлениями.

[Подробнее](../realty-lk-www/README.md)

Поддержкой занимается команда **Classified**

### realty-mobile-www <a name="realty-mobile-www"></a>
Мобильная (тач) версия сервиса Яндекс.Недвижимость

[Подробнее](../realty-mobile-www/README.md)

Поддержкой занимается команда **Classified**

### realty-partner <a name="realty-partner"></a>
Партнерский кабинет для управления ЖК и КП застройщиками, рекламными агентствами, так же нашим отделом продаж.

[Подробнее](../realty-partner/README.md)

Поддержкой занимается команда **Classified**

### realty-payment <a name="realty-payment"></a>
Сервис платежной формы. По сути просто iframe с виджетом ЮКассы. Находится под PCI DSS.

[Подробнее](../realty-payment/README.md)

Поддержкой занимается команда **Classified**

### realty-pdf-printer <a name="realty-pdf-printer"></a>
Сервис, формирующий pdf-документ на основе шаблонов.

[Подробнее](../realty-pdf-printer/README.md)

Поддержкой занимается команда **Arenda**

### realty-router-api <a name="realty-router-api"></a>
Сервис, занимающийся роутингом Недвижимости и построением ссылок.
Создан как замена пакету `realty-router `.

[Подробнее](../realty-router-api/README.md)

Поддержкой занимается команда **VTF**

### realty-search-app <a name="realty-search-app"></a>
Сервис для встраивания блоков Яндекс.Недвижимости на главную и поиск Яндекса.

[Подробнее](../realty-search-app/README.md)

Поддержкой занимается команда **VTF**

### realty-search-app-updater <a name="realty-search-app-updater"></a>
Обновляет данные в YDB, откуда их читает search-app.

[Подробнее](../realty-search-app-updater/README.md)

Поддержкой занимается команда **VTF**

### realty-seo-api <a name="realty-seo-api"></a>
Сервис, созданный для динамического формирования данных для нужд SEO (апи для формирования сайтмапа, шаблонные тексты и т.п.).

[Подробнее](../realty-seo-api/README.md)

Поддержкой занимается команда **VTF**

### realty-spammer <a name="realty-spammer"></a>
Сервис предназначен для отправки email'ов пользователям по инициативе другого сервиса на стороне бекэнда,

[Подробнее](../realty-spammer/README.md)

Поддержкой занимается команда **VTF**

### realty-www <a name="realty-www"></a>
Десктопная версия сервиса Яндекс.Недвижимость.

[Подробнее](../realty-www/README.md)

Поддержкой занимается команда **Classified**

### realty-www-nginx-static <a name="realty-www-nginx-static"></a>
Сервис отдающий статичные файлы (favicon, служебные файлы для роботов, браузеров и т.п.)

[Подробнее](../realty-www-nginx-static)

Поддержкой занимается команды **Classified** и **Arenda**
