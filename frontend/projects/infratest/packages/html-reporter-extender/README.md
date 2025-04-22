# html-reporter-extender

Plugin for [hermione](https://github.com/gemini-testing/hermione) and [gemini](https://github.com/gemini-testing/gemini) which is intended to add external information to [html-report](https://github.com/gemini-testing/html-reporter).

You can read more about hermione plugins [here](https://github.com/gemini-testing/hermione#plugins) and about gemini plugins [here](https://github.com/gemini-testing/gemini#plugins).

## Installation

```bash
$ npm install @yandex-int/html-reporter-extender
```

## Usage

Plugin has following configuration:

* **enabled** (optional) `Boolean` – enable/disable the plugin; by default plugin is enabled
* **extraItems** (optional) `Boolean` – external information for html-reporter plugin; by default is empty object
* **s3Images** (optional) `Object` - [s3 config](#s3-config) for images.
* **s3ReportData** (optional) `Object` - [s3 config](#s3-config) for sqlite dbs.

Also you can override plugin parameters by CLI options or environment variables
(see [configparser](https://github.com/gemini-testing/configparser)).
Use `html_reporter_extender_` prefix for the environment variables and `--html-reporter-extender-` for the cli options.

### s3 config

s3 storage configuration `Object`. Read more about external storage [here](https://github.com/gemini-testing/html-reporter/#externalstorage).

Allowed s3 config fields:

* **enabled** (optional) `Boolean` - enable/disable saving in s3 storage; `false` by default
* **endpoint** (optional) `String` - endpoint in s3 storage, `https://s3.mds.yandex.net` by default
* **bucket** (optional) `String` - bucket name in s3 storage, `hermione-tests-report` by default
* **accessKeyId** (optional) `String` - vault path of s3 accessKeyId in [yav](https://yav.yandex-team.ru) in format `<vault-id>[#<key>]`. If `key` not specified than the first one value will be used.
* **secretAccessKey** (optional) `String` - vault path of s3 secretAccessKey in [yav](https://yav.yandex-team.ru) in format `<vault-id>[#<key>]`. If `key` not specified than the first one value will be used.
* **path** (optional) `String` - path to folder in s3 storage.

### example

Add plugin to your `hermione` or `gemini` config file:

```js
module.exports = {
    // ...
    system: {
        plugins: {
            '@yandex-int/hermione-report-extender': {
                enabled: true,
                extraItems: {foo: 'bar'}
            }
        }
    },
    // ...
}
```

After that you can pass external information in json format to `html-reporter` using environment: `HTML_REPORTER_EXTRA_ITEMS='{"sandbox task": "https://sandbox.yandex-team.ru/task/123456"}'`

## Testing

Run [mocha](http://mochajs.org) tests:
```bash
npm run unit
```

Run [eslint](http://eslint.org) codestyle verification
```bash
npm run lint
```
