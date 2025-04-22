# ZoneEvents

Модуль для разметки кода и отправки событий с помощью зон.

## Важно!

Это экспериментальный модуль, который пока используется только на "Единой странице заказов".

## Какую задачу решает

Данный модуль сделан по мотивам библиотеки [@yandex-market/cia](https://a.yandex-team.ru/svn/trunk/arcadia/market/front/monomarket/lib/lib/cia), и предназначен для сбора информации о событии при его прохождении через соответствующие зоны (контексты).

В отличие от библиотеки данный модуль не занимается автосбором кликов и прочих событий.

Модуль представляет собой набор компонентов и хуков для разметки кода с помощью зон, через которые можно отправлять события.

Отправку событий через зоны необходимо делать вручную.

Используется в основном для сборки и отправки целей Яндекс.Метрики для различных пользовательских событий.

Для передачи информации о прохождении события через зоны использует React-контекст, в результате чего такой подход отлично работает с порталами.

## Zone + useZoneEvent

`Zone` - предназначен для оборачивания дочерних компонентов в специальную зону.

Для зон можно задавать дополнительные параметры, но они не являются обязательными.

`useZoneEvent` - возвращает ф-ию, вызов которой отправит событие для прохождения через зоны вверх по дереву React-компонентов.

```tsx
import {Button} from '@yandex-levitan/b2b';
import {Zone, useZoneEvent} from '~/components/ZoneEvents';

const MyButton = () => {
    const sendZoneClickEvent = useZoneEvent('click');

    return <Button onClick={sendZoneClickEvent}>Test</Button>
}

const Test = () => {
    return (
        <Zone name="zone1" params={{a: 1}}>
            <Zone name="zone2" params={{b: 2}}>
                <Zone name="zone3">
                    <MyButton />
                </Zone>
            </Zone>
        </Zone>
    );
}
```

В результате клика по кнопке информация о клике пройдет через все зоны вверх по дереву React-компонентов.

## ZoneEvents

Данный компонент служит для обработки события после его прохождения через все зоны.

Как правило, в данный компонент необходимо оборачивать всю страницу.

```tsx
import {EventType, EventParams, ZoneInfo, ZoneEvents} from '~/components/ZoneEvents';
import {sendMetrika} from '~/utils/metrika';

type Props = {
    children: ReactNode;
};

const ZoneMetrika = ({children}: Props) => {
    const callback = (eventType: EventType, zones: ZoneInfo[]) => {
        // Используем информацию о событии и зонах, через которое прошло данное событие, для отправки целей Яндекс.Метрики.
        const goalName = ...;
        const goalParams = ...;

        if (goalName) {
            sendMetrika(goalName, goalParams)();
        }
    };

    return <ZoneEvents callback={callback}>{children}</ZoneEvents>;
};

const App = () => (
    <ZoneMetrika><Content /></ZoneMetrika>
);
```

## useZone

Иногда нет возможности, или же не хочется создавать враппер для компонента, чтобы была возможность отправить событие через нужную зону.

Для этих целей можно использовать специальный хук.

Важно понимать, что если внутри такого компонента будут вложенные компоненты со своими зонами, то события, отправленные из дочерних компонентов не получат информацию, что они прошли через указанную зону.

Вы можете использовать данный хук без каких-либо опасений для компонентов, которые являются самыми нижними в иерархии зон.

```tsx
import {Button} from '@yandex-levitan/b2b';
import {Zone, useZone} from '~/components/ZoneEvents';

const MyButton = () => {
    const {sendZoneClickEvent} = useZone('myButton');

    return <Button onClick={sendZoneClickEvent}>Test</Button>;
};

const Test = () => {
    return (
        <ZoneEvents callback={() => {
            // Здесь мы получим информацию обо всех зонах + зону myButton.
        }}>
            <Zone name="zone1" params={{a: 1}}>
                <Zone name="zone2" params={{b: 2}}>
                    <Zone name="zone3">
                        <MyButton />
                    </Zone>
                </Zone>
            </Zone>
        </ZoneEvents>
    );
}
```
