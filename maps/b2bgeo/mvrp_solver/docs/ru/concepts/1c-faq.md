# Часто задаваемые вопросы

### Можно ли дорабатывать модуль самостоятельно?

Да, можно. Модуль предоставляется безвозмездно и без каких-либо ограничений по возможностям его модификации. Подробнее см. в разделе [Лицензия](https://yandex.ru/routing/doc/vrp/concepts/1c-integration-modules_index-page.html#litsenziia).

### Где найти дополнительную информацию о модуле?

Посмотрите вебинар [Как научить 1C планировать оптимальные маршруты?](https://yandex.ru/routing/webinar/10-09-2020-marshruty-1c-zapis)

### Запускаю автоматическую обработку — не заполняется справочник «Основные настройки».

Попробуйте загрузить настройки из файла, см. пункт 2 [Шага 3: Заполнение справочников и настроек](https://yandex.ru/routing/doc/vrp/concepts/1c-guide-uf.html#shag-3-zapolnenie-spravochnikov-i-nastroek).

### Откуда берутся координаты при заполнении заказов?

См. пункт 3 [Шага 4: Загрузка заказов](https://yandex.ru/routing/doc/vrp/concepts/1c-guide-uf.html#shag-4-zagruzka-zakazov). В справочнике **Общие настройки** есть параметр **Заполнять координаты случайными значениями**. Он отвечает за формирование случайных координат для заказов в зависимости от координат склада, чтобы можно было тестировать модуль без подключения геокодера.

### У меня в базе 1С ведутся свои данные по координатам. Нужен ли мне геокодер?

Нет. Геокодер нужен в ситуации, когда есть данные только по адресам и эти адреса постоянно меняются. Модуль на текущий момент не поддерживает справочник координат для адресов, т. е. использование своих данных по координатам необходимо доработать.

### Откуда взять ключи/токены, чтобы модуль работал с Яндекс.Маршрутизацией?

**КлючAPI для Яндекс.Маршрутизация** после регистрации на [сервисе](https://yandex.ru/courier/) нужно взять из раздела **Настройки** → **Компания** → **API Key**.

**КлючAPI для Яндекс.Геокодирование** необходимо получить в [Кабинете Разработчика](https://developer.tech.yandex.ru) для сервиса **JavaScript API и HTTP Геокодер**. Бесплатный ключ не будет работать из 1С (см. [условия использования](https://yandex.ru/dev/maps/jsapi/doc/2.1/terms/index.html/#index__conditions)). Как приобрести Геокодер, см. в разделе [Как купить лицензию](https://yandex.ru/dev/maps/commercial/doc/concepts/how-to-buy.html) документа [Коммерческая версия API Яндекс.Карт](https://yandex.ru/dev/maps/commercial/doc/concepts/about-enterprise.html).

**Токен для Яндекс.Мониторинг** нужно [получить на сервисе Яндекс.OAuth](https://yandex.ru/routing/doc/delivery/concepts/quickstart/register.html). Это делается через учетную запись, у которой есть доступ уровня **Администратор** к ID компании в [Яндекс.Маршрутизации](https://yandex.ru/courier).

Обратите внимание, что значения ключей и токена разные.

### В рабочем месте логиста нажимаю кнопку «Отправить запрос» — возникает ошибка «Query parameter ‘apikey’ is missing».

В справочнике **Общие настройки** нужно заполнить параметр **Ключ API для Яндекс.Маршрутизации**.

### В рабочем месте логиста нажимаю кнопку «Отправить запрос» — возникает ошибка: «Json document is not consistent with schema. Schema document: #/properties/vehicles/items/properties/shifts/items/properties/penalty Fail keyword: additionalProperties Fail document: #/vehicles/0/shifts/0/penalty/drop».

Ошибка `Json document is not consistent with schema` означает, что нарушена [структура JSON-запроса к API](https://yandex.ru/routing/doc/vrp/ref/MultipleVehiclesRouting/addMVRPTask.html). Это может происходить, если отсутствует обязательный параметр; добавлен лишний параметр, которого нет в спецификации; нарушены ограничения минимальных или максимальных значений.

В тексте сообщения указано, в каком параметре ошибка. В данном случае в смену транспортного средства был добавлен лишний параметр `penalty.drop`, т. е. для смен ТС в справочнике **Настройки штрафов для алгоритма** указан штраф за недоставку. Его можно определять только для заказов.
