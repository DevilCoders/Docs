## Оффлайн в мобильном приложении Я.Почты

На андройде реализована возможность работы календаря в режиме `readonly` в оффлайне

Для реализации ф-циональности оффлайна в мобильном приложении кешируются статические и динамическкие данные


### Кеширование статики (js-файлов, css-файлов, картинок)

Для того чтобы у приложения изначально были все нужные статические файлы в его сборку итоговую сборку добавляется вся статика.


#### Дистрибуция статических файлов для приложения
На андройде реализована возможность работы календаря в режиме `readonly` в оффлайне

Для реализации ф-циональности оффлайна в мобильном приложении кешируются статические и динамическкие данные


### Кеширование статики (js-файлов, css-файлов, картинок)

Для того чтобы у приложения изначально были все нужные статические файлы в его сборку итоговую сборку добавляется вся статика.


#### Дистрибуция статических файлов для приложения

Статичекие файлы календаря, которые включаются в сборку приложения доставляются с помощью npm-модуля `@ps-int/maya` (сейчас в owners этого модуля @pistch и @3y3k0,  по хорошему нужно дать права какому-нибудь боту и выкладывать пакеты от его имени).

При каждой сборке релизного пакета календаря в корпоративный регистр npm публикуется модуль `@ps-int/maya` под тэгом beta. Этот модуль содержит все файлы проекта, полученные после сборки вебпаком, а так же файл `manifest.json` (о нем ниже).

При мерже релизной ветки календаря в дев модулю `@ps-int/maya` с нужным тэгом в регистре присваивается тэг `latest`.

Таким образом, при сборке бета-версии мобильного приложения из npm вытягивается последняя опубликованная версия модуля `@ps-int/maya` под тегом beta. При сборке прод. версии мобильного приложения из npm вытягивается последняя версия `@ps-int/maya` под тэгом `latest`.

#### Статический индекс

Для работы календаря в мобильном приложении в оффлайне, кроме css и js файлов нужен статический index.html, в котором описывается загрузка всех нужных начальных скриптов, стилей, политика csp, подключение сторонних скриптов и конфигов.

Сам статический index.html собирается во время сборки основного приложения с помощью плагина html-webpack-plugin, при этом при сборке этого файла используется тот же самый шаблон из папки `shared`, что и для динамического индекса (динамический индекс выдается из ручки индекса в веб-версии календаря, статический индекс используется в оффлайн версии календаря в моб приложении). В том числе, кроме переиспользования шаблона индексной страницы, переиспользуются и все скрипты, которые вставляются в динамическую индексную страницу, но какие-то из них могут не подключаться в зависимости от конфигурации сборки статической страницы. Так же переиспользуется логика создания csp политики, но в статическом индексе вся csp политика инлайнится в index.html в специальный meta-тег с плейсхолдером для доменов.

Для работы index.html в него нужно встроить определенные статические конфиги, и заменить некоторые плейсхолдеры, об этом подробнее написано [тут](https://wiki.yandex-team.ru/users/epsilonn/Offlajjn-kalendar-v-mobilnom-prilozhenii/).

Так же нужно подгрузить динамический конфиг, о котором будет написано в разделе кеширования динамических данных.


#### Обновление статических файлов в приложении при новых релизах календаря

Раз в 2 часа (приблизительно) мобильное приложение ходит в апи календаря, а именно в ручку `/manifest`, которая отдает актуальную версию файла `manifest.json`.

Файл `manifest.json` содержит в себе конфиг с метаинформацией, которая нужна мобильному приложению для обновления календаря у себя. Одним из важных полей в этом файле является `cache.resources` - в нем содержится список статических файлов текущей версии календаря.

Таким образом, когда приложение подгружает новый `manifest.json`, оно сравнивает старый и новый списки статических файлов и если появились изменения, то подгружает новые файлы.

Подробнее про формат файла `manifest.json` можно почитать [тут](https://wiki.yandex-team.ru/users/epsilonn/Offlajjn-kalendar-v-mobilnom-prilozhenii/)

Важное замечание, которого сейчас нет в доке `manifest.json` - чтобы заработал оффлайн, в конфиге `environment` нужно указать флаг `isStaticPage` со значением `true`.


### Кеширование динамически данных

Для кеширования динамических данных используются [localforage](https://github.com/localForage/localForage) и [redux-persist](https://github.com/rt2zz/redux-persist). Содержимое стора кешируется в indexedDB. Для сериализации данных стора и структур Immutable, а так же кастомных Immutable.Record используется библиотека [remotedev-serialize](https://github.com/zalmoxisus/remotedev-serialize)

Данные складваются из стора в indexedDB каждый раз, как только поменялся стор с debounce в 100 мс (задержку можно конфигурировать).

Восстановление данных их indexedDB происходит в разные моменты работы приложения, в зависимости от разновидности данных. В данный момент есть 3 разновидности данных: динамический конфиг, события и все остальные данные стора. Динамический конфиг и все данные стора кроме событий восстанавливаются сразу при загрузке и инициализации приложения, события восстанавливаются только по надобности - например, если юзер перешел в какой-то конкретный временной интервал, то восстановятся только события из этого интервала, вместо выгрузки событий сразу всех возможных временных интервалов.


#### Текущая структура хранилища данных календаря в indexedDB 

В indexedDB сейчас создается 3 таблицы для различных данных.

Таблица `configs` - для динамического конфига календаря, данные записываются при загрузке приложения, сразу после запроса последней версии динамического конфига. Данные хранятся в виде строк сериализованных с помощью `JSON.stringify` json`а.

Таблица `common` - для всех данных стора кроме событий, модифицируется и перезаписывается каждый раз при изменении стора в приложении с debounce 100мс (задержку можно конфигурировать). Данные хранятся в той же форме, что и в сторе, в виде строк, сериализованных с помощью `remotedev-serialize`. 

Таблица `events` - содержит в себе данные о событиях юзера, модифицируется и перезаписывается каждый раз при изменении стора в приложении с debounce 100мс (задержку можно конфигурировать). Данные при хранении группируются в поля по дням и слоям, например в ячейке таблицы под названием `123:567891`, где `123` - id слоя, а `567891` - таймстемп начала дня, хранятся все события слоя `123` за соответсвующий таймстемпу день, в виде строки сериализованной с помощью `remotedev-serialize`.


#### Redux-мидлвара для запросов за динамическимии данными

Если приложение в оффлайне, то оно не должно ходить в сеть за динамическими данными, чтобы не генерировать дополнительные не информативные ошибки, таким образом последовательность действий по получению динамических данных в оффлайне и в онлайне может отличаться. Отличия в логике получения динамических данных абстрагированы от реакт компонентов и находятся на уровне бизнес-логики. За определение того, какую стратегию (оффлайн/онлайн) получения динамических данных стоит выбрать для текущего экшена в данный конкретный момент отвечает специальная redux-мидлвара.

##### Принцип работы мидлвары

Мидлвара принимает на вход redux-action, в котором должно быть поле `meta` в следующем формате:

```json
{
    "meta": {
        "offline": {
            "network": {},
            "rollback": {}
        }
    }
}
```

Если в мидлвару приходит экшен без поля `offline` в `meta`, то она ничего не делает и пропускает экшен дальше. Если поле есть, то мидлвара извлекает из стора данные о том, какой статус сети сейчас у приложения (`offline`/`online`). Если `offline`, то мидлвара диспатчит экшен из `meta.offline.rollback`, если такой экшен не передан, то мидлвара считает, что ничего делать не нужно. Если текущий статус `online`, то мидлвара диспатчит экшен из поля `meta.offline.network`.

Таким образом, получаем, что интерфейсные компоненты ничего не знают о разных стратегиях получения данных, в них просто нужно диспатчить экшен `выдай данные`, а уже в этом экшене в мете указаны экшены для разных стратегий, решение о запуске которых принимается в одном единственном месте - мидлваре. 

Концепцию можно развивать и применять дополнительные стратегии получения данных (кроме получения данных в онлайне или оффлайне) для определенных случаев.

