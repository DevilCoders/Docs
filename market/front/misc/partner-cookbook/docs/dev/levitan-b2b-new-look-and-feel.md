# Levitan New L&F

Сейчас силами дизайнеров идет разработка новых и редизайн старых компонентов (в фигме в рамках дизайн системы B2B New look and feel). Часть из компонентов уже поддержана в левитане и используется в ПИ. В документе собран список новых компонентов и компонентов, у которых есть две версии, с описанием, какую нужно использовать в каком месте. Так же есть пример добавления на свою страницу новых компонентов.

Фигма: https://www.figma.com/file/NOuXaQrQECrHvHwBfjFnlI/Levitan-B2B-%5Bnew-L%26F%5D?node-id=0%3A1

Какое-то время у нас будут страницы в двух версиях дизайнов, но по итогу в светлом будущем все страницы переедут в новый дизайн. Пока у команды дизайна нет конкретных сроков.

<details>
<summary>Пример страницы в новом дизайне и старом.</summary>
Слева - новый, справа - старый:

<img src="https://jing.yandex-team.ru/files/saaaaaaaaasha/Screenshot%202021-07-27%20at%2016.27.30.5492cda.png" alt="new" height="200"/> <img src="https://jing.yandex-team.ru/files/saaaaaaaaasha/Screenshot%202021-07-27%20at%2016.33.55.aff5690.png" alt="old" height="200"/> 

</details>

## Список с новыми компонентами

Цитата из фигмы:

> Используем только для полностью новых макетов. Не используем для доработок текущих макетов или сценариев.

Нет запрета использовать эти компоненты на старых страницах, но нужно синкануться с дизайнером, что компонент используется осознанно. Если вы думаете, что страницу можно несложными изменениями перевести на новый дизайн (и это не повлияет на сроки релиза проекта), то можно сходить к дизайнеру и предложить ему обновить страницу.

| Название |  Ссылка |
|---|---|
| Message |  https://levitan.yandex-team.ru/b2b/develop/core/message |
| Drawer |  https://levitan.yandex-team.ru/b2b/develop/core/drawer |
| Skeleton |  https://levitan.yandex-team.ru/b2b/develop/core/skeleton |
| StackedBar |  https://levitan.yandex-team.ru/b2b/develop/core/stackedbar |

## Список с заредизайнеными компонентами

Для компонентов, которые используются на старых страницах, выставлена версия компонентов с префиксом `@deprecated` (это не значит, что их нельзя использовать на текущих страницах, но это значит, что эти компоненты нельзя использовать на страницах с новым дизайном).

По умолчанию сейчас на всех страницах используется `@deprecated` версия компонентов, перечисленных ниже. Новые нужно включать через `Registry.RegistryProvider`.

| Название |  Есть ли `@deprecated` версия | Ссылка | Отличия |
|---|:---|:---|:---|
| Button (+v0.2.17) |  + | https://levitan.yandex-team.ru/b2b/develop/core/button | Изменены стили: скругления, размеры шрифта и паддингов |
| Icon | - | https://levitan.yandex-team.ru/b2b/develop/core/icon | Новые иконки выкатились на все страницы |
| RatingMeter | + | https://levitan.yandex-team.ru/b2b/develop/core/ratingmeter | Новые стили |
| Text3 | Text2\* | https://levitan.yandex-team.ru/b2b/develop/core/text3 | Новый API использования, новые размеры, шрифты |
| Link | + | *еще не реализовано* | Другие размеры, цвет |

> (*) Компонент Text, которые встречается в ПИ, использовать не нужно. Для страниц в старом дизайне нужно использовать Text2, в новом - Text3.

### Как подключить новую версию компонента

Пример использования новых версий компонентов (в котором заменяем `Button` и `RatingMeter` на новые версии): https://github.yandex-team.ru/market/partnernode/blob/master/client.next/pages/FulfillmentSummary/App.tsx

```typescript
import React from 'react';
import {Registry, Button, RatingMeter} from '@yandex-levitan/b2b';

export const App = () => (
    <Registry.RegistryProvider
        {...{
            [String(Button)]: Button,
            [String(RatingMeter)]: RatingMeter,
        }}
    >
        <PageWithInitializationError>
            <LayoutWrapper theme="smokeGray">
                <UnitedSummary />
            </LayoutWrapper>
        </PageWithInitializationError>
    </Registry.RegistryProvider>
);
```

Версия `deprecated` выставлена для использования по умолчанию, логика описана в [`LevitanProvider`](https://github.yandex-team.ru/market/partnernode/blob/master/client.next/containers/LevitanProvider/index.tsx).
