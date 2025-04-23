# Турбо-приложение для Заправок

Ссылки:

-   [Описание API есть в сценарии в PDF](https://st.yandex-team.ru/TAP-763/attachments/16902872/)
-   [Использование API в мобильном SDK](https://bb.yandex-team.ru/projects/TANKER/repos/tanker-android-navigator/browse/sdk/src/main/java/ru/tankerapp/android/sdk/navigator/services/client/ClientApi.kt/)
-   [Графики балансера – тестинг](https://yasm.yandex-team.ru/template/panel/tap/upstream=refuel-testing-total/)
-   [Графики балансера – продакшн](https://yasm.yandex-team.ru/template/panel/tap/upstream=refuel-total/)

Окружения:

-   [Тестинг](https://refuel.tap-tst.yandex.ru/) (собирается автоматически из мастера)
-   [Релизный стенд](https://refuel.tap-rc.yandex.ru/) (собирается автоматически для релизной ветки)
-   [Продакшн](https://refuel.tap.yandex.ru/) (выкатывается релиз-инженером вручную)

## Запуск

Устанавливаем зависимости:

```bash
npx lerna bootstrap --scope @yandex-int/turboapp-refuel --include-filtered-dependencies
```

Для локальной разработки запускаем скрипт:

```bash
npx lerna run start --scope @yandex-int/turboapp-refuel --stream
```

Открыть приложение можно по ссылке [http://localhost:3000](http://localhost:3000).

Приложение автоматически перезапустится при изменениях в коде.
Ошибки линтинга можно увидеть в консоли.

Для тестирования вне платформы турбоаппов можно получить авторизационный токен по [ссылке](https://oauth.yandex.ru/authorize?response_type=token&client_id=9e445c9aacec4266bf265302facb8293). 
После разрешения доступа приложению MiniApp Example произойдет редирект, в урле будет находиться токен.

## Команды

-   `npm start` – запуск приложения в режиме разработки
-   `npm run build` – сборка production версии приложения

## Разработка

-   [Подробнее про стор](./src/redux/README.md)
-   Документация по [Create React App](https://facebook.github.io/create-react-app/docs/getting-started).
-   Документация по [React](https://reactjs.org).

## Мониторинг ошибок

-   [Проект в Error Booster](https://error.yandex-team.ru/projects/turboapp-refuel/projectDashboard)
-   [Ошибки в проде за последний час](https://error.yandex-team.ru/projects/turboapp-refuel/projectDashboard?filter=environment%20==%20production&period=hour)
-   [Конфиг алертов](https://error.yandex-team.ru/projects/turboapp-refuel/settings/alerts)
-   [Настройки уведомлений](https://juggler.yandex-team.ru/notification_rules/?query=namespace%3DTAP)

## Сценарий предоплаты

### Общий сценарий
1. Водитель выбирает АЗС на карте, либо автоматически открывается АЗС по геолокации пользователя. На карте можно увидеть все АЗС во всех городах.
2. Нажимает кнопку «Заправиться»
3. Выбирает номер колонки из списка
4. Выбирает тип топлива из списка, количество топлива или сумму, метод оплаты
5. Жмет «Оплатить»
6. Создается заказ, проходит оплата
7. Заправляется топливо, сопровождается анимацией наполнения бака, бегущей стоимостью и литрами как на колонке
8. После заправки показывается чек и предложение оценить сервис
9. Водитель жмет «Закрыть» и попадает снова на карту в п.1

### Создание заказа

Заказ создается с помощью метода [POST /order/create/v2](https://bb.yandex-team.ru/projects/TANKER/repos/tanker-android-navigator/browse/sdk/src/main/java/ru/tankerapp/android/sdk/navigator/services/client/ClientApi.kt#29). Важно: данные отправляются ввиде `form-data`, поэтому при `fetch`'е важно указать заголовок `Content-Type: application/x-www-form-urlencoded`.

Информацию о заправочной станции можно получить через запрос `GET /station/item?id=${id}`, где `id` - идентификатор заправочной станции. Ответ включает в себя информацию о колонках выбранной заправочной станции.

Доступные в колонке топлива и их цены за литр могут быть получены с помощью запроса `GET /order/offers/v2` со следующими параметрами:

-   `orderId` - создается на клиенте, представляет собой uuid без минусов (отсутствие минусов обязательно);
-   `orderType` - тип единиц измерения ([Money, Litres, Full tank](https://bb.yandex-team.ru/projects/TANKER/repos/tanker-android-navigator/browse/sdk/src/main/java/ru/tankerapp/android/sdk/navigator/models/data/OrderType.kt#5));
-   `orderVolume` - количество единиц заказа;
-   `stationId` - `id` заправочной станции;
-   `columnId` - `id` колонки;
-   `lat`, `lon` - широта и долгота по геолокации.

Для создания заказа необходимы следующие параметры:

-   `orderId` - создается на клиенте, представляет собой uuid без минусов (отсутствие минусов обязательно);
-   `orderType` - тип единиц измерения ([Money, Litres, Full tank](https://bb.yandex-team.ru/projects/TANKER/repos/tanker-android-navigator/browse/sdk/src/main/java/ru/tankerapp/android/sdk/navigator/models/data/OrderType.kt#5));
-   `orderVolume` - количество единиц заказа;
-   `stationId` - `id` заправочной станции;
-   `columnId` - `id` колонки;
-   `fuelId` - `id` топлива;
-   `paymentId` - `id` способа оплаты (приходит в ответе от `GET /user/payment`);
-   `billingPayType` - тип оплаты (приходит в ответе от `GET /user/payment`);
-   `lat`, `lon` - широта и долгота по геолокации;
-   `accuracy` - точность геолокации.

После создания заказа, с периодом в 5 секунд происходит запрос в `GET /order/status?orderId=${orderId}` с `id` заказа. Важно: в разные стадии заказа ручка возвращает разные ответы:

-   Сразу после создания заказа, до начала заправки:

```json
{
    "data": {
        "status": 20,
        "date": "2020-03-30T13:24:08.3601382Z"
    },
    "description": "Оставайтесь в машине, заправка сейчас начнется",
    "availableBalance": 0.0
}
```

-   Во время заправки:

```json
{
    "data": {
        "status": 30,
        "date": "2020-03-30T13:24:11.8031489Z"
    },
    "volume": 6.66,
    "volumeSpeed": 0.025,
    "volumeMax": 18.97
}
```

-   После окончания заправки:

```json
{
    "data": {
        "status": 50,
        "date": "2020-03-30T13:24:45.197Z"
    },
    "description": "Заправлено: 18,97 л на сумму 849,67 ₽",
    "availableBalance": 0.0,
    "order": {
        "litreCompleted": 18.97,
        "sumPaidCard": 849.67,
        "sumPaid": 849.67,
        "sum": 849.67,
        "sumPaidCardCompleted": 849.67,
        "sumPaidCompleted": 849.67,
        "priceFuel": 44.79,
        "fuel": {
            "id": "a95",
            "marka": "АИ-95"
        },
        "promoText": "",
        "bill": {
            "rows": [
                {
                    "title": "Оплачено",
                    "description": "849,67 ₽",
                    "type": "Total"
                },
                {
                    "type": "Separator"
                },
                {
                    "title": "Заправка",
                    "description": "849,67 ₽"
                },
                {
                    "type": "Separator"
                },
                {
                    "title": "Топливо",
                    "description": "АИ-95",
                    "type": "Total"
                },
                {
                    "type": "Separator"
                },
                {
                    "title": "Колонка",
                    "description": "№1"
                },
                {
                    "type": "Separator"
                },
                {
                    "title": "Цена за 1 л",
                    "description": "44,79 ₽"
                },
                {
                    "type": "Separator"
                },
                {
                    "title": "Количество",
                    "description": "18,97 л"
                },
                {
                    "type": "Separator"
                },
                {
                    "title": "Дата",
                    "description": "30 марта 2020 в 16:24 МСК"
                },
                {
                    "type": "Separator"
                },
                {
                    "title": "Время заправки",
                    "description": "42 сек"
                },
                {
                    "type": "Separator"
                },
                {
                    "title": "Удачной дороги!",
                    "type": "Center"
                }
            ]
        },
        "banner": {
            "darkUrl": "https://tanker.s3.yandex.net/gasstaions.png",
            "lightUrl": "https://tanker.s3.yandex.net/gasstaions.png",
            "clickUrl": "https://937662.redirect.appmetrica.yandex.com/?appmetrica_tracking_id=674911232079210781"
        },
        "tips": {
            "items": [
                {
                    "title": "0 ₽"
                },
                {
                    "title": "8 ₽",
                    "value": 1.0
                },
                {
                    "title": "16 ₽",
                    "value": 2.0
                },
                {
                    "title": "25 ₽",
                    "value": 3.0
                },
                {
                    "title": "42 ₽",
                    "value": 5.0
                },
                {
                    "title": "59 ₽",
                    "value": 7.0
                }
            ]
        }
    }
}
```

В последнем ответе поллинга приходит вся информация о заказе, включающая полную сумму оплаты, объем заправленного топлива и время заправки.
