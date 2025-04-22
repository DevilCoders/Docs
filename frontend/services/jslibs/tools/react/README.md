# ReactJS

React для yastatic

Добавление новой версии:
```bash
› npm ci
› ./get.sh <react-version>
```

Реакт скачивается с [официального CDN](https://reactjs.org/docs/cdn-links.html).

Версии полифилов указываются в `package.json`.

В сборку `react-with-dom-and-polyfills` входят полифилы, [рекомендуемые командой реакта](https://reactjs.org/docs/javascript-environment-requirements.html) (`Map`, `Set`, `requestAnimationFrame`), а также полифил `Promise`, поскольку он является часто используемым и может потребоваться на ранних этапах загрузки страницы.
