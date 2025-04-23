# FAQ. Ленивая загрузка компонентов

Иногда требуется загрузить компонент синглтон на страницу отложенно. Такими компонентами например являются
[ExtralinksPopup](../../features/Organic/Organic.features/OrganicExtralinksPopup/OrganicExtralinksPopup.tsx), [VanillaTooltip](../../features/Organic/Organic.components/VanillaTooltip/VanillaTooltip.tsx), [ReactBurgerMenu](../../components/ReactBurgerMenu/ReactBurgerMenu.tsx)

Для этого нужно использовать блок-загрузчик `LazyLoader`.

### Как добавить свой компонент

Компонент ленивой загрузки лежит [тут](../LazyLoader).

Необходимо добавить свою обертку-загрузчик в `loaders/{componentName}/{componentName}@{platform}.tsx`.

После, добавить вызов загрузчка в `LazyLoader@{platform].tsx`

Если необходим рендер по условию, то нужно записать в `GlobalContext.lazyLoadRegistry` переменную,
а потом положить ее в пропсы компонента в адаптере.

```ts
conditionLoadList: {
    marketCart: lazyLoadRegistry.has('hasMarketCart')
    // ваша переменная
}
```

В компоненте

```tsx
{conditionLoadList.marketCart && <MarketCartDrawerLoader/>}
```

### Взаимодействие со старым стеком
Обратите внимание, на то что LazyLoader инициализируется гидрацией реакта.У нас нет гарантии того, что реакт проинициализируется раньше бэма.

Поэтому при необходимости организации общения загружаемого блока со старым стеком используйте [ReactBus](../../components/ReactBus) и не завязывайтесь на инциализацию старого стека в новом и наоборот.
