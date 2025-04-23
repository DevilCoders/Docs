### Section - компонент для блока с отступами, фоном и возможностью закруглять края

Статья:

```jsx
const generateLoremIpsum = require('../../styleguide/components/lorem-ipsum/LoremIpsum').generate;

<Article>
    <h1>{generateLoremIpsum(5)}</h1>
    <p>{generateLoremIpsum(40)}</p>

    <h2>{generateLoremIpsum(10)}</h2>
    <p>{generateLoremIpsum(10)}</p>
    <p>
        {generateLoremIpsum(30)}<br/>
        <span>({generateLoremIpsum(2)})</span>
    </p>
    
    <h3>{generateLoremIpsum(2)}</h3>
    <p>{generateLoremIpsum(5)}</p>
    <ol>
        <li>{generateLoremIpsum(5)}</li>
        <li>{generateLoremIpsum(10)}</li>
        <li>{generateLoremIpsum(85)}</li>
        <li>{generateLoremIpsum(3)}</li>
    </ol>
    
    <p>{generateLoremIpsum(15)}</p>
    <ul>
        <li>{generateLoremIpsum(5)}</li>
        <li>{generateLoremIpsum(10)}</li>
        <li>{generateLoremIpsum(85)}</li>
        <li>{generateLoremIpsum(3)}</li>
    </ul>

    <p>{generateLoremIpsum(12)}</p>
    <hr/>
    <p>{generateLoremIpsum(14)}</p>
    
    <h2>{generateLoremIpsum(12)}</h2>
    <h3>{generateLoremIpsum(5)}</h3>
    
    <blockquote cite="taxi.yandex.ru">{generateLoremIpsum(50)}</blockquote>
    <p>{generateLoremIpsum(10)}</p>

    <ol>
        <li>{generateLoremIpsum(5)}</li>
        <li>{generateLoremIpsum(15)}</li>
        <li>{generateLoremIpsum(65)}</li>
        <li>{generateLoremIpsum(10)}
            <ol>
                <li>{generateLoremIpsum(5)}</li>
                <li>{generateLoremIpsum(5)}</li>
                <li>{generateLoremIpsum(85)}</li>
                <li>{generateLoremIpsum(12)}</li>
            </ol>
        </li>
    </ol>
    <p>{generateLoremIpsum(10)}</p>
</Article>
```
