## Sites YT export
[Периодическая таска в шиве](https://docs.yandex-team.ru/classifieds-infra/deploy/specification/periodic), которая строит экспорт новостроек в YT.
[Поставка](https://yt.yandex-team.ru/hahn/navigation?path=//home/sprav/providers/yandex-realty)
Используется яндекс.картами для показа данных о новостройках при объектном ответе
![alt text](img/object-answer.png "Объектный ответ на серпе")

### Как работают карты
Сперва из справочника получают все организации с provider_id недвижимости, потом отфильтровывают из низ дубли, затем клеют это с данными из //home/sprav/tycoon/production/snapshot/ad_export_orders (я так понимаю это про то заказывалась реклама или нет)  Потом все это мы клеим с нашими данными. И к этому доливают похожие.
Если организации нет в //home/sprav/tycoon/production/snapshot/ad_export_orders поэтому мы не делают сниппет для нее, а по запросу рисуют обычный геопоисковый колдунщик с данными из [алтая](https://altay.yandex-team.ru/cards/8272947177)
