# Recommended build scripts for projects on React and TypeScript

It's configurable dev and prod scripts for React applications on TypeScript. Inspired by [Create React App](https://github.com/facebook/create-react-app) and [React App Rewired](https://github.com/timarney/react-app-rewired).

## Usage

### Templar middleware

> NODE_ENV=development templar start --middleware='@yandex-int/react-ts-scripts/middlewares/templar-hmr'

### HMR middleware client

If you want to customise entry paths you need to add `@yandex-int/react-ts-scripts/middlewares/client-hmr` as last chunk in your entry.

### CLI

#### Start with webpack-dev-server

> react-ts-scripts start

#### Build static assets

> react-ts-scripts build

### NodeJS API

#### Start with webpack-dev-server

``` js
const { start } = require('@yandex-int/react-ts-scripts/scripts/start');

(async () => {
    await start();
})();
```


#### Build static assets

``` js
const { build } = require('@yandex-int/react-ts-scripts/scripts/build');

(async () => {
    await build();
})();
```

### Configs overrides

Create `react-ts-scripts.js` in your project root.

``` js
modules.exports = {
    // Override default project settings
    paths(paths) {
        paths.entry = [
            './path/to/my/entry',
            '@yandex-int/react-ts-scripts/middlewares/client-hmr'
        ];

        return paths;
    },
    // Override webpack config. DANGER ZONE!
    webpack(config) {
        config.module.rules[0].oneOf[2].use = config.module.rules[0].oneOf[2].use
            .filter({ loader } => !loader.includes('postcss-loader'));

        return config;
    },
    vars(vars) {/* ... */}
};
```

## Globals

- `process.env.DEBUG` — shows debug log and static file sizes after build, default: `false`
- `process.env.WEBPACK_NO_HMR` — disable HMR for the local testing, default: `false`
- `process.env.HOST` — host for webpack-dev-server, default: `0.0.0.0`
- `process.env.PORT` — port for webpack-dev-server, default: `3000`
- `process.env.HTTPS` — secure testing, default: `false`
- `process.env.DANGEROUSLY_DISABLE_HOST_CHECK` — base host checking for webpack-dev-server, default: `false`
- `process.env.WEBPACK_DEV_SERVER_LOG_LEVEL` — logging level for webpack-dev-server, default: `warn`
- `process.env.PUBLIC_URL` — base application url, will be passed to React ENV
