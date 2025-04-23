# RegionAsync

[Документация](https://github.yandex-team.ru/pages/market/user-region-async/index.html)

Компонент для [nodules-user](https://github.yandex-team.ru/nodules/user), созданный на основе текущей версии [region](https://github.yandex-team.ru/nodules/user/blob/master/components/region.js) и [этого коммита](https://github.yandex-team.ru/nodules/user/commit/4f896b698528ff9798dee29aa28a0c53c25de74c).

Предоставляет асинхронный интерфейс и возможность инжектить инициализированный инстанс [node-geobase](https://github.yandex-team.ru/varankinv/node-geobase). Для полу-синхронной работы с регионом, предусмотрен метод `ensureProps`.

## Архитектура
![Architecture img](img/architecture.png)

### nodules-user
[Репозиторий](https://github.yandex-team.ru/nodules/user)  
Базовый модуль для получения информации о пользователе, его регионе, браузере и l10n-параметрах.

### node-geobase
[Репозиторий](https://github.yandex-team.ru/varankinv/node-geobase Репозиторий)  
Клиент для геобазы, реализующий механизм драйверов. Абстрагирует работу с разными имплементациями геобазы.

### geobase-remote-driver
[Репозиторий](https://github.yandex-team.ru/varankinv/geobase-remote-driver Репозиторий)  
Драйвер для node-geobase. Работает с удаленным vertis-geobase по протоколу TCP.

### geobase-native-driver
[Репозиторий](https://github.yandex-team.ru/varankinv/geobase-native-driver Репозиторий)  
Драйвер для node-geobase. Является оберткой над нативными биндингами для Node.js.

### vertis-geobase
[Репозиторий](https://github.yandex-team.ru/vertis/vertis-geobase Репозиторий)  
[Кондуктор](https://c.yandex-team.ru/packages/yandex-vertis-geobase)  
Надстройка над geobaas-server. Запускает воркеры с помощью luster, настраивает логирование. Дает возможность задавать конфиги для разных сред окружения (dev, prod и т. д.). Устанавливается как Debian-пакет.

### geobaas-server
[Репозиторий](https://github.yandex-team.ru/varankinv/geobaas-server Репозиторий)  
Локальный сервис, предоставляющий SaaS-like интерфейс к libgeobase4 по TCP.

### Биндинги (geobase4)
[Документация](https://doc.yandex-team.ru/face/libgeobase/concepts/interfaces-nodejs.xml)

### Геобаза
[Документация](https://doc.yandex-team.ru/face/libgeobase/concepts/about.xml)

## Инициализация
```javascript
// ... инициализация lookup (node-geobase), конфига для nodules-user
config.regionAsync = {
    driver: lookup // инстанс node-geobase
}
// стандартная регистрация и инициализация компонента для nodules-user
User.registerComponent('regionAsync', RegionAsync);
var user = new User(request, response, config)
    .init('auth')
    .then(function (user) {
        return user.init('regionAsync');
    }).then(function (user) {
        // можно работать с user.regionAsync;
    });
```

## Метод `ensureProps`
Обеспечивает синхронный доступ к переданным свойствам. Данные запрашивает из геобазы для текущего определившегося id региона. Повторный запрос одних и тех же свойств не делает, но можно дозапрашивать новые. В случае смены id региона (например, с помощью `setId`) — сбросит кеш свойств и будет запрашивать заново.

Доступные свойства для инициализации через `ensureProps`:
- **name**
- **names**
- **isInternalNetwork**
- **linguistics**
- **country**
- **info**
- **timezone**

Пример использования:
```javascript
user.regionAsync.ensureProps(
    'country',
    'linguistics'
).then(function(region) {
    // далее работа как с синхронной версией
    console.log(region.linguistics);
    console.log(region.timezone);
    console.log(region.info);
});

// ... позднее в коде (после завершения предыдующих операций)
user.regionAsync.ensureProps(
    'country', // уже было запрошено, запрос не произойдет
    'linguistics', // тоже уже было запрошено
    'timezone' // сделает запрос и сохранит
);

// ... 
user.regionAsync.setId(143).then(function() {
    // изменен id - запрашиваем данные заново
    user.regionAsync.ensureProps(
        'country',
        'linguistics',
        'timezone'
    );
});
```
Если не передавать имена свойств в метод, то он проинициализирует все доступные свойства
```javascript
user.regionAsync.ensureProps().then(function(region) {
    console.log(region.name);
    console.log(region.names);
    console.log(region.isInternalNetwork);
    console.log(region.linguistics);
    console.log(region.country);
    console.log(region.info);
    console.log(region.timezone);
});
```

## Документация по API
Чтобы сгенерировать HTML-документацию в папку docs:  
```npm run docs```
