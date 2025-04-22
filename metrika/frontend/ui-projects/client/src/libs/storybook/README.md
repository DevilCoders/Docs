# Storybook utils

* Для получения метаданных компонента (export default в story файле) необходимо вызвать метод `getComponentStoriesMeta`
* Для создания Primary story с возможностью конфигурации пропсов в интерфейсе из фигмы необходимо вызвать метод `createPrimaryStory`
* Для создания простой story c фиксированным набором пропсов используется метод `createStory`
* Для создания story с набором состояний компонента используется метод `createMultiStory`
* Пример создания story с перечисляемыми значениями одного свойства:
```
export const Story = createMultiStory(
    getSimpleMultiStoryProps(
        MyComponent,
        componentProps,
        'myProp',
        [myPropsVal1, myPropsVal2, myPropsVal2]
    )
);
```

* Пример создания story с перечисляемыми значениями нескольких свойств:

```
export const View = createMultiStory({
    component: MyComponent,
    groups: [
        getPropertiesGroup<ButtonProps, 'view'>(
            componentProps1,
            'myProp1',
            [myPropsVal11, myPropsVal12, myPropsVal13]
        ),
        getPropertiesGroup<ButtonProps, 'view'>(
            componentProps2,
            'myProp2',
            [myPropsVal21, myPropsVal22, myPropsVal23]
        )
    ]
}));
```

* Пример более полного и гибкого формата (необходим для контроля заголовков и в случае сложного тайпинга)

```
export const TextButtonWithIcon = createMultiStory({
    component: Button,
    groups: [{
        items: getPropsSetForValues(
            defaultTextProps,
            'iconLeft',
            [
                <PlusIcon color="currentColor" size={16}/>,
                <BellIcon color="currentColor" size={32}/>
            ]
        ),
    }, {
        items: getPropsSetForValues(
            defaultTextProps,
            'iconRight',
            [
                <PlusIcon color="currentColor" size={16}/>,
                <BellIcon color="currentColor" size={32}/>
            ]
        )
    }]
});

```

* Для того, чтобы добавить description надо обернуть story в метод withDescription. Пример:

```
export const View = withDescription('Button view properties', createMultiStory({
    component: Button,
    groups: [
        getPropertiesGroup<ButtonProps, 'view'>(
            defaultTextProps,
            'view',
            [ButtonView.Shade, ButtonView.Contrast]
        ),
        getPropertiesGroup<ButtonProps, 'view'>(
            defaultIconProps,
            'view',
            [ButtonView.Shade, ButtonView.Contrast]
        )
    ]
}));

```

* Для того, чтобы добавить макет с дизайном на отдельный Story его надо обернуть в метод withDesign. Пример:

```
export const Main = withDesign(designUrl, createPrimaryStory(
    Button,
    defaultTextProps
));
```
