### **NewsCardVerticalSlider**

Скролящийся блок-таблица с доскролом, до ближайшего столбца.

*Интерфейс*:
 - items: IItems[];
 - rowNumber?: number;
 - columnNumber?: number;
 - direction?: 'vertical' | 'horizontal';
 - cardAlign?: 'left' | 'center';
 - hideBullets?: boolean;

---
**items** - массив элементов в виде json вида:
```
[
    {
        agencyImageSrc: {string} - путь до картинки в ячейке,
        title: {string} - текст ячейки,
        agency: {string} - имя агенства,
        time: {string} - время публикации,
        href: {string} - путь к новости (открывается в турбо поверх страницы)
    },
    ...
];
```

Пример *items* можно посмотреть в фавйле *NewsCardVerticalSlider/datastub.ts*;

**rowNumber** - количество *строк* в таблице;

**columnNumber** - количество *столбцов* в таблице;

**direction** (по-умолчанию - *horizontal*) - направление распределения ячеек в таблице
    (вертикально или горизонтально);

**cardAlign** (по-умолчанию - *center*) - размещение столца относительно контейнера
    (по центру "center" и прижать к левому краю "left");

**hideBullets** (по-умолчанию - *false*) - скрыть полосу с буллетами или оставить.

---
### **ВАЖНО!**

Если указать **количество столбцов и количество строк одновременно**, то элемент будет **обрезать
данные**, если их пришло **больше чем указанное количество ячеек**!

Например если вызвать элемент с данными из stub { newsCardVerticalSliderData }, который содержит 10 элементов:
```
import { newsCardVerticalSliderData } from './datastub';

...

console.log(`items.length = ${newsCardVerticalSliderData.length}`) // items.length = 10
<NewsCardVerticalSlider
    items={newsCardVerticalSliderData}
    rowNumber={3}
    columnNumber={3}
/>
```

То будет выведена таблица размером **3Х3**, а не **3Х4**!!!

Так как передано сразу два параметра
**rowNumber** и **columnNumber**!!!
Если передано более **9** элементов в **items**, то они будут **ИГНОРИРОВАТЬСЯ**!

---

Если нужно выводить все данные, которые пришли в **items**, то **не надо** указывать второй параметр!

Например:
```
<NewsCardVerticalSlider
    items={newsCardVerticalSliderData}
    rowNumber={3}
/>
```

или

```
<NewsCardVerticalSlider
    items={newsCardVerticalSliderData}
    direction="vertical"
    columnNumber={3}
/>
```

Если **не указывать** *columnNumber* и *rowNumber*, то элементы будут выведены **горизонтально в одну строку**!

---



