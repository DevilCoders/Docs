# hermione-testpalm-steps

Plugin for [hermione](https://github.com/gemini-testing/hermione) which is intended to add TestPalm steps for each test. For the plugin to work properly, it is expected that the [palmsync](https://github.yandex-team.ru/search-interfaces/infratest/tree/master/packages/palmsync) is available in your environment

You can read more about hermione plugins [here](https://github.com/gemini-testing/hermione#plugins).

## Installation

```bash
$ npm install @yandex-int/hermione-testpalm-steps
```

## Usage

Plugin has following configuration:

* **enabled** (optional) `Boolean` – enable/disable the plugin; by default plugin is enabled
* **scenarioType** (optional) `String` – scenario type for find test case; by default "specs"; possible values: "specs", "specs-integration"

Also there is ability to override plugin parameters by CLI options or environment variables
(see [configparser](https://github.com/gemini-testing/configparser)).
Use `hermione_testpalm_steps_` prefix for the environment variables and `--hermione-testpalm-steps-` for the cli options.

Add plugin to your `hermione` config file:

```js
module.exports = {
    // ...
    system: {
        plugins: {
            '@yandex-int/hermione-testpalm-steps': {
                enabled: true
            }
        }
    },
    //...
}
```

## Testing

Run [mocha](http://mochajs.org) tests:
```bash
npm run unit
```

Run [eslint](http://eslint.org) codestyle verification
```bash
npm run lint
```
