# Миксины

В адаптерах ["Авиа"](../../../src/features/GeoCommonUnisearch) код, реализующий метод `ajax` для генерации содержимого табиков, оформлен в виде миксина:

``` ts
export function adapterGeoCommonUnisearchTab(BaseAdapter) {
    return class extends BaseAdapter {
        ajax(): {
            // ...
        }
    };
}
```

Если адаптер должен уметь генерировать содержимое тибика, он просто используем миксин `adapterGeoCommonUnisearchTab`:

``` ts
import { adapterGeoCommonUnisearchTab } from './mixin';
import { AdapterGeoCommonUnisearch as Base } from '../GeoCommonUnisearch@touch-phone.server';

export class AdapterGeoCommonUnisearch_tab extends adapterGeoCommonUnisearchTab(Base) {
    // ...
}
```
