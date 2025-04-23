# Nesu
[Документация](https://nesu.tst.vs.market.yandex.net/swagger-ui.html).

## getWarehouses

В стейте объект, ключ: shopId

```
[
    {
        id: 10000481773,
        name: 'Раковый дропшип-склад',
        contact: {
            lastName: 'Тестов',
            firstName: 'Тест',
            middleName: '',
            phoneNumber: '987-789-98-77',
            internalNumber: '221',
        },
        address: {
            geoId: 15,
            region: 'Тульская область',
            locality: 'Тула',
            street: 'Ленина',
            house: '12',
            housing: '',
            building: '',
            apartment: '',
            postCode: '114432',
            comment: 'Ленинский склад',
        },
        schedule: [
            {
                day: 5,
                timeFrom: '09:00:00',
                timeTo: '23:00:00',
            }, {
                day: 4,
                timeFrom: '09:00:00',
                timeTo: '23:00:00',
            }, {
                day: 2,
                timeFrom: '09:00:00',
                timeTo: '23:00:00',
            }, {
                day: 1,
                timeFrom: '09:00:00',
                timeTo: '23:00:00',
            }, {
                day: 3,
                timeFrom: '09:00:00',
                timeTo: '23:00:00',
            },
        ],
    },
]

```

## updateWarehouseUsingPOST
[Документация](https://nesu.tst.vs.market.yandex.net/swagger-ui.html#/shop-warehouse-controller/updateWarehouseUsingPOST)

обновление данных склада

## getLogisticPoints

В стейте массив

```
[
    {
        id: 10000879640,
        partnerId: 100136,
        name: 'Склад СДТ',
        instruction: null,
        address: {
            geoId: 213,
            region: 'Москва',
            subRegion: null,
            locality: 'Москва',
            street: 'Котляковская',
            house: '1с',
            housing: null,
            building: null,
            apartment: null,
            postCode: null,
            comment: null,
        },
        contact: {
            lastName: 'Иванов',
            firstName: 'Иван',
            middleName: 'Иванович',
            phoneNumber: null,
            internalNumber: null,
        },
        schedule: [
            {
                id: 77057365,
                day: 1,
                timeFrom: '10:00:00',
                timeTo: '20:00:00',
            },
        ],
        shipmentType: 'WITHDRAW',
        shipmentSchedule: [
            {
                id: 7,
                day: 1,
                timeFrom: '09:00:00',
                timeTo: '13:00:00',
            },
        ],
    },
]
```

## getPartnerWarehouses

В стейте массив

```
[
    {
        id: 48242,
        marketId: 2013342,
        name: 'DropShip_Пухлая складка',
        readableName: 'Пухлая складка',
        partnerType: 'DROPSHIP',
        logoUrl: null,
        status: 'TESTING',
        flags: {assessedValueTotalCheckNeeded: false, postalCodeNeeded: false},
    },
]
```

## getPartnerCapacity

В стейте объект, ключ - partnerId. Поле partnerId подставляется автоматически

```
{
    capacityService: 'SHIPMENT',
    countingType: 'ORDER',
    day: null,
    deliveryType: null,
    id: 1125,
    locationFrom: 225,
    locationTo: 225,
    partnerId: 48242,
    platformClientId: 1,
    type: 'REGULAR',
    value: 50,
}
```

## getPartnerRelation

В стейте объект, ключ - partnerId

```
{
    fromPartner: {
        id: 48242,
        marketId: 2013342,
        name: 'DropShip_Пухлая складка',
        readableName: 'Пухлая складка',
        partnerType: 'DROPSHIP',
        logoUrl: null,
        status: 'TESTING',
        capacities: [
            {
                id: 1125,
                partnerId: 48242,
                locationFrom: 225,
                locationTo: 225,
                deliveryType: null,
                type: 'REGULAR',
                countingType: 'ORDER',
                platformClientId: 1,
                day: null,
                value: 50,
            },
        ],
        handlingTimes: [
            {
                id: 402,
                partnerId: 48242,
                locationFrom: 225,
                locationTo: 225,
                handlingTimeDays: 1,
            },
        ],
    },
    toPartner: {
        id: 1005117,
        marketId: 1005117,
        name: 'СДТ',
        readableName: 'СДТ',
        partnerType: 'DELIVERY',
        logoUrl: 'uuuurl',
        status: 'ACTIVE',
        capacities: [],
        handlingTimes: [],
    },
    toPartnerLogisticsPoint: {
        id: 10000879557,
        partnerId: 1005117,
        name: 'Склад СДТ (СД)',
        instruction: null,
        address: {
            geoId: 213,
            region: null,
            subRegion: null,
            locality: 'Москва',
            street: 'Котляковская',
            house: '1с',
            housing: null,
            building: null,
            apartment: null,
            postCode: null,
            comment: null,
        },
        contact: {
            lastName: 'Иванов',
            firstName: 'Иван',
            middleName: 'Иванович',
            phoneNumber: null,
            internalNumber: null,
        },
        schedule: [
            {
                id: 77056724,
                day: 1,
                timeFrom: '00:00:00',
                timeTo: '23:59:00',
            },
        ],
        shipmentTypes: null,
    },
    fromPartnerId: 48242,
    toPartnerId: 1005117,
    returnPartnerId: 48242,
    handlingTime: 0,
    shipmentType: 'IMPORT',
    productRatings: [
        {
            locationId: 225,
            rating: 0,
        },
    ],
    cutoffs: [
        {
            locationId: 225,
            cutoffTime: '18:00:00',
            packagingDuration: null,
        },
    ],
    shipmentSchedule: [
        {
            id: null,
            day: 1,
            timeFrom: '10:00:00',
            timeTo: '19:00:00',
        },
    ],
    registerSchedule: [
        {
            id: 77570198,
            day: 1,
            timeFrom: '00:00:00',
            timeTo: '00:00:00',
        },
    ],
    transferTime: null,
    inboundTime: null,

}
```
# Новые ручки Nesu, разработаные для проекта мультискладовость

## getBusinessWarehouses

Полный аналог старой ручки [getWarehouses](https://github.yandex-team.ru/market/kadavrique/tree/master/mocks/Nesu#getwarehouses)
возвращает список складов бизнеса

## getBusinessWarehouseById

[Ручка получения информации](https://nesu.tst.vs.market.yandex.net/swagger-ui.html#/business-controller/getWarehouseUsingGET) о конкретном складе в виде:

```

{
    id: 10000481773,
    name: 'Раковый дропшип-склад',
    externalId: '2345',
    contact: {
        lastName: 'Тестов',
        firstName: 'Тест',
        middleName: '',
        phoneNumber: '987-789-98-77',
        internalNumber: '221',
    },
    address: {
        geoId: 15,
        region: 'Тульская область',
        locality: 'Тула',
        street: 'Ленина',
        house: '12',
        housing: '',
        building: '',
        apartment: '',
        postCode: '114432',
        comment: 'Ленинский склад',
    },
    schedule: [
        {
            day: 5,
            timeFrom: '09:00:00',
            timeTo: '23:00:00',
        }, {
            day: 4,
            timeFrom: '09:00:00',
            timeTo: '23:00:00',
        }, {
            day: 2,
            timeFrom: '09:00:00',
            timeTo: '23:00:00',
        }, {
            day: 1,
            timeFrom: '09:00:00',
            timeTo: '23:00:00',
        }, {
            day: 3,
            timeFrom: '09:00:00',
            timeTo: '23:00:00',
        },
    ],
}
```

## createBusinessWarehouse

[ручка создания нового склада ](https://nesu.tst.vs.market.yandex.net/swagger-ui.html#/business-controller/createWarehouseUsingPOST)

## updateBusinessWarehouse

[ручка изменения информации о складе](https://nesu.tst.vs.market.yandex.net/swagger-ui.html#/business-controller/updateWarehouseUsingPUT)

## getBusinessWarehouseShipmentSettings

[ручка для получения информации о настройках отгрузки](https://nesu.tst.vs.market.yandex.net/swagger-ui.html#/business-warehouse-controller/getShipmentSettingsUsingGET)

## setBusinessWarehouseShipmentSettings

[ручка для сохранения информации о настройках отгрузки](https://nesu.tst.vs.market.yandex.net/swagger-ui.html#/business-warehouse-controller/getShipmentSettingsUsingGET)

## getPostalCodes

[ручка получения почтовых индексов для адреса](https://nesu.tst.vs.market.yandex.net/swagger-ui.html#/location-controller/searchPostalCodeUsingGET)
