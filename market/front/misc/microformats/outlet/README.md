# Микроформат точки на карте
Тут содержится вся информация о точке на карте

Инлет -- пункт приема товара от магазина. Относится к почте России. Из инлета возят товар в течение 1 рабочего дня в соответствующий аутлет.

В поле "inletId" выводится идентификатор инлета из которого привезли товар в аутлет.

В поле "inletShipmentDay" выводится день отгрузки товара из инлета почты России для доставки в аутлет почты России. Выводится только для аутлетов почты России.

Добавлено поле "purpose", которое может содержать все виды уникальных назначений аутлета. "mixed" значение запрещено, т.к. может быть представлено как "pickup", "store".
Со временем "purpose" будет использоваться вместо "type"

Добавлено поле serviceId. Это идентификатор сервиса, к которому принадлежит аутлет.
