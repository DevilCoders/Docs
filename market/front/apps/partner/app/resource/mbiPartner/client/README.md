# Client methods

* [getAlerts] - Уведомления для пользователя.
* [getCampaignRoles] - Информация о правах доступа.
* [getCampaignsBriefInfo] - Сводка кампаний, в которых пользователь играет какую-либо роль.
* [getCampaignsDataStatus] - Статус фида кампаний, привязанных к клиенту, который указан в euid.
* [getCampaignsFinanceStatus] - Финансовая информация о кампаниях, привязанных к клиенту, который указан в euid.
* [getClientIds] - Получить список идентификаторов клиентов для текущего пользователя/агенства. В результате для обычных пользователей будет один `client_id`, к которому привязан пользователь, для агенств - все `client_id` магазинов, с которыми работает агенство.
* [getMessageFilterShopInfo] - Легковесная ручка для получения списка всех доступных магазинов/кампаний по `client_id` для фильтрации уведомлений. Если параметр не указан, и пользователь является агенством, то будет выдана информация по всем `client_id` агенства, если это обычный пользователь, то по его `client_id`.
* [getSuperAdmin] - Информация о суперадмине
* [registerCampaign] - Создания магазина.
* [searchCampaignsFullInfo] - Поиск информации по кампаниям, привязанным к клиенту, который указан в euid. Возвращает только кампании, к которым есть привязки.
* [setInternalName] - Меняет внутреннее название магазина.

[getAlerts]: https://wiki.yandex-team.ru/MBI/NewDesign/components/market-payment/getAlerts/
[getCampaignRoles]: https://wiki.yandex-team.ru/mbi/newdesign/components/market-payment/getcampaignroles/
[getCampaignsBriefInfo]: https://wiki.yandex-team.ru/MBI/NewDesign/components/market-payment/getCampaignsBriefInfo/
[getCampaignsDataStatus]: https://wiki.yandex-team.ru/mbi/newdesign/components/market-payment/getcampaignsdatastatus/
[getCampaignsFinanceStatus]: https://wiki.yandex-team.ru/mbi/newdesign/components/market-payment/getcampaignsfinancestatus/
[getClientIds]: https://wiki.yandex-team.ru/MBI/NewDesign/components/market-payment/getClientIds/
[getMessageFilterShopInfo]: https://wiki.yandex-team.ru/MBI/NewDesign/components/market-payment/getMessageFilterShopInfo/
[getSuperAdmin]: https://wiki.yandex-team.ru/mbi/newdesign/components/market-payment/getsuperadmin/
[registerCampaign]: https://wiki.yandex-team.ru/mbi/newdesign/components/market-payment/register-shop/
[searchCampaignsFullInfo]: https://wiki.yandex-team.ru/mbi/newdesign/components/market-payment/searchcampaignsfullinfo/
[setInternalName]: https://wiki.yandex-team.ru/mbi/newdesign/components/market-payment/shop/internalname/
