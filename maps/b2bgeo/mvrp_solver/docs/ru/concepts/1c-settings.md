# Описание справочников и настроек

## Общие настройки

Поле |Описание
:--- |:---
**ID Компании в Яндекс.Маршрутизация**|Идентификатор компании в Яндекс.Маршрутизации (число). В интерфейсе содержится в адресной строке браузера: `https://yandex.ru/courier/companies/<ID Компании>`.
**КлючAPI для Яндекс.Маршрутизация**|Ключ для доступа к сервису планирования. В интерфейсе сервиса его можно увидеть в разделе **Настройки** → **Компания** → **API Key**.

**Группа полей Геокодирование**

Поле |Описание
:--- |:---
**Адрес сервиса Яндекс.Геокодирование**|Предопределенное значение: `geocode-maps.yandex.ru`, менять не требуется.
**Заполнять координаты случайными значениями**|Предопределенное значение: `Да`. При нем для адресов заказов будут формироваться случайные координаты (в зависимости от координат склада). Используется, когда нужно протестировать модуль без Геокодера. Если вы приобрели [Геокодер](https://yandex.ru/dev/maps/geocoder/) и ввели ключ в поле **КлючAPI для Яндекс.Геокодирование**, укажите значение **Нет**.
**КлючAPI для Яндекс.Геокодирование**|Ключ для [сервиса геокодирования](https://yandex.ru/dev/maps/geocoder/). Отличается от **КлючAPI для Яндекс.Маршрутизация**.
**Область поиска, по долготе**|Предопределенное значение: `3`. Задается в координатах. Поиск координат по долготе осуществляется в зависимости от долготы склада ± **Область поиска, по долготе** / 2 (используется при расчете параметра Геокодера [bbox](https://yandex.ru/dev/maps/geocoder/doc/desc/concepts/input_params.html)).
**Область поиска, по широте**|Предопределенное значение: `3`. Задается в координатах. Поиск координат по широте осуществляется в зависимости от широты склада ± **Область поиска, по широте** / 2 (используется при расчете параметра Геокодера [bbox](https://yandex.ru/dev/maps/geocoder/doc/desc/concepts/input_params.html)).

**Группа полей Мониторинг**

Поле |Описание
:--- |:---
**Радиус на точке доставки по умолчанию, м**|Предопределенное значение: `500`. Соответствует полю `mark_delivered_radius` при [добавлении/обновлении заказов](https://yandex.ru/routing/doc/delivery/ref/orders/api_v1_companies_company_id_orders-batch_post.html) в API Мониторинга.
**Статус заказа по умолчанию**|Предопределенное значение: `new`. Также допустимо `confirmed` (при нем в мобильном приложении Яндекс.Курьер предварительно звонить клиенту необязательно: можно сразу выполнять маршрут). Соответствует полю `status` при [добавлении/обновлении заказов](https://yandex.ru/routing/doc/delivery/ref/orders/api_v1_companies_company_id_orders-batch_post.html) в API Мониторинга.
**Токен для Яндекс.Мониторинг**|Токен для загрузки данных в сервис мониторинга (см. раздел [Получение OAuth-токена](https://yandex.ru/routing/doc/delivery/concepts/quickstart/register.html)). Токен нужно получать через учетную запись, которая имеет доступ уровня **Администратор** к вашему ID компании в сервисе [Яндекс.Маршрутизация](https://yandex.ru/courier).<br>Значение отличается от **КлючAPI для Яндекс.Маршрутизация** и **КлючAPI для Яндекс.Геокодирование**.

**Группа полей Маршрутизация → Значения по умолчанию**

Указанные значения проставляются по умолчанию для всех заказов. Если требуется задавать индивидуальные значения для отдельных заказов, такую возможность нужно дорабатывать.

Поле |Описание
:--- |:---
**Временное окно заказа**|Предопределенное значение: `0.07:00:00 – 0.23:00:00`. Соответствует полю `time_window` для `location` при отправке запроса на построение маршрутов. В модуле используется общее [временное окно](https://yandex.ru/routing/doc/vrp/concepts/properties-of-orders.html#vremennoe-okno-zakaza) для всех заказов.<br>Временное окно нужно указывать в [относительном формате](https://yandex.ru/routing/doc/vrp/concepts/properties-of-time-window.html#otnositelnyi-format-vremennykh-okon) с учетом сдвига от даты планирования.<br>Например, `0.20:00:00 – 1.06:00:00` — это промежуток с 20 часов текущего дня до 6 утра следующего дня (отсчет ведется от даты планирования).
**Жесткое временное окно заказа**|Предопределенное значение: `Да`. Соответствует полю `hard_window` для `location` при отправке запроса на построение маршрутов. Подробнее см. [Временное окно заказа](https://yandex.ru/routing/doc/vrp/concepts/properties-of-orders.html#vremennoe-okno-zakaza).
**Настройки штрафов для заказов**|Предопределенное значение: ссылка на элемент справочника **Настройки штрафов для алгоритма**. Соответствует полям `location` при отправке запроса на построение маршрутов:<ul><li>`penalty.drop`</li><li>`penalty.early.fixed`</li><li>`penalty.early.minute`</li><li>`penalty.late.fixed`</li><li>`penalty.late.minute`</li><li>`penalty.out_of_time.fixed`</li><li>`penalty.out_of_time.minute`</li></ul> Cм. описание штрафов за [нарушение временных окон заказов](https://yandex.ru/routing/doc/vrp/concepts/properties-of-orders.html#shtrafy-za-narushenie-vremennykh-okon-zakazov) и [недоставку](https://yandex.ru/routing/doc/vrp/concepts/properties-of-orders.html#shtrafy-za-nevypolnenie-zakaza).
**Сервисное время на адрес, c**|Предопределенное значение: `900`. Соответствует полю `shared_service_duration_s` для `location` при отправке запроса на построение маршрутов. Подробнее см. [Сервисное время при доставке заказов](https://yandex.ru/routing/doc/vrp/concepts/properties-of-orders.html#servisnoe-vremia-pri-dostavke-zakazov).
**Сервисное время на заказ, с**|Предопределенное значение: `120`. Соответствует полю `service_duration_s` для `location` при отправке запроса на построение маршрутов. Подробнее см. [Сервисное время при доставке заказов](https://yandex.ru/routing/doc/vrp/concepts/properties-of-orders.html#servisnoe-vremia-pri-dostavke-zakazov).
**Тип заказа**|Предопределенное значение: `delivery`. Также допускается значение `pickup` (для случаев, когда выполняется сбор заказов для доставки на склад). Другие типы заказов в модуле не поддерживаются. Подробнее см. [Тип заказа](https://yandex.ru/routing/doc/vrp/concepts/properties-of-orders.html#tip-zakaza).<br>Соответствует полю `type` для `location` при отправке запроса на построение маршрутов.

**Группа полей Маршрутизация → Настройки маршрутизации**

Поле |Описание
:--- |:---
**Адрес запроса результата маршрутизации**|Предопределенное значение: `/vrs/api/v1/result/mvrp/`, менять не требуется.
**Адрес отправки запроса на маршрутизацию**|Предопределенное значение: `/vrs/api/v1/add/mvrp?apikey=`, менять не требуется.
**Адрес просмотра результатов планирования**|Предопределенное значение: `https://courier.yandex.ru/mvrp-map#`, менять не требуется.
**Адрес сервиса Яндекс.Маршрутизация**|Предопределенное значение: `courier.yandex.ru`, менять не требуется.

**Группа полей Маршрутизация → Опции**

Поле |Описание
:--- |:---
**merge_multiorders**|Предопределенное значение: `Да`. Соответствует полю `merge_multiorders` для `options` при отправке запроса на построение маршрутов. Подробнее см. [Мультизаказы](https://yandex.ru/routing/doc/vrp/concepts/properties-of-orders.html#multizakazy).
**penalize_late_service**|Предопределенное значение: `Нет`. Соответствует полю `penalize_late_service` для `options` при отправке запроса на построение маршрутов. Подробнее см. в разделе [Штраф за обслуживание вне временного окна](https://yandex.ru/routing/doc/vrp/concepts/penalize-late.html).
**proximity_factor**|Предопределенное значение отсутствует. Соответствует полю `proximity_factor` для `options` при отправке запроса на построение маршрутов. Подробнее см. в разделе [Устойчивые к изменению окон доставки маршруты](https://yandex.ru/routing/doc/vrp/concepts/planning-proximity.html).
**Использовать группы балансировки**|Предопределенное значение: `Да`. Определяет, используются ли в решении группы балансировки (в модуле — справочник **Группы балансировки**). При включенной опции в запрос на маршрутизацию для `options` вставляется блок `balanced_groups`. Подробнее см. в разделе [Опция равномерной загрузки](https://yandex.ru/routing/doc/vrp/concepts/balanced-groups.html).

## Настройки штрафов для алгоритма

Здесь указываются штрафы для алгоритма (подробнее о нем рассказано в разделе [Как работает алгоритм планирования](https://yandex.ru/routing/doc/vrp/concepts/routing-algorithm_index-page.html)). Штрафы необходимо настраивать в объектах:

- Транспортное средство (на каждой смене),

- Склад,

- Заказы (в **Общих настройках** в параметре **Настройки штрафов для заказов**).

Если используется несколько складов и транспортных средств, с помощью справочника можно задавать для них разные штрафы.

В каждом элементе справочника нужно указывать только допустимые виды штрафов (т. е. применимые для объекта, для которого эти штрафы предполагается использовать).

Вид штрафа |Комментарий| Применимость для склада| Применимость для ТС | Применимость для заказа
:--- |:---|:---|:---|:---
**За факт нарушения временного окна,**<br>**За факт раннего приезда,**<br>**За факт опоздания**|Предопределенное значение: `1000`. Подробнее см. в разделах о штрафах для [заказов](https://yandex.ru/routing/doc/vrp/concepts/properties-of-orders.html#shtrafy-za-narushenie-vremennykh-okon-zakazov), [транспортных средств](https://yandex.ru/routing/doc/vrp/concepts/properties-of-vehicles.html#smeny-raboty-avtomobilia-ili-kurera), [склада](https://yandex.ru/routing/doc/vrp/concepts/properties-of-depot.html#shtrafy-za-narushenie-vremennogo-okna-sklada). Соответствует полям запроса `penalty.out_of_time.fixed`, `penalty.early.fixed`, `penalty.late.fixed`.|Да|Да|Да
**За минуту нарушения временного окна,**<br>**За минуту раннего приезда,**<br>**За минуту опоздания**|Предопределенное значение: `17`. Подробнее см. в разделах о штрафах для [заказов](https://yandex.ru/routing/doc/vrp/concepts/properties-of-orders.html#shtrafy-za-narushenie-vremennykh-okon-zakazov), [транспортных средств](https://yandex.ru/routing/doc/vrp/concepts/properties-of-vehicles.html#smeny-raboty-avtomobilia-ili-kurera), [склада](https://yandex.ru/routing/doc/vrp/concepts/properties-of-depot.html#shtrafy-za-narushenie-vremennogo-okna-sklada). Соответствует полям запроса `penalty.out_of_time.minute`, `penalty.early.minute`, `penalty.late.minute`.|Да|Да|Да
**Штраф за недоставку**|Предопределенное значение: `1000000`. Подробнее см. [Штрафы за невыполнение заказа](https://yandex.ru/routing/doc/vrp/concepts/properties-of-orders.html#shtrafy-za-nevypolnenie-zakaza). Соответствует `penalty.drop` в запросе.|**Нет**|**Нет**|Да
**За факт превышения максимального количества остановок**|Предопределенное значение: `100`. Подробнее см. [Ограничение количества остановок в смене](https://yandex.ru/routing/doc/vrp/concepts/properties-of-vehicles.html#ogranichenie-kolichestva-ostanovok-v-smene). Соответствует `penalty.stop_excess.fixed` в запросе.|**Нет**|Да|**Нет**
**За каждую остановку сверх максимального количества**|Предопределенное значение: `100`. Подробнее см. [Ограничение количества остановок в смене](https://yandex.ru/routing/doc/vrp/concepts/properties-of-vehicles.html#ogranichenie-kolichestva-ostanovok-v-smene). Соответствует `penalty.stop_excess.per_stop` в запросе.|**Нет**|Да|**Нет**
**За факт не достижения минимального количества остановок**|Предопределенное значение: `100`. Подробнее см. [Ограничение количества остановок в смене](https://yandex.ru/routing/doc/vrp/concepts/properties-of-vehicles.html#ogranichenie-kolichestva-ostanovok-v-smene). Соответствует `penalty.stop_lack.fixed` в запросе.|**Нет**|Да|**Нет**
**За каждую остановку меньше минимального количества**|Предопределенное значение: `100`. Подробнее см. [Ограничение количества остановок в смене](https://yandex.ru/routing/doc/vrp/concepts/properties-of-vehicles.html#ogranichenie-kolichestva-ostanovok-v-smene). Соответствует `penalty.stop_lack.per_stop` в запросе.|**Нет**|Да|**Нет**
**За факт превышения максимального пробега**|Предопределенное значение: `100`. Подробнее см. [Максимальный пробег за смену](https://yandex.ru/routing/doc/vrp/concepts/properties-of-vehicles.html#maksimalnyi-probeg-za-smenu). Соответствует `penalty.max_mileage.fixed` в запросе.|**Нет**|Да|**Нет**
**За каждый километр превышения максимального пробега**|Предопределенное значение: `100`. Подробнее см. [Максимальный пробег за смену](https://yandex.ru/routing/doc/vrp/concepts/properties-of-vehicles.html#maksimalnyi-probeg-za-smenu). Соответствует `penalty.max_mileage.km` в запросе.|**Нет**|Да|**Нет**

## Склады

Поле |Описание
:--- |:---
**Код**|Идентификатор склада. Соответствует полю `id` для `depot` в запросе на маршрутизацию.
**Работает**|Укажите `Да`, чтобы использовать этот склад в модуле.
**Наименование**|Наименование склада. Соответствует полю `ref` для `depot`.
**Адрес**| Необязательное информационное поле.
**Склад 1С**|Устанавливает соответствие склада в модуле значению из стандартного справочника складов в 1С. Если установлено, в рабочем месте логиста фильтруются только заказы с указанного склада.
**Широта, Долгота**|[Координаты склада](https://yandex.ru/routing/doc/vrp/concepts/properties-of-depot.html#koordinaty-sklada). Соответствует полям `point.lon` и `point.lat` для `depot`.
**Временное окно**|[Временное окно работы склада](https://yandex.ru/routing/doc/vrp/concepts/properties-of-depot.html#vremennoe-okno-sklada). Соответствует полю `time_window` для `depot`. Заполнять нужно в [относительном формате](https://yandex.ru/routing/doc/vrp/concepts/properties-of-time-window.html#otnositelnyi-format-vremennykh-okon) с учетом сдвига от даты планирования. Например, `0.20:00:00 - 1.06:00:00` — это промежуток с 20 часов текущего дня до 6 утра следующего дня (отсчет ведется от даты планирования).
**Жесткое временное окно**|Жесткость [временного окна склада](https://yandex.ru/routing/doc/vrp/concepts/properties-of-depot.html#vremennoe-okno-sklada). Соответствует полю `hard_window` для `depot`.
**Сервисное время в начале рейса**,<br>**Сервисное время в конце рейса**| Время, которое добавляется в начале/конце каждого рейса (в случае возврата на склад). Подробнее см. [Сервисное время на складе](https://yandex.ru/routing/doc/vrp/concepts/properties-of-depot.html#servisnoe-vremia-na-sklade). Соответствуют полям `service_duration_s` и `finish_service_duration_s` для `depot`.
**Гибкое время старта**|Определяет, должно ли [время старта](https://yandex.ru/routing/doc/vrp/concepts/properties-of-depot.html#gibkoe-vremia-starta) рассчитываться алгоритмом или оно совпадает с началом временного окна смены или склада. Соответствует полю `flexible_start_time` для `depot`.
**Штрафы**|Ссылка на элемент справочника **Настройки штрафов для алгоритма**. Соответствует полям `depot` при отправке запроса на построение маршрутов:<ul><li>penalty.early.fixed</li><li>penalty.early.minute</li><li>penalty.late.fixed</li><li>penalty.late.minute</li><li>penalty.out_of_time.fixed</li><li>penalty.out_of_time.minute</li><ul>

## Транспортные средства

Поле |Описание
:--- |:---
**Наименование**|[Наименование транспортного средства](https://yandex.ru/routing/doc/vrp/concepts/properties-of-vehicles.html#identifikator-avtomobilia). Соответствует полю `ref` для `vehicle`.
**Работает**|Укажите `Да`, чтобы использовать данное транспортное средство в модуле.
**Номер машины (логин курьера)**|[Идентификатор транспортного средства](https://yandex.ru/routing/doc/vrp/concepts/properties-of-vehicles.html#identifikator-avtomobilia). Соответствует полю `id` для `vehicle`.<br>В Мониторинге поле используется как логин в мобильном приложении.
**Номер телефона**|Необязательное информационное поле.
**Способ перемещения**|Возможные значения: `Автомобиль`, `Грузовой автомобиль`, `Пешком`, `Общественный транспорт`. Соответствует полю `routing_mode` для `vehicle`. Подробнее см. [Режим маршрутизации](https://yandex.ru/routing/doc/vrp/concepts/properties-of-vehicles.html#rezhim-marshrutizatsii).

**Вкладка Параметры**

Поле |Описание
:--- |:---
**Количество мест**|[Вместимость ТС](https://yandex.ru/routing/doc/vrp/concepts/properties-of-vehicles.html#vmestimost-avtomobilia-ili-kurera) по количеству грузовых мест. Соответствует полю `units` для `vehicle.capacity`.
**Грузоподъемность, кг**|[Грузоподъемность ТС](https://yandex.ru/routing/doc/vrp/concepts/properties-of-vehicles.html#vmestimost-avtomobilia-ili-kurera). Соответствует полю `weight_kg` для `vehicle.capacity`.
**Максимальная длина груза, м**<br>**Максимальная ширина груза, м**<br>**Максимальная высота груза, м**<br>|[Габариты кузова ТС](https://yandex.ru/routing/doc/vrp/concepts/properties-of-vehicles.html#vmestimost-avtomobilia-ili-kurera). Вместимость ТС по объему будет вычисляться как произведение данных полей.<br>Соответствует полям `depth_m`, `width_m`, `height_m` для `vehicle.capacity.volume`.
**Стоимость за км,**<br>**Стоимость за час,**<br>**Фиксированная стоимость,**<br>**Стоимость за рейс,**<br>**Стоимость за заказ**|[Стоимость использования ТС](https://yandex.ru/routing/doc/vrp/concepts/properties-of-vehicles.html#stoimost-avtomobilia-ili-kurera) (необходима для алгоритма оптимизации). Соответствует полям `km`, `hour`, `fixed`, `run`, `location` для `vehicle.cost`.
**Максимальное количество рейсов**|[Максимальное количество рейсов ТС](https://yandex.ru/routing/doc/vrp/concepts/properties-of-vehicles.html#neskolko-reisov-avtomobilia-v-den). Соответствует полю `max_runs` для `vehicle`.
**Старт не на складе**|Если курьер стартует не со склада, укажите `Да`. Подробнее см. [Старт автомобиля не со склада](https://yandex.ru/routing/doc/vrp/concepts/properties-of-vehicles.html#start-avtomobilia-ne-so-sklada).
**Заехать на склад после точки старта**|Если курьеру после старта не на складе нужно заехать на склад, укажите `Да`. Подробнее см. [Посещение склада перед началом рабочего дня](https://yandex.ru/routing/doc/vrp/concepts/properties-of-vehicles.html#poseshchenie-sklada-pered-nachalom-rabochego-dnia).
**Временное окно точки старта**|Если **Старт не на складе** = `Да`, укажите в этом поле временное окно, когда можно стартовать (для точки старта в запросе на маршрутизацию передается отдельный `location` c типом `garage`).
**Широта точки старта,**<br>**Долгота точки старта**|Если **Старт не на складе** = `Да`, в этих полях укажите координаты точки старта (для точки старта в запросе на маршрутизацию передается отдельный `location` c типом `garage`).
**Завершение не на складе**|Если курьер завершает маршрут не на складе,  включите эту опцию. Подробнее см. [Возврат на произвольную точку в конце маршрута](https://yandex.ru/routing/doc/vrp/concepts/properties-of-vehicles.html#vozvrat-na-proizvolnuiu-tochku-v-kontse-marshruta).
**Возврат на склад**|Если курьеру нужно вернуться на склад в конце маршрута, включите эту опцию. Подробнее см. [Возврат на склад в конце рабочего дня](https://yandex.ru/routing/doc/vrp/concepts/properties-of-vehicles.html#vozvrat-na-sklad-v-kontse-rabochego-dnia). Если одновременно включены **Завершение не на складе** и **Возврат на склад**, то курьер вернется сначала на склад, а затем — в точку завершения маршрута.
**Временное окно точки завершения**|Если **Завершение не на складе** = `Да`, укажите временное окно, когда можно вернуться в точку завершения (для точки завершения в запросе на маршрутизацию передается отдельный `location` c типом `garage`).
**Широта точки завершения,**<br>**Долгота точки завершения**|Если **Завершение не на складе** = `Да`, укажите координаты точки завершения (для точки завершения в запросе на маршрутизацию передается отдельный `location` c типом `garage`).

**Вкладка Теги**

Поле |Описание
:--- |:---
**Тег**|Ссылка на элемент справочника **Теги (совместимость заказов и ТС)**. Может быть задано несколько элементов. Подробнее см. [Теги автомобиля](https://yandex.ru/routing/doc/vrp/concepts/properties-of-vehicles.html#tegi-avtomobilia). Соответствует полю `tags` для `vehicle`.


**Вкладка Смены**

Поле |Описание
:--- |:---
**Номер**|Соответствует полю `id` для элемента `vehicle.shifts`. Для одного ТС может быть задано несколько смен.
**Штрафы**|Ссылка на элемент справочника **Настройки штрафов для алгоритма**. Соответствует полям `vehicle.shifts` при отправке запроса на построение маршрутов:<ul><li>`penalty.early.fixed`</li><li>`penalty.early.minute`</li><li>`penalty.late.fixed`</li><li>`penalty.late.minute`</li><li>`penalty.out_of_time.fixed`</li><li>`penalty.out_of_time.minute`</li><li>`penalty.max_mileage.fixed`</li><li>`penalty.max_mileage.km`</li><li>`penalty.stop_excess.fixed`</li><li>`penalty.stop_excess.per_stop`</li><li>`penalty.stop_lack.fixed`</li><li>`penalty.stop_lack.per_stop`</li></ul>
**Группа балансировки**|Ссылка на элемент справочника **Группа балансировки**. Заполните, если для ТС нужна [равномерность маршрутов](https://yandex.ru/routing/doc/vrp/concepts/balanced-groups.html). Соответствует полю `balanced_group_id` для элемента `vehicle.shifts`.
**Временное окно**|Соответствует полю `time_windows` для элемента `vehicle.shifts`. Подробнее см. [Смены работы автомобиля или курьера](https://yandex.ru/routing/doc/vrp/concepts/properties-of-vehicles.html#smeny-raboty-avtomobilia-ili-kurera).
**Жесткое временное окно**|Соответствует полю `hard_windows` для элемента `vehicle.shifts`. Подробнее см. [Смены работы автомобиля или курьера](https://yandex.ru/routing/doc/vrp/concepts/properties-of-vehicles.html#smeny-raboty-avtomobilia-ili-kurera).
**Минимальное количество стопов**|Соответствует полю `minimal_stops` для элемента `vehicle.shifts`. Подробнее см. [Ограничение количества остановок в смене](https://yandex.ru/routing/doc/vrp/concepts/properties-of-vehicles.html#ogranichenie-kolichestva-ostanovok-v-smene).
**Максимальное количество стопов**|Соответствует полю `maximal_stops` для элемента `vehicle.shifts`. Подробнее см. [Ограничение количества остановок в смене](https://yandex.ru/routing/doc/vrp/concepts/properties-of-vehicles.html#ogranichenie-kolichestva-ostanovok-v-smene).
**Максимальный пробег, км**|Соответствует полю `max_mileage_km` для элемента `vehicle.shifts`. Подробнее см. [Максимальный пробег за смену](https://yandex.ru/routing/doc/vrp/concepts/properties-of-vehicles.html#maksimalnyi-probeg-za-smenu).
**Максимальная продолжительность смены, с**|Соответствует полю `max_duration_s` для элемента `vehicle.shifts`. Подробнее см. [Максимальная продолжительность смены](https://yandex.ru/routing/doc/vrp/concepts/properties-of-vehicles.html#maksimalnaia-prodolzhitelnost-smeny).


## Группы балансировки

Предопределены 2 группы балансировки с одинаковыми настройками: `Группа 1` и `Группа 2`. Если нет необходимости использовать группы балансировки, на сменах транспортных средств их можно не указывать.

Поле |Описание
:--- |:---
**ID группы балансировки**|Идентификатор группы. Указывается на сменах тех ТС, которые нужно [балансировать по времени/количеству остановок](https://yandex.ru/routing/doc/vrp/concepts/balanced-groups.html).
**Штраф за отклонение от среднего времени маршрута**|Предопределенное значение: `200`. Если не нужно балансировать по продолжительности маршрута, укажите `0`.
**Штраф за отклонение от среднего количества остановок**|Предопределенное значение: `100`. Если не нужно балансировать по количеству остановок, укажите `0`.

## Теги (совместимость заказов и ТС)

Поле |Описание
:--- |:---
**Наименование**|Cправочник в дальнейшем можно использовать для транспортного средства. На заказах теги нужно заполнять вручную в Рабочем месте логиста в поле **Необходимые свойства машины** (либо доработать автоматизированное заполнение тегов для заказов). Подробнее см. [Теги автомобиля](https://yandex.ru/routing/doc/vrp/concepts/properties-of-vehicles.html#tegi-avtomobilia).


## Запросы на маршрутизацию

Здесь представлена история запросов к сервису маршрутизации из модуля. Может содержать несколько статусов по каждому уникальному ID задачи.

При нажатии на кнопку **Результат планирования** выполнится переход в Рабочее место логиста.

Поле |Описание
:--- |:---
**Период**|Дата и время запроса к сервису планирования.
**Id**|Уникальный идентификатор задачи планирования. Каждая задача представлена ссылкой, при нажатии на которую открывается карта для просмотра результатов решения задачи.
**Сообщение**|Ответ от сервиса планирования маршрутов. Содержит текущий статус решения задачи или текст ответа от сервиса (если возникли ошибки). Сообщения:<ul><li>`Task queued` — для статуса `Отправлен`;</li><li>`Task started and available for polling` или `Task is running and available for polling` — для статуса `Запланирован`;</li><li>`Task successfully completed` — для статуса `Завершен`.</li></ul>
**Статус запроса**|Возможные значения: `Отправлен`, `Запланирован`, `Завершен`, `Ошибка`.