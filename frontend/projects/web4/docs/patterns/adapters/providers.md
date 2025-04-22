# Провайдеры

В адаптере ["Авиа"](../../../src/features/GeoCommonUnisearch) нужно уметь обрабатывать данные сразу нескольких источников. Чтобы не писать весь этот код в одном файле, придумали [Провайдеры](../../../src/features/GeoCommonUnisearch/providers).

Для каждого источника данных пишется свой провайдер:

``` ts
export class AviaProviderBase implements IProvider {
    getTitleUrl(): string { return this.data.title.url; }

    // ...
}
```

Основной адаптер смотрит в данные и по выбирает, какие провайдеры использовать для подготовки данных для фичи:

``` ts
export abstract class AdapterGeoCommonUnisearchBase extends Adapter<IGeoCommonUnisearchSnippet> {
    static AviaProvider: typeof AviaProviderBase;
    static BusProvider: typeof BusProviderBase;
    static TrainProvider: typeof TrainProviderBase;

    getSources() {
        const sources = {} as Record<Transport, IProvider>;
        const { avia, bus, rasp } = this.snippet.data.sources;

        if (avia) {
            sources.avia = new this.constructor.AviaProvider(this.context, avia);
        }

        if (bus && bus.offers.some(offer => Boolean(offer.freeSeats))) {
            sources.bus = new this.constructor.BusProvider(this.context, bus);
        }

        if (rasp) {
            sources.rasp = new this.constructor.TrainProvider(this.context, rasp);
        }

        return sources;
    }

    // ...
}
```
