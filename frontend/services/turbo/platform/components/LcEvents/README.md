# lcEvents

`lcEvents` - синглтон в [Конструкторе лендингов](https://lpc.yandex-team.ru), используемый в Lc-секциях для обработки их событий. Событие - это действие, которое совершил пользователь и на которое секция может откликнуться. Пример - открытие модального окна по клику на кнопку или при просмотре какой-либо секции.

События для конкретной секции добавляет и настраивает пользователь в Конструкторе лендингов (lpc.yandex-team.ru).

Триггеры (`LcBaseTrigger`) - классы, реализующие интерфейс `ILcEventTrigger` для обработки (метод `handle`) событий и подписки/отписки (`on`/`off`) на действия.

`LcTriggers` - указание, какой триггер использовать для обработки множества событий. Пример для понимания:
```
export const LcTriggers = {
    [LcSectionType.LcMetrika]: LcMetrikaTrigger,
    [LcSectionType.Modal]: LcBaseTrigger,
    [LcSectionType.LcGoogleAnalytics]: LcGoogleAnalyticsTrigger,
};
```

`LcEventType` - возможные события (клик/отправка формы/наведение курсора/просмотр секции/...).

`LcEventAction` - возможные действия (открытие или закрытие модального окна, переключение слайдов/...).

Событие (`LcEvent`) - это объект, который включает в себя:
* `type` - произошедшее событие;
* `action` - действие, которое нужно выполнить при наступлении события;
* `target` - данные о секции, которая среагирует на событие. Содержит в себе type, тип секции (LcSectionType), и `sectionId` - id секции, который может понадобиться в обработчике действия;
* `data` - данные, нужные для обработки события;

Для того, чтобы секция умела работать с событиями, нужно:
* Импортировать синглтон
```
import lcEvents from '@yandex-turbo/components/LcEvents';
import { LcSectionType } from '@yandex-turbo/components/LcEvents/LcEvents.constants';
```
* Инициализировать необходимый триггер
```
lcEvents.initTrigger(target, params);
```
`target` - это секция, чей триггер должен быть указан:
```
target = { type: LcSectionType.SomeSection, sectionId: '123' }
```
Тип секции должен быть обязательно указан. `sectionId` нужно указать в том случае, если на странице может быть несколько секций указанного типа.

`params` - это настройки для конкретного триггера. В них можно указать `handler` - функцию, которая будет обрабатывать все события (`{ handler: this.handleEventSomeWay }`).

* Добавить обработчики действий, если необходимо
```
lcEvents.on(LcSectionType.SomeSection, LcEventAction.Open, this.handleModalOpen);
```
* Позволить событию случиться :)
```
LcEvents.execute(LcEventType.Click, events, nativeEvent);
```
`nativeEvent` – нативное событие, которое дальше будет передано в обработчик

`events` - массив событий (LcEvent) данной секции. При наступлении события events фильтруются по его типу. Пример events:
```
[
    {
        type: LcEventType.Click,
        action: LcEventAction.Open,
        target: { type: LcSectionType.LcModal, sectionId: 'id секции модального окна' },
        data: {}
    },
    {
        type: LcEventType.Click,
        action: LcEventAction.ChangeSlide,
        target: { type: LcSectionType.Slider, sectionId: 'id секции модального окна' },
        data: { slide: '1' }
    },
    {
        type: LcEventType.Submit,
        action: LcEventAction.Close,
        target: { type: LcSectionType.LcModal, sectionId: 'id секции модального окна' },
        data: {}
    },
];
```
(Если мы выполним клик, то произойдет открытие модального окна и смена слайда. Если отправим форму, модальное окно закроется.)

Если нам нужно просто как-то обработать событие (например, отправить достижение цели при клике на кнопку), то достаточно добавить вызов `LcEvents.execute`.

Подписаться можно двумя способами:
1. Передать `handler` при инициализации, например, так
```
lcEvents.initTrigger({ type: LcSectionType.LcEffect }, { handler: this.handler });
```
Тут есть нюанс. Такой кейс подойдет вам, если у вас всего один handler на target. Если у вас несколько обработчиков (например, в каждой секции свой), то тогда нужно использовать способ 2
2. Передать `handler` в `on`, например, так:
```
lcEvents.initTrigger({ type: LcSectionType.LcEffect });
lcEvents.on(LcSectionType.LcEffect, LcEventAction.ApplyEffect, this.handler);
```
В обработчике нужно проверять тот ли handler вызывался, так как они вызываются все.
Пример тут `turbo/platform/components/LcEffect/LcEffect.tsx`
