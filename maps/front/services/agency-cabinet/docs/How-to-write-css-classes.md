## How to write CSS classes

Let's write CSS-file for `app`-component.
```css
.app {
    margin: 10px 30px;
}

.section {
    margin-bottom: 15px;
}

.title {
    font-size: 200%;
}
```

Let's include CSS-file into `app`-component:
```js
import styles from './app.css';

const App = () => (
    <div className={styles.app}>
        <p className={styles.title}>Hello, Wombatt.</p>
        <p className={styles.section}>{'Go to "client/components/app/app.jsx" and do your best!'}</p>
    </div>
);

export default App;
```

Look at first row: `import styles from './app.css';` It does one amazing thing — this operator imports names of classes as hash.

So now we can use object notation in className attributes:
```
className={styles.app}
className={styles.title}
className={styles.section}
```

We can have this feature because of webpack's css-loader, wich makes every css-file as module

### Look also
[CSS-модули](https://habrahabr.ru/post/270103/)
