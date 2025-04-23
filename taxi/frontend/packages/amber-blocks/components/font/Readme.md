Шрифты.

`import 'amber-blocks/font/font.styl'`

```jsx harmony
require('./font.styl');
const LoremIpsum = require('../../styleguide/components/lorem-ipsum/LoremIpsum').default;

const FONTS = [
    {name: 'YS Text', weights: [300, 400, 500, 700]},
    {name: 'YS Display', weights: [400, 500, 700]},
    {name: 'Yandex Sans Display', weights: [400]},
    {name: 'Yandex Sans Text Web', weights: [300, 400, 500, 700]}
];

<div style={{fontSize: 17}}>
    {FONTS.map(({name, weights}) => (
        <article style={{fontFamily: name}} key={name}>
            <h2>{name}</h2>
            {weights.map(weight => (
                <div key={weight} style={{paddingLeft: 32}}>
                    <h4 style={{fontWeight: weight}}>{weight}</h4>
                    <p style={{fontWeight: weight}}><LoremIpsum n={50}/></p>
                </div>
            ))}
        </article>
    ))}
</div>
```
