# Киперы для компонентов

## Описание

[Base Context](https://a.yandex-team.ru/arc_vcs/portal/avocado/morda-go/pkg/contexts/base.go?rev=r9651790#L9) - это интерфейс доступа
к компонентам, которые вычисляются от параметров запроса. Он вычисляется на каждый запрос и передается между узлами аппхоста.
Кипер реализует часть интерфейса Base Context, связанную с отдельным компонентом. Для каждого компонента, доступного через
Base Context, есть кипер. Киперы реализованы в отдельных пакетах папки [libs/utils](https://a.yandex-team.ru/arc_vcs/portal/avocado/libs/utils),
которые названы аналогично соответствующим компонентам.

{% cut "Пример" %}
> Возьмем для примера простой компонент - Device. Интерфейс доступа к нему выглядит [вот так](https://a.yandex-team.ru/arc_vcs/portal/avocado/morda-go/pkg/contexts/base.go?rev=r9651790#L85).
> Кипер для него реализован в пакете [libs/utils/devices/keeper.go](https://a.yandex-team.ru/arc_vcs/portal/avocado/libs/utils/devices/keeper.go?rev=r9651790).
>
{% endcut %}

Мы стараемся делать все киперы по одной схеме.
У каждого кипера есть публичные методы: **конструктор**, **Get-методы**, **методы переопределения кеша**,
и приватные поля: **cached** и **cacheUpdated**.

### Конструктор
Конструктор возвращает указатель на приватную структуру. Указатель нужен для того, чтобы в методах кипера иметь возможность модифицировать приватные поля - *cached* и флаг *cacheUpdated*.
Аргументы конструктора - DTO (Data Transfer Object) компонента и компоненты, необходимые для вычисления.
В кеше *cached* хранится указатель на модель, полученную из DTO. Он может быть пустым и содержать nil.

{% cut "Пример" %}
> [конструктор для DeviceKeeper](https://a.yandex-team.ru/arc_vcs/portal/avocado/libs/utils/devices/keeper.go?rev=r9651790#L10)
> принимает cache *morda_data.Device, парсер, логгер.
> cache из DTO [преобразуется](https://a.yandex-team.ru/arc_vcs/portal/avocado/libs/utils/devices/keeper.go?rev=r9651790#L14) в указатель на модель.
>
>
>
{% endcut %}

### GetOrErr

Метод GetOrErr возвращает кеш, если он есть, или пытается вычислить компоненту в противном случае.
Возвращает результат и ошибку, если она происходит.

### Get

Метод Get работает аналогично GetOrErr, но не возвращает ошибку наружу, а логирует ее.

### GetIfUpdated

Метод GetIfUpdated возвращает компоненту в виде DTO, если она обновилась с момента создания кипера.
Например, если в конструктор пришел пустой кеш, и компонента вычислилась впервые.
Либо если кеш поменялся другим способом, например методом Force или Clean.

Этот метод применяется, чтобы [записать обновленный кеш](https://a.yandex-team.ru/arc_vcs/portal/avocado/libs/utils/base/context.go?rev=r9661902#L329) в аппхост.

### Force

Метод Force перезаписывает кеш кипера другим значением.
Кипер с методом Force будет частично удовлетворять интерфейсу [ChangeableBase](https://a.yandex-team.ru/arc_vcs/portal/avocado/morda-go/pkg/contexts/base.go?rev=r9651790#L42).

> позже тут появится описание примеров и ссылка на статью про селектор

### Clean

Метод Clean очищает кеш кипера.
Кипер с методом Clean будет частично удовлетворять интерфейсу [CleanableBase](https://a.yandex-team.ru/arc_vcs/portal/avocado/morda-go/pkg/contexts/base.go?rev=r9651790#L59).

> позже тут появится описание примеров и ссылка на статью про использование

### Приватные вспомогательные методы

Для удобной работы с кешем в киперах реализованы методы *getCached* и *setCache*.

{% cut "Пример" %}
> [getCached](https://a.yandex-team.ru/arc_vcs/portal/avocado/libs/utils/devices/keeper.go?rev=r9651790#L69) и [setCache](https://a.yandex-team.ru/arc_vcs/portal/avocado/libs/utils/devices/keeper.go?rev=r9651790#L73) для deviceKeeper
>
{% endcut %}

## Использование

Киперы для компонентов [создаются](https://a.yandex-team.ru/arc_vcs/portal/avocado/libs/utils/base/context.go?rev=r9661902#L199) в начале каждого запроса, для обработки которого нужен BaseContext.
Они собираются в структуру [context](https://a.yandex-team.ru/arc_vcs/portal/avocado/libs/utils/base/context.go?rev=r9661902#L298), которая удовлетворяет интерфейсам
BaseContext, ChangeableBase, CleanableBase.

Некоторые из компонент зависят от других, так что в конструкторы одних киперов могут передаваться другие (через парсер).

{% cut "Пример" %}
> [requestKeeper](https://a.yandex-team.ru/arc_vcs/portal/avocado/libs/utils/base/context.go?rev=r9661902#L202) и [cookieKeeper](https://a.yandex-team.ru/arc_vcs/portal/avocado/libs/utils/base/context.go?rev=r9661902#L199) не зависят от других компонент и вычисляются только по данным исходного запроса.
> [geoKeeper](https://a.yandex-team.ru/arc_vcs/portal/avocado/libs/utils/base/context.go?rev=r9661902#L245) зависит от множества других компонент.
>
{% endcut %}

### Циклические зависимости

Есть случаи, когда между компонентами возникает циклическая зависимость.
Например, друг от друга зависят Geo и MordaZone: MordaZone вычисляется по части Geo,
а другая часть Geo переопределяется в зависимости от MordaZone.
Похожая зависимость (тоже циклическая, но длинная) возникает между MordaZone и Device.

Такие ситуации разрешаются следующим образом:
* сначала создаются киперы для компонент [Geo](https://a.yandex-team.ru/arc_vcs/portal/avocado/libs/utils/base/context.go?rev=r9661902#L245) и [Device](https://a.yandex-team.ru/arc_vcs/portal/avocado/libs/utils/base/context.go?rev=r9661902#L221) (эти киперы пока не зависят от MordaZone).
* создается [парсер](https://a.yandex-team.ru/arc_vcs/portal/avocado/libs/utils/base/context.go?rev=r9661902#L259) и [кипер](https://a.yandex-team.ru/arc_vcs/portal/avocado/libs/utils/base/context.go?rev=r9661902#L262) MordaZone, которые зависят от киперов Geo и Device.
* в конце вызова метода [Parse](https://a.yandex-team.ru/arc_vcs/portal/avocado/libs/utils/mordazone/parser.go?rev=r9652181#L163) парсера MordaZone компоненты Geo и Device [переопределяются](https://a.yandex-team.ru/arc_vcs/portal/avocado/libs/utils/mordazone/parser.go?rev=r9652181#L187) с помощью методов [geoKeeper.OverrideWithMordaZone](https://a.yandex-team.ru/arc_vcs/portal/avocado/libs/utils/geo/keeper.go?rev=r9532648#L64) и [deviceKeeper.SetIsTouchGramps](https://a.yandex-team.ru/arc_vcs/portal/avocado/libs/utils/devices/keeper.go?rev=r9651790#L63).
