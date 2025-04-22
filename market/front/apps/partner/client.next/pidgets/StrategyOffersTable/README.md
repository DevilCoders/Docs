## Пиджет таблицы товаров 

Пиджет подгружает список товаров компании или всего магазина если не передан id-кампании (пропа ```id```) и закидывает их в коллекцию [campaignsOffers](https://a.yandex-team.ru/svn/trunk/arcadia/market/front/apps/partner/shared/collections/), откдуа потом забирает селекторами той же коллекции. 

Также пиджет смотрит на коллекцию [campaignsInfo](https://a.yandex-team.ru/svn/trunk/arcadia/market/front/apps/partner/shared/collections/), в которой хранится информация по кампаниям и откуда подтягиваются статус и прочие нужные пиджету данные. Если пропа с id-кампании передана, то прелоадеры скроются только когда будет загруженна кампания, если пропа ```undefined```, то прелоадеры будут скрыты сразу после загрузки товаров и списка кампаний магазина, а ```strategy.status```

### Props

```Typescript
type Props = {
    // id-кампании у которой подгружаем товары. Если его не передать, то будут грузиться все товары кампании
    id?: StrategyId;
    // может ли мерч редактировать кампанию
    canCreateStrategy: boolean;

    // инфа о мерче
    uid: number;
    shopId: number;
    businessId: BusinessId | null;
    campaignId: number;
    campaignType: CampaignType;
    platformType: Platform;
    isDbs: boolean;
    isSupplier: boolean;

    // конфиг с именами компонентов-фильтров, если передать пустой массив, то фильтров у таблицы не будет
    filterComponents: FiltersComponent[];
    // конфиг таблицы, в котором задаем какие колонки отображать
    tableConfig: TableColumnsConfigs;

    // при true не отчищает за собой коллекцию campaignsOffers, и использует от туда готовые данные при повторном маунте (default = true)
    cashed?: boolean
};
```
