Предоставляет набор классов для оформления текста.

`import tpClassNames from 'amber-blocks/typography'`

Доступный набор элементов
```jsx
const tp = require('./');

<pre className={tp.caps}>{Object.keys(tp).join('\n')}</pre>
```

```jsx
require('./_demo.styl');

const tp = require('./');

<div className={tp.b}>
    <div className="demo-typography__layout">
        <div className="demo-typography__column">
            <div className="demo-typography__row">
                <div className="demo-typography__column-title">className</div>
            </div>
            <div className="demo-typography__row">
                <div className={tp.caps}>caps</div>
            </div>
            <div className="demo-typography__row">
                <div className={tp.caption}>caption</div>
            </div>
            <div className="demo-typography__row">
                <div className={tp.body1}>body1</div>
            </div>
            <div className="demo-typography__row">
                <div className={tp.body2}>body2</div>
            </div>
            <div className="demo-typography__row">
                <div className={tp.headline}>headline</div>
            </div>
            <div className="demo-typography__row">
                <div className={tp.title}>title</div>
            </div>
        </div>

        <div className="demo-typography__column">
            <div className="demo-typography__row">
                <div className="demo-typography__column-title">Размеры</div>
            </div>
            <div className="demo-typography__row">
                <div className={tp.caps}>CAPS — 10/16px</div>
                <div className={tp.caption}>всякие подписи к пунктам меню или лейблам</div>
                <div className={tp.caps}>{`<span>|<p>`}</div>
            </div>
            <div className="demo-typography__row">
                <div className={tp.caption}>Caption — 12/16px</div>
                <div className={tp.caption}>любой мелкий второстепенный текст, подписи, подзаголовки</div>
                <div className={tp.caps}>{`<p>`}</div>
            </div>
            <div className="demo-typography__row">
                <div className={tp.body1}>Body 1 — 14/20px</div>
                <div className={tp.caption}>основной наборный, используется в контролах</div>
                <div className={tp.caps}>{`<p>`}</div>
            </div>
            <div className="demo-typography__row">
                <div className={tp.body2}>Body 2 — 17/26px</div>
                <div className={tp.caption}>увеличенный наборный, для коммуникации и промо</div>
                <div className={tp.caps}>{`<p>`}</div>
            </div>
            <div className="demo-typography__row">
                <div className={tp.headline}>Headline — 20/24px</div>
                <div className={tp.caption}>локальный заголовок</div>
                <div className={tp.caps}>{`<h2?>`}</div>
            </div>
            <div className="demo-typography__row">
                <div className={tp.title}>Title — 32/36px</div>
                <div className={tp.caption}>основной заголовок экрана</div>
                <div className={tp.caps}>{`<h1>`}</div>
            </div>
        </div>
    </div>
</div>
```
