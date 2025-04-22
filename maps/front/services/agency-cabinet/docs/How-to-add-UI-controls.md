## How to add UI controls

There are at least two UI-libraries with React-components in Yandex.
1. [y-components](https://github.yandex-team.ru/y-components/y-components)
2. [Lego on React](https://github.yandex-team.ru/lego/islands/tree/dev/contribs/lego-on-react)

### How to add Y-components
Developed by Anton Grischenko's team at Ekaterinburg.
[See demo page](https://github.yandex-team.ru/pages/y-components/y-components/).

1. Install `y-components` as production dependency
    ```sh
    npm i --save y-components
    ```

2. Import css-file into `/client/components/app/app.jsx`:
    ```diff
     import styles from './app.css';
    +import '!style-loader!css-loader!postcss-loader!../../../node_modules/y-components/dist/main.css';

     // ...
    ```
----
_**Note!**_

_You've imported `app.css` as a CSS Module for using styles as object `styles.app`, `styles.section` etc. But for
using Y-components this feature is odd — we have to import its styles as is. That's why we import
y-components's styles with `!style-loader!css-loader!postcss-loader!`_

----

3. Import needed components into you component:
    ```diff
     import styles from './app.css';
     import '!style-loader!css-loader!postcss-loader!../../../node_modules/y-components/dist/main.css';

    +import {YInput, YButton} from 'y-components';

     const App = () => (
         <div className={styles.app}>
             <p className={styles.title}>Hello, Wombatt.</p>
             <p className={styles.section}>{'Go to "client/components/app/app.jsx" and do your best!'}</p>

    +        <YInput />
    +        <YButton size="s">My button</YButton>
         </div>
     );

     export default App;
    ```
