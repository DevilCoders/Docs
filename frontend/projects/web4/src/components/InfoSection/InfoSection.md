# InfoSection

Инфо блок

## Использование
```typescript
<InfoSection /* props */ />
```


## Props
```typescript
export interface IInfoSectionLinkProps {
    /**
     * Адрес ссылки, на которую переведет событие нажатия на карточку
     * @default 'https://ya.ru'
     */
    url?: string;
}

export type TTextProps = IInfoSectionLinkProps & {
    text: string;

    /**
     * Стиль оформления и оборачивание в ссылку, если выбрано "link"
     * @default 'info' для верхней строки и 'footnote' для нижней
     */
    type?: 'hidden' | 'link' | 'info' | 'footnote';

    /**
     * Кол-во видимых строк
     * @default 1
     */
    lines?: 1 | 2 | 3;
}

export interface IInfoSectionTextProps {
    primaryText: TTextProps;
    secondaryText?: TTextProps;
}

export type TClickOutProps = IInfoSectionLinkProps & {
    type?: 'none' | 'arrow' | 'button';

    /**
     * Текст на кнопке, если выбран тип "button"
     */
    buttonText?: string;

    /**
     * Размер кнопки, если выбран тип "button" - 'm' | 's'
     * @default 'm'
     */
    buttonSize?: TButtonSize;
}

export interface IInfoSectionClickOutProps {
    clickOutProps?: TClickOutProps;
}

export type TThumbType = 'none' | 's' | 'm' | 'l' | 'xl' | 'bulk';

export interface IInfoSectionThumbProps {
    /**
     * Режим отображения картинки (картинок)
     * @default 'none'
     */
    thumbType?: TThumbType;

    /**
     * Отступ картинки от края разрешенной области (обрамление серым фоном)
     * Работает только в режимах 'm' | 'l'
     * @default 0
     */
    imagePadding?: number;

    /**
     * Урлы картинок.
     * В режимах, отличных от "bulk", будет использована только первая картинка в массиве
     */
    images?: string[];
}

export interface IInfoSectionProps
    extends
        IClassNameProps,
        IInfoSectionLinkProps,
        IInfoSectionThumbProps,
        IInfoSectionTextProps,
        IInfoSectionClickOutProps {
    /**
     * Разделительная черта над блоком
     */
    divider?: boolean;
}
```