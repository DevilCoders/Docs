# TplOutlet

Данные в стейте:

```
{
    // @deprecated
    "TplOutlet.partners": {
        [id]: PartnerData,
    },
    "TplPartner.partners": {
        [_id]: PartnerData,
    },
    "TplPartner.tplPrePartners.data": {
        [_id]: PrePartnerData,
    },
    "TplPartner.reports.stub": ReportsData,
    "TplPartner.reports.data": {
        isPassEmptyParams: boolean,
        params: ReportsRequestParams,
        response: ReportsData,
    }
    "TplOutlet.returns.data": {
        [_id]: DispatchItem,
    },
    "TplOutlet.orders": {
        [orderId]: Order,
    },
    "TplOutlet.pickupPoints": {
        [prePickupPointId]: PickupPoint,
    },
    "TplOutlet.returnableItems": {
        [orderId]: ReturnOrderItems,
    },
    "TplOutlet.clientReturns": {
        [_returnId]: ReturnRequestsItem,
    }
    "TplOutlet.infoMessages": {
        banners: TplOutletBannerMessage[];
        popups: TplOutletPopupMessage[];
    },
    "TplOutlet.calendar": Calendar;
    "TplOutlet.consumablesCapacity": ConsumablesCapacity[];
    "TplOutlet.receptionShipments": Shipment[];
    "TplOutlet.dispatchingShipments": Shipment[];
    "TplOutlet.incompleteOrders": IncompleteOrder[];
}
```
