# GreenUrl

Компонент Гринурла для продуктовых карточек

## Использование
```jsx
<GreenUrl {...props} />

```


## Props
```typescript
/**
 * Ссылка для гринурла
 */
url?: string;

/**
 * Открывать в новой или текущей вкладке
 */
target?: '_self' | '_blank' | '_parent' | '_top';

/**
 * Текст для гринурла
 */
text?: string;

/**
 * Тема для гринурла
 * outer - Зеленая
 * ghost - Серая
 * @default 'outer'
 */
theme?: 'outer' | 'ghost';

/**
 * Болдирование гринурла
 * bold - Жирный
 * normal - Обычный
 * @default 'bold'
 */
fontWeight?: 'normal' | 'bold';

/**
 * Флаг, означающий что это продуктовая карточка Директа
 */
isDirect?: true;

```