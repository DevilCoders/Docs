# OrderBoxCount

## Что это

Виджет для задания количества грузомест

## Используемые бэкенды

[setOrderDeliveryParcelBoxes](http://checkouter.tst.vs.market.yandex.net:39001/swagger-ui.html#/parcel-box-controller/putParcelBoxesUsingPUT)

## Пропсы

```
export type Props = {
    orderId: number;
    parcelId: number;
    count: number;
    onSuccess?: () => void;
    onError?: () => void;
};
```