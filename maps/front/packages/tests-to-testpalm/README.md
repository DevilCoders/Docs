# `@yandex-int/tests-to-testpalm`

Package for sync your hermione tests with test palm.

## Installation

Also install `hermione`.

```sh
npm i -D @yandex-int/tests-to-testpalm
```

## Usage

Configuration in your custom file `tests/config.ts`:

```js
export default {
    testPalm: {
        projectId: 'PROJECT_ID',
        token: process.env.TESTPALM_OAUTH_TOKEN
    },
    // Array with globs.
    filePatterns: [
        path.join(__dirname, '../tests/sets/mobile/**/*.ts')
    ],
    // Optional
    getComponentByFile: (filePath: string) => {
        const [componentDirName] = filePath.split('/');
        return componentDirName;
    },
    // Add other commands
    browserStubs: {
        attributes: {
            openPage: () => {}
        },
        description: {
            openPage: (url) => `Open page with next url "${url}"`
        },
        estimate: {
            openPage: () => 1
        }
    },
    minEstimate: 2 * 60 * 1000,
    getSelectorsDescriptions: () => {
        '.selector': {
            description: 'Human-readable description for selector',
            screenshot: 'link-to-image or null'
        }
    },
    report: {
        folder: './path/to/folder',
        name: `synced-hermione`
    },
    engine: ENGINE.HERMIONE,
    stQueue: 'MAPSUI'
};
```

Then sync cases:

```sh
npx tests-to-testpalm sync --config ./tests/config.ts --mode dry-run
```

Modes:

-   `dry-run` (default)
-   `validation` — don't compare local cases with remote cases in test-palm. Use case: pre-commit hooks.
-   `full`

As result:

-   JSON report
-   HTML report with testpalm-like views.
-   Output with additional information about commands and selectors.

## Hermione plugin

Connect hermione plugin in `.hermione.conf.js`:

```js
module.exports = {
    // ...
    plugins: {
        // ...
        '@yandex-int/hermione-to-test-palm/out/hermione/plugin': {}
    }
};
```

With this plugin you can do next things:

1. Use `browser.perform(async () => {}, 'description of actions')` command.
2. Change component for some `describe` and `it`: `hermione.testPalm.setComponent('my-component')`.

## Contributing

Publish:

```sh
npm version major | minor | patch
arc push
```
