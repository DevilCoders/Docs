# Виджет Switcher

Позволяет сделать переключение слотов, аналог switch-case в коде, но для виджетов.

С помощью данного виджета можно реализовать различные варианты UI, которые предполагают отображения одного из N кейсов, такие как:
1) табы
2) визарды
3) туториалы
4) A/B тесты (?)

**Очень важно импортировать этот виджет ПОСЛЕ виджетов кейсов, потому что в apiary есть бага с резолвингом клиентских зависимостей, когда они импортируются не в самом виджете, а в виджете уровнем выше.**
**Если импортировать неправильно, то на клиенте будет ошибка.**
https://st.yandex-team.ru/MARKETFRONTECH-721

**Неправильно:**
```js static
import '@self/root/src/widgets/core/Switcher';
import '@self/project/src/widgets/parts/SomeCase';
```

**Правильно:**
```js static
import '@self/project/src/widgets/parts/SomeCase';
import '@self/root/src/widgets/core/Switcher';
```

## Параметры вызова

* `switcherId: string` - уникальный идентификатор свитчера, необходим для идентификации свитчера при переключении слотов на клиенте с помощью глобального экшена.
* `activeCase: ?string` - активный кейс, слот для этого кейса будет отрендерен на сервере, остальные кейсы рендериться на сервере не будут (их виджеты инициализируются с опцией `bare: true`).
* `cases` - кейсы в виде маппинга "имя кейса" -> "функция, возвращающая результат Widget.create()". По имени активного кейса из этого маппинга выбирается метод и создается виджет. Функция принимает параметр `widgetOptions`, который нужно **обязательно** пробросить в вызов третим параметром: `Widget.create(ctx, {}, widgetsOptions)`.
* `isHiddenWidgetBare: ?boolean` - Необходимо ли создавать неактивные виджеты с опцией `bare`. По умолчанию, `true`.

### Внимание! Если у какого-то виджета в cases есть вложенные виджеты, то нужно передавать isHiddenWidgetBare: false, иначе переключение может работать неправильно (Бага apiary)

## Пример использования

1) В пейдже инициализируем свитчер с двумя кейсами:

```js static
{
    slots: {
        tabs: Switcher.create(ctx, {
            switcherId: 'tabs',
            activeCase: 'first',
            cases: {
                first: widgetOptions => First.create(ctx, {}, widgetOptions),
                second: widgetOptions => Second.create(ctx, {}, widgetOptions),
            }
        }),
    },
}
```

2) Во вьюхе отображаем слот свитчера и можем диспатчить экшены, которые будут переключать активный слот:

```js static
import {switchCase} from '@self/root/src/widgets/core/Switcher/actions';

const mapDispatchToProps = {
    switchCase,
};

export default connect(null, mapDispatchToProps)(({switchCase}) => (
    <div>
        <button onClick={() => switchCase({switcherId: 'tabs', caseName: 'first'})}>first</button>
        <button onClick={() => switchCase({switcherId: 'tabs', caseName: 'second'})}>second</button>
        <Slot name="tabs" />
    </div>
));
```
