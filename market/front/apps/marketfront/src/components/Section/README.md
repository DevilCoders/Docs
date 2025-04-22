Некоторая часть страницы — глава или раздел. Имеет небольшой набор параметров, который позволяет организовывать и оформлять содержимое страницы.
N.B: Вертикальные линии, пересекающие некоторые примеры нужны, чтобы показать границы сетки. В реальной жизни вставлять Section внутрь родителя с рамкой не рекомендуется.

## Песочница
```jsx noeditor
import Title from '@self/root/src/uikit/components/Title';

<Helper.Playground
    component={Section}
    settings={{background: 'transparent'}}
    example={props => (
        <Section {...props}>
            <Title>
                Широкая электрификация южных губерний даст мощный толчок подъёму сельского хозяйства.
            </Title>
        </Section>
    )}
/>
```

## Параметры

### `title`
Заголовок секции.

```jsx
<div>
    <Section
        title="Заголовок секции"
    />
</div>
```

### `actionElem`
Ключевое действие секции, например, показать все элементы на отдельной странице или очистить содержимое.

```jsx
import Button from '@self/root/src/uikit/components/Button';
import Link from '@self/root/src/components/Link';

<div>
    <Section
        title="Заголовок секции со ссылкой"
        actionElem={<Link url="#">Ссылка</Link>}
    />

    <Section
        title="Заголовок секции с кнопкой"
        actionElem={<Button>Кнопка</Button>}
    />
</div>
```

### `theme`
Секция имеет цветовые вариации для адаптации текста к оформлению. Доступные значения dark, light (по умолчанию).
```jsx
import Text from '@self/root/src/uikit/components/Text';

const demoContainer = {
   outline: 'solid 1px #dcdcdc',
   maxWidth: '1200px',
   margin: 'auto',
};
const demoContent = {
    background: 'rgba(255,255,255,0.2)',
    padding: '20px 0',
    height: '60px',
    color: '#fff'
};

<div>
    <Section
        theme="light"
        title="Секция с темой light"
    >
        <Text>Контент секции</Text>
    </Section>

    <Section
        theme="dark"
        backgroundColor="#000"
        title="Секция с темой dark"
    >
        <Text>Контент секции</Text>
    </Section>
</div>
```

### `padding`
Верхнее и нижнее расстояние от края секции может быть нормальным, разряженным или сжатым, а также может задаваться по отдельности через параметры paddingTop и paddingBottom. Доступные значения normal (по умолчанию), condensed, extended.
Так же возможное значение 'none' для случаев, когда паддинги нужно схлопнуть.
```jsx
import Text from '@self/root/src/uikit/components/Text';

<div>
    <Section
        title="Заголовок"
        paddingTop="condensed"
        paddingBottom="extended"
    >
        <Text>
            paddingTop="condensed"
            paddingBottom="extended"
        </Text>
    </Section>

    <Section
        title="Заголовок"
        paddingTop="none"
        paddingBottom="none"
    >
        <Text>
            paddingTop="none"
            paddingBottom="none"
        </Text>
    </Section>
</div>

```

### `background`
Можно передать параметры для настройки фона через соответствующие параметры: backgroundImage, backgroundSize, backgroundPosition, backgroundColor.

```jsx
import Text from '@self/root/src/uikit/components/Text';

<div>
    <Section
        title="Заголовок"
        backgroundColor="#dd3b3d"
    >
        <Text>
            backgroundColor=#dd3b3d
        </Text>
    </Section>
</div>
```

### Якорь

Можно передавать якорь в параметре `anchor`, который появится в заголовке.

### `titleAlign`
Выравнивание заголовка

```jsx
import Text from '@self/root/src/uikit/components/Text';

<div>
    <Section
        title="Заголовок секции"
        titleAlign='center'
    >
        <Text>
            titleAlign=center
        </Text>
    </Section>
</div>
```
