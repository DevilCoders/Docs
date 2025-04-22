# Фильтры
- [Общее](#obshee)
    - [На улучшение](#na-uluchshenie)
- [Разметка](#razmetka)
    - [Быстрые фильтры](#bystrye-filtry)
    - [Модалка со страницами фильтров](#modalka-so-stranicami-filtrov)
    - [Модалка со страницами фильтров / Список фильтров](#modalka-so-stranicami-filtrov-/-spisok-filtrov)
    - [Модалка со страницами фильтров / Список значений фильтра](#modalka-so-stranicami-filtrov-/-spisok-znachenij-filtra)

## Общее

- применение фильтров трекаем просто через клики в кнопки
- состояние фильтров трекаем в атрибуты ноды `$page/$main/product-list-controls/button-open-filters-list`

### На улучшение

- трекать клики в шторке фильтра. Например в `$page/$main/product-list-controls/filters-modal/filter-options/body`
- изменение аттрибутов приводит к append. М.б. надо подумать про внедрение change

## Разметка

- `$page/$main/product-list-controls` — общий блок со всеми контролами [touch](https://jing.yandex-team.ru/files/eshreder/a57a6709e380513fe02c71730258d7b5.png)

- `$page/$main/product-list-controls/sorting` — блок сортировки [touch](https://jing.yandex-team.ru/files/eshreder/540a5f9bde948437cd728972425a5df7.png)<br/>
    ```
    {
        name: 'sorting',
        attrs: {
            sortOrder: 'dpop'
        }
    }
    ```

- `$page/$main/product-list-controls/button-open-filters-list` — кнопка открытия фильтров. В неё логируются примененные фильтры [touch](https://jing.yandex-team.ru/files/eshreder/08c0a0f8b0d05e73276267eff586511d.png)
```
{
    "name": "filters-button",
    "attrs": {
        "checkedFilters": {
            "7893318": [{ "id": "153132" }, { "id": "144123" }],
            "3123123": [{ "id": "1" }],
            "glprice": [{ "min": 0, "max": 100 }]
        }
    }
}
```

### Быстрые фильтры

- `$page/$main/product-list-controls/quick-filters` — быстрые фильтры [touch](https://jing.yandex-team.ru/files/eshreder/27e8552d68324d24573c4a771ab85299.png)

- `$page/$main/product-list-controls/quick-filters/button-clear` — кнопка сброса фильтров (на desktop ее пока нет) [touch](https://jing.yandex-team.ru/files/eshreder/fcfa0110b77bad49016871ed304d0ec4.png)

- `$page/$main/product-list-controls/quick-filters/filter` — конкретный фильтр [touch](https://jing.yandex-team.ru/files/eshreder/b7ac3747370fd716de8aeb0dfa3e139c.png)
```
{
    "filterId": "15464289",
    "name": "Морозильная камера",
    "active": true
}
```

- `$page/$main/product-list-controls/quick-filters/filter/button-open` — кнопка в элементе. По клику открывается конкретный фильтр [touch](https://jing.yandex-team.ru/files/eshreder/512c79b230532a418a3aff0b4fc932f4.png)

- `$page/$main/product-list-controls/quick-filters/filter/button-apply` — кнопка в элементе в случае неактивного тоггл-фильтра. В этом случае по клику сразу применится тоггл-фильтр [touch](https://jing.yandex-team.ru/files/skosheev/quick-filter-toggle-demo.gif) 

- `$page/$main/product-list-controls/quick-filters/filter/button-reset` — крестик в элементе. по клику сбрасывается установленный фильтр. Если фильтр не установлен, этой кнопки нет [touch](https://jing.yandex-team.ru/files/eshreder/5faee5c49a869b4a71e84ebd5132f243.png).
В случае с активным тоггл-фильтром кнопка в элементе также будет представлена этим баобаб узлом так как клик в нее тоже приведет к сбросу фильтра. Таким образом в случае активного тоггл-фильтра будет два баобаб узла `button-reset`


### Модалка со страницами фильтров

- `$page/$main/product-list-controls/filters-modal` — сама модалка, где рендерятся шторки фильтров. Аппендится только при взаимодействии с фильтрами [touch](https://jing.yandex-team.ru/files/eshreder/8c32fe5f4a260f7897ac93bdacf8e15f.png)


### Модалка со страницами фильтров / Список фильтров

- `$page/$main/product-list-controls/filters-modal/filters-list` — список всех фильтров [touch](https://jing.yandex-team.ru/files/eshreder/cbc126bae9948e00d449fd6d678908a2.png)
- `$page/$main/product-list-controls/filters-modal/filters-list/header` — шапка списка фильтров [touch](https://jing.yandex-team.ru/files/eshreder/4fb6ea675de69be7a736259e8a6919a8.png)
- `$page/$main/product-list-controls/filters-modal/filters-list/header/button-close` — кнопка закрытия шторки [touch](https://jing.yandex-team.ru/files/eshreder/ae72363da6ac8633db7b8363dc5354c2.png)
- `$page/$main/product-list-controls/filters-modal/filters-list/button-group` — группа кнопок применения или отмены фильтров к выдаче [touch](https://jing.yandex-team.ru/files/eshreder/fabce57b7429653a4d961453a6981927.png)
- `$page/$main/product-list-controls/filters-modal/filters-list/button-group/button-clear` — сбросить фильтры. Далее будет перезапрос выдачи и обновление ноды `$page/$main/product-list-controls` (show) [touch](https://jing.yandex-team.ru/files/eshreder/a3cb8e81d439ddb1cf4b02a47eeb7d67.png)
- `$page/$main/product-list-controls/filters-modal/filters-list/button-group/button-submit` — применить фильтры.  Далее будет перезапрос выдачи и обновление ноды `$page/$main/product-list-controls` [touch](https://jing.yandex-team.ru/files/eshreder/8903d997f36c9eeb656b2ed6d30db1a5.png)

### Модалка со страницами фильтров / Список значений фильтра

- `$page/$main/product-list-controls/filters-modal/filter-options` — список значений конкретного фильтра [touch](https://jing.yandex-team.ru/files/eshreder/3cc3a7e6df9c6336640cf316244a2dec.png)
- `$page/$main/product-list-controls/filters-modal/filter-options/header` — шапка списка значений фильтра
[touch](https://jing.yandex-team.ru/files/eshreder/0cbcba6339ec4c1eed9fa9539a2fadea.png)
- `$page/$main/product-list-controls/filters-modal/filter-options/header/button-back` — кнопка возврата к списку фильтров [touch](https://jing.yandex-team.ru/files/eshreder/7ce56f07d23005dbb70650a1cb92504d.png)
- `$page/$main/product-list-controls/filters-modal/filter-options/header/button-close` — закрытие модального окна без применения  [touch](https://jing.yandex-team.ru/files/eshreder/6e6e388c3351568943db0a7fc81d4310.png)
- `$page/$main/product-list-controls/filters-modal/filter-options/button-group` — [touch](https://jing.yandex-team.ru/files/eshreder/0f3b0ff1e39563a3ce172667717e3b36.png)
- `$page/$main/product-list-controls/filters-modal/filter-options/button-group/button-clear` —
сбросить значение фильтра. Перезапроса выдачи не происходит [touch](https://jing.yandex-team.ru/files/eshreder/594fb6792aa07b1ec89a4aad754fb48b.png)
- `$page/$main/product-list-controls/filters-modal/filter-options/button-group/button-submit` —
сохраняет выбранные значения фильтра. Если `filter-options` был открыт из `filters-list`, то при нажатии происходит возврат туда, перезапроса нет. Если через `quick-filters/filter`, то происходит перезапрос выдачи [touch](https://jing.yandex-team.ru/files/eshreder/d62a153cdaf613aabd3f2e5cf5431ce7.png)
