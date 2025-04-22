# Рестайлинг мобильной метрики

[Figma](https://www.figma.com/file/gWA4BFqQ4eGVRhxiOcc7cz/Mobile-site?node-id=14766%3A85612)
[Тикет на дизайн](https://st.yandex-team.ru/DSNMETR-93)
[Эпик](https://st.yandex-team.ru/METR-46478)

## Задачи

### 1. Новая шапка мобильной метрики

[Figma](https://www.figma.com/file/gWA4BFqQ4eGVRhxiOcc7cz/Mobile-site?node-id=14766%3A88426)

Было:
![old-header](https://jing.yandex-team.ru/files/gakuznetsov/uhura_2021-09-29T12%3A43%3A05.284182.jpg)

Стало:
![new-header](https://jing.yandex-team.ru/files/gakuznetsov/uhura_2021-09-29T12%3A43%3A06.197558.jpg)

Для нового логотипа можно использовать [генератор](https://logo.common.yandex.net/).

Вместо колокольчика должны быть чаты. Знак вопросика пока не делаем.

### 2. Новые табы

[Figma](https://www.figma.com/file/gWA4BFqQ4eGVRhxiOcc7cz/Mobile-site?node-id=14766%3A88426)

Было:
![old-tabs](https://jing.yandex-team.ru/files/gakuznetsov/uhura_2021-09-29T13%3A17%3A15.144942.jpg)

Стало:
![new-tabs](https://jing.yandex-team.ru/files/gakuznetsov/uhura_2021-09-29T13%3A03%3A01.476756.jpg)

В новом дизайне используются на замену старым хлебным крошкам, а так же как переключатель фильтра на списке счетчиков

Табы должны уметь подскраливаться к активному, каждый таб должен уметь принимать универсальный контент.
Компонент имеет разные скругление углов (в хлебных крошках 12px, в табах отчета 8px)

Примерные интерфейсы:
```typescript
import {ReactNode} from "react";

interface Tab {
    id: string;
    content: string | ReactNode;
    count: number;
    isHighlighted: boolean;
}

enum TabsTheme {
    BreadCrumbs = 'BreadCrumbs', // border-radius 12px
    Default = 'Default' // border-radius 8px
}

interface Tabs {
    tabs: Tab[];
    activeTabId: string;
    isDisabled: boolean;
    theme: TabsTheme; // сейчас влияет только на border-radius, возможно, стоит делать не темой, а одним пропсом
    onTabClick: (tabId: string) => void;
}
```

### 3. Новая кнопка "Показать еще" (предлагаю делать вместе с з. 2, задача маленькая)
[Figma](https://www.figma.com/file/gWA4BFqQ4eGVRhxiOcc7cz/Mobile-site?node-id=14766%3A88426)

Было:
![old-more-btn](https://jing.yandex-team.ru/files/gakuznetsov/uhura_2021-09-29T13%3A22%3A23.110416.jpg)

Стало:
![new-more-btn](https://jing.yandex-team.ru/files/gakuznetsov/uhura_2021-09-29T13%3A22%3A27.072625.jpg)

### 4. Рестайлинг страницы "Список счетчиков"

[Figma](https://www.figma.com/file/gWA4BFqQ4eGVRhxiOcc7cz/Mobile-site?node-id=14766%3A87571)

Было/стало:
![counter-list](https://jing.yandex-team.ru/files/gakuznetsov/uhura_2021-09-29T14%3A50%3A23.061771.jpg)

Что нужно сделать:
1) Заменить шапку на новую (зависит от з. 1)
2) Заменить кнопку "Показать еще" на новую (зависит от з. 3)
4) Сверстать остров "Мои счетчики"
5) Добавить табы с переключением типов счетчиков
6) Рестайлинг карточки счетчика: меняются отступы, размеры текста, убирается тень, меняем цвет скелетона на более теплый (можно выбрать самому и уточнить у Димы)
7) В PageLayoutTouch меняем margin: для экранов > 350px делаем 8px, для остальных 0px

### 5. Рестайлинг отчетов (зависит от з. 4.)

[Figma](https://www.figma.com/file/gWA4BFqQ4eGVRhxiOcc7cz/Mobile-site?node-id=14766%3A87926)

Было/стало:
![reports](https://jing.yandex-team.ru/files/gakuznetsov/uhura_2021-09-29T19%3A35%3A21.758752.jpg)

Что нужно сделать:
1) Рестайлинг острова "Популярные отчеты": делаем островом, меняем стиль заголовка, добавляем новые табы
2) Рестайлинг острова "Сводные отчеты" (аналогично п.1)
3) Рестайлинг островов с графиками и таблицами: меняются размеры текста и легенды, текст легенды больше не цветной

## 6. Рестайлинг кнопок PeriodButton, SegmentationButton, ParamsButton

[Figma](https://www.figma.com/file/gWA4BFqQ4eGVRhxiOcc7cz/Mobile-site?node-id=14766%3A85838)

Было:
![period-button-old](https://jing.yandex-team.ru/files/gakuznetsov/uhura_2021-10-12T19%3A32%3A08.911392.png)

Стало:
![period-button-new](https://jing.yandex-team.ru/files/gakuznetsov/uhura_2021-10-12T19%3A32%3A09.909045.png)

## 7. Рестайлинг боковой шторки

[Figma](https://www.figma.com/file/gWA4BFqQ4eGVRhxiOcc7cz/Mobile-site?node-id=15126%3A91013)

Было:
![profile-modal-old](https://jing.yandex-team.ru/files/gakuznetsov/uhura_2021-10-12T18%3A12%3A20.992833.jpg)

Стало:
![profile-modal-old](https://jing.yandex-team.ru/files/gakuznetsov/uhura_2021-10-12T18%3A12%3A22.110770.jpg)

## 8. Рестайлинг модалок Параметры отчета/Параметры сводки

[Figma](https://www.figma.com/file/gWA4BFqQ4eGVRhxiOcc7cz/Mobile-site?node-id=15052%3A95292)

Было:
![params-modal-old](https://jing.yandex-team.ru/files/gakuznetsov/uhura_2021-10-12T18%3A24%3A45.321270.jpg)

Стало:
![params-modal-new](https://jing.yandex-team.ru/files/gakuznetsov/uhura_2021-10-12T18%3A24%3A46.192936.jpg)

Модалки:
* ReportParamsModal
* ConversionReportParamsModal
* OrdersReportParamsModal
* DashboardParamsModal

## 9. Редизайн шторки "Период и детализация"

[Figma](https://www.figma.com/file/gWA4BFqQ4eGVRhxiOcc7cz/Mobile-site?node-id=14946%3A90843)

Было:
![period-old](https://jing.yandex-team.ru/files/gakuznetsov/uhura_2021-10-12T18%3A27%3A09.470672.jpg)

Стало:
![period-new](https://jing.yandex-team.ru/files/gakuznetsov/uhura_2021-10-12T18%3A27%3A10.587679.jpg)

## 10. Редизайн модалки "Сегментация"

[Figma](https://www.figma.com/file/gWA4BFqQ4eGVRhxiOcc7cz/Mobile-site?node-id=14946%3A91363)

Было:
![segmentation-old](https://jing.yandex-team.ru/files/gakuznetsov/uhura_2021-10-12T19%3A12%3A28.311095.jpg)
![segmentation-old-2](https://jing.yandex-team.ru/files/gakuznetsov/uhura_2021-10-12T19%3A12%3A27.238925.jpg)

Стало:
![segmentation-new](https://jing.yandex-team.ru/files/gakuznetsov/uhura_2021-10-12T19%3A12%3A29.109439.jpg)

## 11. Редизайн модалок сегментов

[Figma](https://www.figma.com/file/gWA4BFqQ4eGVRhxiOcc7cz/Mobile-site?node-id=14946%3A91465)

Было:
![segment-old](https://jing.yandex-team.ru/files/gakuznetsov/uhura_2021-10-12T19%3A24%3A10.952953.png)

Стало:
![segmentat-new](https://jing.yandex-team.ru/files/gakuznetsov/uhura_2021-10-12T19%3A24%3A11.787686.png)

## 12. Редизайн модалок поиска по сегментации

[Figma](https://www.figma.com/file/gWA4BFqQ4eGVRhxiOcc7cz/Mobile-site?node-id=14946%3A91549)

Было:
![search-segment-old](https://jing.yandex-team.ru/files/gakuznetsov/uhura_2021-10-12T19%3A26%3A03.511330.jpg)

Стало:
![search-segmentat-new](https://jing.yandex-team.ru/files/gakuznetsov/uhura_2021-10-12T19%3A26%3A04.232753.jpg)

## 13. Редизайн вкладки "Вебвизор"

[Figma](https://www.figma.com/file/gWA4BFqQ4eGVRhxiOcc7cz/Mobile-site?node-id=14950%3A91757)

Было:
![webvisor](https://jing.yandex-team.ru/files/gakuznetsov/uhura_2021-10-12T19%3A34%3A58.057883.png)

Стало:
![webvisor-new](https://jing.yandex-team.ru/files/gakuznetsov/uhura_2021-10-12T19%3A34%3A59.254529.png)

## 14. Редизайн "Информации о визите"

[Figma](https://www.figma.com/file/gWA4BFqQ4eGVRhxiOcc7cz/Mobile-site?node-id=14950%3A91757)

Было:
![webvisor-info](https://jing.yandex-team.ru/files/gakuznetsov/uhura_2021-10-12T19%3A38%3A43.138879.png)

Стало:
![webvisor-info-new](https://jing.yandex-team.ru/files/gakuznetsov/uhura_2021-10-12T19%3A38%3A44.042123.png)

## 15. Редизайн "Настройки счетчика"

[Figma](https://www.figma.com/file/gWA4BFqQ4eGVRhxiOcc7cz/Mobile-site?node-id=14950%3A94839)

Было:
![settings](https://jing.yandex-team.ru/files/gakuznetsov/uhura_2021-10-12T19%3A41%3A24.650669.png)

Стало:
![settings-new](https://jing.yandex-team.ru/files/gakuznetsov/uhura_2021-10-12T19%3A41%3A25.698472.png)

## 16. Редизайн поиска на списке счетчиков

Отдельного дизайна нет, ориентируемся на дизайн поиска по сегментации. Вставляем в острова наши острова с найденными счетчиками

[Figma](https://www.figma.com/file/gWA4BFqQ4eGVRhxiOcc7cz/Mobile-site?node-id=14946%3A91549)

## 17. Редизайн отчета "Конверсии"

[Figma](https://www.figma.com/file/gWA4BFqQ4eGVRhxiOcc7cz/Mobile-site?node-id=15047%3A94745)

Было:
![conversion](https://jing.yandex-team.ru/files/gakuznetsov/uhura_2021-10-13T14%3A35%3A52.616671.jpg)

Стало:
![conversion-new](https://jing.yandex-team.ru/files/gakuznetsov/uhura_2021-10-13T14%3A35%3A51.149737.jpg)
