# API constructor.show

constructor.show - это модуль, который помогает отобразить данные из конструктора на карте.
Модуль не будет менять состояние карты (устанавливать центр, зум, менять тип подложки и т.п.)

Модуль получает на вход карту и данные карты из конструктора.
Сейчас ожидаемый формат данных карты соответствует результату работы ручки contructor-int#v1.
Этот формат данных содержит всю информацию о карте - состояние и все геобъекты.
../docs/v1/spec.yaml#L23

В будущем интерфейс constructor.show будет расширен. Вместо данных можно будет передавать только sid карты.
Загрузка информации о геообъектах будет производиться самостоятельно.
Для установки состояния карты все равно нужно будет использовать данные запроса contructor-int#v2
../docs/v1/spec.yaml#L23

В будущем планируется поддерживать обратную совместимость в модуле. Поэтому почти все методы сейчас асинхронные.

## Подключение модуля
endpoint, который возвращает модуль принимает на вход один GET-параметр - ns.
Это пространство имен API Яндекс.Карт, в котором нужно инициализировать модуль.
```
https://api01e.tst.maps.yandex.ru/services/constructor/1.0/show/?ns=myNS
```
Если его опустить, то будет использовать пространство имен "ymaps".
После подключения необходимо вызвать инициализацию самого модуля в API.
```
myNS.modules.require('constructor.show' ...
```

## Интерфейс модуля
Модуль представляет из себя функцию, которая принимает на вход карту и данные карты.
```
// Инициализация модуля
customNS.modules.require('constructor.show', function (show) {
    // Передаем в модуль карту и данные карты
    show(myMap, mapData).then(function (shower) {
        // ...
    });
});
```

### selectObject
Метод производит выбор объекта на карте. По умолчанию происходит центрирование карты, а после открытие балуна, если объект не попадает (или частично попадает) в текущую видимую область.
Балун не будет открыт, если у объекта нет данных. Но состоятие карты будет применено.
```
shower.selectObject('123').then(function (data) {
    // data.status === 'balloonWasOpened' Был открыт балун объекта на карте
    // data.status === 'mapStateWasApplied' Было произведено только лишь центрирование карты
    console.log(
        data.status
    );
}, function (error) {

});
```

### Отслеживание выделение объекта
Выделение объекта на карте можно производить через поля selectedObjectId и objectWithBalloonId в состоянии объекта.
selectedObjectId - произошел клик по объекту на карте/вызов метода selectObject.
objectWithBalloonId - произошло открытие балуна объекта на карте.
```
// Слушаем поле 'objectWithBalloonId' в состоянии
var monitor = new customNS.Monitor(shower.state);
monitor.add('selectedObjectId', function (value) {
    // id выделенного объекта
    console.log(value);
});
monitor.add('objectWithBalloonId', function (value) {
    // id объекта с балуном
    console.log(value);
});
```

### destroy
Уничтожение объекта-show
```
shower.destroy();
```

### Полный пример
```
myNS.modules.require('constructor.show', function (show) {
    show(myMap, mapData).then(function (shower) {

        shower.selectObject('123');

        var monitor = new myNS.Monitor(shower.state);
        monitor.add('objectWithBalloonId', function (value) {
            console.log(value);
            shower.destroy();
        });
    });
});
```
