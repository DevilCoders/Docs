## Библиотека для подключения клиента mds

1. ```ru.yandex.market.adv.config.MdsAutoconfiguration``` - автоконфигурация для подключения к mds
   через ```ru.yandex.market.adv.client.MdsClient```.
    1. ```ru.yandex.market.adv.client.MdsRealClient``` - клиент для подключения к реальному mds
       через ```ru.yandex.market.common.mds.s3.client.service.api.MdsS3Client```.
    2. ```ru.yandex.market.adv.client.MdsLocalClient``` - клиент для локального подъема приложения. Сохраняет данные на
       диск по указанному пути в конфигурации.
    3. ```ru.yandex.market.adv.client.MdsMockClient``` - клиент, который ничего не сохраняет и не удаляет, а только
       вычитывает данные из classpath приложения.

## Подключение MdsRealClient клиента

Для включения нужно установить ```mds.s3.type=REAL```.

1. Заводим робота для подключения к mds по [инструкции](https://wiki.yandex-team.ru/tools/support/zombik/).
2. Получаем **Access key id** и **Access Secret key**
   по [инструкции](https://wiki.yandex-team.ru/mds/s3-api/authorization/#s3-roles).
3. Создаем bucket для тестинга и прода по [инструкции](https://wiki.yandex-team.ru/bliss/sozdat-s3-baket/).
4. Для прода bucket и их параметры можно менять
   через [Yandex.Cloud](https://wiki.yandex-team.ru/mds/s3-api/faq/#anonymous-access).

Все настройки клиента для подключения к реальному mds:

1. ```mds.s3.type``` - тип клиента для соединения с mds. По умолчанию соединение с реальным сервисом.
2. ```mds.s3.bucket``` - название bucket'а, созданного в пункте 3.
3. ```mds.s3.endpoint``` - URL адрес сервиса. Прод - ```s3.mds.yandex.net```, тестинг - ```s3.mdst.yandex.net```.
4. ```mds.s3.key.access``` - **Access key id** для доступа к mds из пункта 2.
5. ```mds.s3.key.secret``` - **Access Secret key** для доступа к mds из пункта 2.
6. ```mds.s3.prefix``` - общий префикс для ключей. По умолчанию не задан.

## Подключение MdsLocalClient клиента

Для включения нужно установить ```mds.s3.type=LOCAL```.

Все настройки mds клиента для локального подъема приложения:

1. ```mds.s3.type``` - тип клиента для соединения с mds. По умолчанию соединение с реальным сервисом.
2. ```mds.s3.prefix``` - путь на диске, откуда нужно вычитывать файлы и куда нужно сохранять. По умолчанию из корня.

## Подключение MdsMockClient клиента

Для включения нужно установить ```mds.s3.type=MOCK```.

Все настройки mds клиента, вычитывающего данные из classpath приложения:

1. ```mds.s3.type``` - тип клиента для соединения с mds. По умолчанию соединение с реальным сервисом.
2. ```mds.s3.prefix``` - путь в classpath'е из которого будут вычитываться файлы. По умолчанию из корня.
