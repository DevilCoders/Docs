## How to write CSS classes

Let's write PCSS-file for `app`-component.
```postcss
.app {
    margin: 10px 30px;
    
    &__section {
        margin-bottom: 15px;
    }

    &__title {
        font-size: 200%;
    }
}
```

Let's include PCSS-file into `app`-component:
```typescript jsx
import style from './app.pcss';

import * as React from 'react';
import bem from 'bem-css-modules';

const b = bem(style);

const App = () => (
    <div className={b()}>
        <div className={b('title')}>Hello, Wombat</div>
        <div className={b('section')}>{'Go to "src/client/components/app/app.tsx" and do your best!'}</div>
        <div className={b('wombat')} />
    </div>
);

export default App;
```

So now we can use the following notation to assign className attributes:
```
className={b()} // for 'app' class
className={b('title')}
className={b('section')}
```

We can have this feature because of webpack's pcss-loader,
which converts every pcss-file into a module.

### Look also
[CSS-модули](https://habrahabr.ru/post/270103/)
