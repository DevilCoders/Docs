# Memo
Добавил небольшую мидлварю для сохранения / восстановления бранчей стора.

Возможная замена для storables. Подходит для кейсов, когда нужно просто данные из какого-либо бранча стора сохранять в ls. При загрузке пэйджа стор патчится данными из ls обратно.

Пока что заюзано на карте с машинками для пинов и ордеров.

Задаётся через параметр memos:arrayOf(object(type:string, path:string)) в asPage. Type — экшн редакса, path — какой бранч сохранять.

```JavaScript
asPage({
    memos: [ // see memosMiddleware
        {
            type: 'TAXIMAP/PINS/FILTERS/CHANGE',
            path: 'taximap.pins.filters'
        },
        {
            type: 'TAXIMAP/PINS/VISIBILITY/CHANGE',
            path: 'taximap.pins.visibility'
        },
        {
            type: 'TAXIMAP/PINS/SETTINGS/CHANGE',
            path: 'taximap.pins.settings'
        },
        {
            type: 'TAXIMAP/ORDERS/FILTERS/CHANGE',
            path: 'taximap.orders.filters'
        },
        {
            type: 'TAXIMAP/ORDERS/VISIBILITY/CHANGE',
            path: 'taximap.orders.visibility'
        },
        {
            type: 'TAXIMAP/ORDERS/SETTINGS/CHANGE',
            path: 'taximap.orders.settings'
        },
        {
            type: 'TAXIMAP/METRICS/SETTINGS/CHANGE',
            path: 'taximap.metrics.settings'
        }
    ]
}
```

Миддлвара смотрит на memos пэйджа, и если видит, что для этого экшна нужно сохранять данные, сохраняет их (middlewares/memo).

При инициализации пэйджа в asPage происходит PageApi.restore(), внутри которого происходит загрузка данных в обратную сторону (GLOBAL/RESTORE).

https://github.yandex-team.ru/taxi/taxi-atlas/pull/231

# Очистка LocalStorage
Реализована в модуле `static/api/lsManager.js`

Бывают случаи, когда структура данных или сами данные, которые мы храним в LocalStorage, потеряла актуальность и может привести к ошибкам или неправильному поведению приложения.
В таких ситуациях необходимо очистить либо весь LS целиком, либо конкретную часть LS.

У нас поддерживаются оба варианта очистки.

## Очистка всех данных в LS
Для очистки всех данных, необходимо повысить версию в переменной LSManager.VERSION.

Как только у пользователя загрузится приложение, LSManager поймёт, что данные в LS пользователя потеряли актуальность, очистит весь LS и проставит в LS актуальную версию. При следующей загрузке приложения версии в коде и в LS будут совпадать и чистки LS не будет.

## Частичная очистка LS
Частичная очистка LS работает аналогично очистке всех данных в LS. Вместо глобальной версии необходимо указать версию по конкретному пути в LS.

Версии хранятся в объекте `LSManager.storeVersions`.  
Для того, чтобы очистить LS по конкретному пути, необходимо указать путь в ключе объекта `storeVersions` и указать или повысить версию в значении.

К примеру, мы хотим очистить LS по пути `taximap.taximapUiFilters.combinedStatuses`, где `taximap` - ключ в LS.  
![](https://jing.yandex-team.ru/files/csilence/lsmanager_clear_path.png)

Назначаем версию по данному пути в `LSManager.storeVersions`.
```JavaScript
class LSManager {
    ...
    // Путь должен соответствовать объекту в LS а не реальному пути в redux store
    static storeVersions = {
        'taximap.taximapUiFilters.combinedStatuses': 1
    }
    ...
}
```

Если путь уже существует в объекте storeVersions, нужно просто инкрементировать версию.

При следующей загрузке приложения все данные по пути `taximap.taximapUiFilters.combinedStatuses` будут удалены **вместе с ключём** `combinedStatuses`.

# storable + storableRegistry

Устаревший инструмент для работы с ls.
Сделан был тогда, когда было несколько очень сильно похожих разделов типа Pixel, для хранения фильтров, настроек хитмапа и проч.

В ней есть 3 уровня переопределения настроек: defaultState, localStorage, shortLink.

Такая схема (с пошаренными брэнчами) не оправдала себя — регулярно забываем чистить стейт при анмаунте контейнеров, он протекает туда, куда не надо, интерфейсы не очень удобные и т.п.

Кажется, что больше использовать storable не стоит. Лучше использовать мемо и конкретные брэнчи.
