# Общая информация

Чтобы начать планировать маршруты, определите склад, автомобили и заказы для одного интервала планирования.

В результате планирования вы получите оптимальные маршруты автомобилей, и метрики для анализа результатов.

Ниже мы рассмотрим основные свойства склада, автомобилей и заказов, и продемонстрируем их использование на реальном примере.

Более подробно о свойствах и частных случаях оптимизации вы можете узнать далее в главах [Свойства временных окон](properties-of-time-window.md), [Свойства веса и объема](properties-of-weight.md), [Cвойства автомобилей](properties-of-vehicles.md) и [Свойства заказов](properties-of-orders.md).

## Склад
Склад — это точка, в которой начинаются и могут заканчиваться все маршруты. На складе происходит загрузка заказов в автомобили. В одном запросе можно указать только один склад. У склада должно быть указано время работы.
Подробное описание параметров доступно в разделе [Свойства складов](properties-of-depot.md).

Параметры складов задаются в поле `depot`.

## Автомобили
Доставка заказов может выполняться как обычными автомобилями, так и курьерами, передвигающимися пешком или на общественном транспорте. Автомобиль и курьер имеют общий набор свойств.

Параметры автомобилей или курьеров задаются в поле `vehicles`.

## Грузоподъемность автомобиля
У автомобиля можно определить емкость или грузоподъемность. Их желательно указать в запросе. В противном случае, Маршрутизатор может построить маршруты, в которых автомобили будут перегружены.

Параметры вместимости и грузоподъемности задаются в поле `vehicle.capacity`.

## Заказы
Заказы это точки, в которые необходимо доставить груз. Для каждого заказа необходимо указать его географические координаты, а также временное окно.

Параметры заказов задаются в поле `locations`.

## Координаты заказа
Местоположение заказа задается в виде географических координат, соответствующих точке парковки или остановки на адресе заказа.

Если местоположение заказа в вашей системе задается адресом, необходимо произвести [геокодирование](https://tech.yandex.ru/maps/geocoder/) (преобразование адреса из текста в географические координаты).

Параметры координат заказа задаются в поле `location.point`.

## Временное окно заказа
Всем заказам нужно указать временное окно — интервал времени, когда автомобиль или курьер должен прибыть на адрес заказа.

Параметры временных окон заказа задаются в поле `location.time_window`.

## Сервисное время заказа
Для каждого заказа может быть определено время на его вручение клиенту. Это время включает в себя любые операции, которые автомобиль или курьер выполняет после прибытия на адрес заказа, до момента отъезда на следующий заказ, например вручение заказа клиенту.

Cервисное время задается в поле `location.service_duration_s`, в секундах.

## Вес заказа
Для каждого заказа можно указать его вес. Определение веса не обязательно, но рекомендуется чтобы избегать перегрузки автомобилей.

Веса заказ задается в поле `location.shipment_size`.

## Маршруты
Результатом работы сервиса являются маршруты — последовательности посещения заказов для каждой машины с прогнозом времени прибытия на каждый заказ.

В ответе сервиса маршруты указаны в поле `routes`.

## Метрики
В дополнение к оптимизированным маршрутам, в ответе сервиса будут метрики для анализа эффективности планирования. Например, предоставляется суммарное расстояние и время маршрутов, количество и абсолютное время опозданий, и другие.

Метрики рассчитываются как для всех маршрутов вместе, так и для каждого по отдельности, и указываются в поле ответа `metrics`.

## Cтоимость маршрутов
Оптимизация минимизирует стоимость маршрутов. Стоимость складывается из следующих параметров:

 - сумма стоимости всех автомобилей (в рублях за километр, час, и факт использования автомобиля),
 - сумма штрафов за нарушение бизнес-ограничений (штрафы за невыполнение заказа, за нарушение временных окон и другие).

Стоимость рассчитываются как для всех маршрутов вместе, так и для каждого в отдельности, и указывается в поле ответа `metrics`.


<p class="p"><a href="feedback.html" class="xref button">Написать в службу поддержки</a></p>
