## Универсальный поиск (UniSearch)

- [Описание на wiki](https://wiki.yandex-team.ru/universal-search/)
- Существующие тематики
    - [Образование](https://a.yandex-team.ru/arc_vcs/frontend/projects/web4/src/features/UniSearch/README.md#obrazovanie)
    - [Приложения](https://a.yandex-team.ru/arc_vcs/frontend/projects/web4/src/features/UniSearch/README.md#prilozheniya)
    - [Вакансии](https://a.yandex-team.ru/arc_vcs/frontend/projects/web4/src/features/UniSearch/README.md#vakansii)
- Описание ФС
    - [`./UniSearch.components`](https://a.yandex-team.ru/arc_vcs/frontend/projects/web4/src/features/UniSearch/README.md#obshie-komponenty)
    - [`./UniSearch.hooks`](https://a.yandex-team.ru/arc_vcs/frontend/projects/web4/src/features/UniSearch/README.md#obshaya-funkcionalьnostь)
    - [`./UniSearch.features`](https://a.yandex-team.ru/arc_vcs/frontend/projects/web4/src/features/UniSearch/README.md#tematicheskie-poiski)
- Создание новой тематики
- Известные проблемы

### Эксперименты
Префикс для флагов `unisearch_*`

### Пространство в arc
В арке есть общая группа, чтобы работать совместно в одной ветке `groups/unisearch/`
т.е. пушить можно теперь так `push -u groups/unisearch/ISSUE-KEY`

### Существующие тематики
#### Образование
[code](https://a.yandex-team.ru/arc/trunk/arcadia/frontend/projects/web4/src/features/UniSearch/UniSearch.features/UniSearchEducation), [foreverdata](https://yandex.ru/search/?lr=213&text=foreverdata&foreverdata=1072539687)

<details><summary>screen touch</summary>

![](https://jing.yandex-team.ru/files/al88/plain.png)
</details>

<details><summary>screen desktop</summary>

![](https://jing.yandex-team.ru/files/al88/plain%20%281%29.png)
</details>

#### Приложения
> [code](https://a.yandex-team.ru/arc/trunk/arcadia/frontend/projects/web4/src/features/UniSearch/UniSearch.features/UniSearchApps), [foreverdata](https://yandex.ru/search/touch/?lr=213&text=foreverdata&foreverdata=1177338420&redircnt=1631117027.3&noredirect=1)

<details><summary>screen touch</summary>

![](https://jing.yandex-team.ru/files/al88/plain%20%282%29.png)
</details>

---

### Описание ФС
#### Общие компоненты
Используются для построения колдунщиков на Серпе. Предпочтительней использовать их, т.к. по структуре тематические блоки должны строиться одинаково.

>Если какие-то компоненты не подходят, нужно:
>- доработать их
>- если они визуально не подходят к остальным тематикам, надо поговорить с дизайнером, не хотим ли мы тогда новый блок раскатить на все тематики
>- если это нужно только в конкретной тематике, то следует сделать отдельный внутри нее

```
./UniSearch.components
    ./Layout
        ./Layout                        # Корневой блок для колдунщика
        ./Content                       # Блок контента (листинги)
        ./FilterScroller                # Блок для блока фильтров
        ./Footer                        # Блок для подвала (ссылки на подключение, кнопки дозагрузки и т.п.)
        ./Header                        # Блок для шапки (название колдунщика, жалобщик, фильтры)
    ./List
        ./List                          # Блок для отображения списка
        ./Item                          # Блок обертки элемента (отступы, бордеры)
    ./More                              # Дефолтная кнопка «показать еще»
    ./Partnership                       # Ссылка на подключение к тематике
    ./QuickFilter                       # Дефолтные фильтры (пока только в виде кнопки)
    ./Title                             # Блок названия тематики
```

#### Общая функциональность
Т.к. охота сохранить однообразие для колдунщиков, стараемся, чтобы везде была одинаковая логика работы. Если по каким-то причинам логика работы бекенда не подходит, то стоит пообщаться  с командой бэкенда, привести это к общему виду.

```
UniSearch.hooks/
    ./useClassName.ts                   # Простой хэлпер для мемоизации генерации className
    ./useAjaxUpdate.ts                  # Создает функцию похода за данными в нужный адаптер
    ./useItems.ts                       # Предоставляет логику работы с элементами, решает проблемы с дублями и т.д.
    ./useFixScroller.ts                 #
    ./useMetrika.ts                     #
    ./usePreviewHistorySync.ts          #
    ./usePreviewReady.ts                #
```

#### Тематические поиски
```
./UniSearch.features
    ./UniSearchBase
        ./UniSearchBase.typings         # Общие тайпинги для данных и props. Подразумевает, что тематики отличаются
                                        # только форматом данных самих сущностей
        ./UniSearchBase.server.tsx      # Базовый адаптер (абстрактный класс) для тематик. Подразумевает,
                                        # что в конкретной реализации достаточно определить getItem и App
        ./UniSearchBase.hooks           #
            ./useItemsWithFilters.tsx   # Шаблонная логика работы с items, ajax и т.д.
        ./UniSearchBase.tsx             # Базовая обертка для компонент (baobab - контекст, прокидывает высчитанные пропсы, хэндлер)
```

#### Обмен событиями
Для общения удаленных друг от друга компонентов используется паттерн [издатель-подписчик](https://ru.wikipedia.org/wiki/Издатель-подписчик_(шаблон_проектирования)), реализованный на базе [компонента reactBus](https://a.yandex-team.ru/arcadia/frontend/projects/web4/src/components/ReactBus).
События, передаваемые через reactBus указаны в [константах](https://a.yandex-team.ru/arcadia/frontend/projects/web4/src/features/UniSearch/UniSearch.const/index.ts)

### Известные проблемы
- `./UniSearch.components/Title` — собран отдельно по частям. Надо решить проблему, разъезда верстки органики и заголовка УП
