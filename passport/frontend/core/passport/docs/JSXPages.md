# Как сделать страницу на реакте

Создаем папку в pages с флагом `JSX=y`, например, `make pages/react/auth JSX=y`. Получаем:

```bash
$ ls -l pages/react/auth
total 16
-rw-r--r-- 1 y-i-demin y-i-demin 378 Jun  7 17:32 App.jsx
-rw-r--r-- 1 y-i-demin y-i-demin 320 Jun  7 17:32 configureStore.js
-rw-r--r-- 1 y-i-demin y-i-demin   0 Jun  7 17:32 opt.skipNanoislands
-rw-r--r-- 1 y-i-demin y-i-demin 919 Jun  7 17:32 auth.client.jsx
-rw-r--r-- 1 y-i-demin y-i-demin 473 Jun  7 17:32 auth.server.jsx
-rw-r--r-- 1 y-i-demin y-i-demin 127 Jun  7 17:32 Auth.styl
```

* Вероятно, стили наноостровов не нужны, поэтому сразу добавляем файл `opt.skipNanoislands`;
* `auth.client.jsx` и `auth.server.jsx` - точки входа для сборки webpack'ом, клиентский и серверный файл соответсвенно;
* `App.jsx` - само приложение;
* `configureStore.js` конфигуратор состояния приложения для redux;

```js
// routes

const serialize = require('serialize-javascript');
const config = require('../configs/current');
const reactTemplates = {};

[].concat(config.langs).forEach(function(lang) {
    reactTemplates[lang] = require(`../../templates/react.authv2.react.${lang}.js`);
});

function renderPage(req, res) {
    const getRootComponent = reactTemplates[res.locals.language];

    // стор лежит в res.locals.store
    res.locals.serializedStore = serialize(res.locals.store, {isJSON: true});

    getRootComponent.renderPage(req, res);
}
```

```jsx
// auth.server.jsx

import path from 'path';
import React from 'react';
import {Provider} from 'react-redux';
import {StaticRouter} from 'react-router-dom';
import {ChunkExtractor} from '@loadable/server';
import {renderToStaticMarkup, renderToNodeStream} from 'react-dom/server';
import createMemoryHistory from 'history/createMemoryHistory';
import classnames from 'classnames';
import configureStore from '@blocks/authv2/configureStore';
import App from '/App.jsx';
import {Head, Body} from '@components/Layout';
import {getDefaultLayoutProps} from '@blocks/selectors';

const renderPage = (req, res) => {
    const defaultLayoutProps = getDefaultLayoutProps(res.locals);
    const {store = {}, authPage, pdd_title: pddTitle} = res.locals;
    const {language, uatraits, display, page} = defaultLayoutProps;
    const {isTouch, isTablet} = uatraits;
    const {common = {}} = store;
    const {pane} = common;

    const layoutProps = {
        ...defaultLayoutProps,
        title: pddTitle ? pddTitle : i18n('Frontend.title.authorization'),
        isMagiclinkAuth: authPage === 'magiclink-auth'
    };

    const headClassName = classnames('is-js_no', {
        'is-touch': (isTouch && !isTablet) || display === 'touch',
        'is-tablet': isTablet
    });
    const html = `<html lang="${language}" data-page-type="${page}" class="${headClassName}">`;
    const head = renderToStaticMarkup(<Head {...layoutProps} />);
    const body = Body.getOpenBodyTag(layoutProps);

    res.type('html');
    res.write(`<!doctype html>${html}${head}${body}`, 'utf-8', {end: false});

    const context = {};
    const history = createMemoryHistory();
    const configuredStore = configureStore(store, history);
    const statsFile = path.resolve(`./loadable/${language}/loadable-stats.json`);
    const extractor = new ChunkExtractor({statsFile, entrypoints: [page]});
    const stream = renderToNodeStream(
        extractor.collectChunks(
            <Body {...layoutProps}>
                <Provider store={configuredStore}>
                    <StaticRouter location={pane} context={context}>
                        <App />
                    </StaticRouter>
                </Provider>
            </Body>
        )
    );

    const scriptTags = extractor.getScriptTags();
    const linkTags = extractor.getLinkTags();
    const styleTags = extractor.getStyleTags();

    stream.on('end', () => res.end(`${scriptTags}${linkTags}${styleTags}</body></html>`));
    stream.pipe(res);
};

export {renderPage};
```

```jsx
// auth.client.jsx

import './Auth.styl';
import React from 'react';
import {hydrate} from 'react-dom';
import {Provider} from 'react-redux';
import {ConnectedRouter} from 'connected-react-router';
import createBrowserHistory from 'history/createBrowserHistory';
import {loadableReady} from '@loadable/component';
import passport from '@plibs/pclientjs/js/passport';
import metrics from '@blocks/metrics';
import api from '@blocks/api';
import configureStore from './configureStore';
import App from '/App.jsx';

loadableReady(() => {
    const storeScript = document.querySelector('#storeScript');
    const reduxStore = window.__REDUX_STORE__;
    const history = createBrowserHistory();
    const store = configureStore(reduxStore, history);

    delete window.__REDUX_STORE__;
    storeScript.parentNode.removeChild(storeScript);

    api.init(store);
    passport.init();
    metrics.init(store);

    hydrate(
        <Provider store={store}>
            <ConnectedRouter history={history}>
                <App />
            </ConnectedRouter>
        </Provider>,
        document.getElementById('root')
    );

    metrics.send(['показ страницы']);
});
```
