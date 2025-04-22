# hermione-searchapp-commands

Plugin for [hermione](https://github.com/gemini-testing/hermione) which is intended to add/wrap browser commands in order to work properly with the search application.

You can read more about hermione plugins [here](https://github.com/gemini-testing/hermione#plugins).

## Installation

```bash
$ npm install @yandex-int/hermione-searchapp-commands
```

## Usage

Plugin has following configuration:

* **enabled** (optional) `Boolean` – enable/disable the plugin; by default plugin is enabled
* **browsers** (required) `Object` - the list of browsers to use for wrap commands
  * **commands** (required) `Array` - commands which will be wrapped
  * **webViewContext** (required) `String` - web view context name
  * **orientation** (optinal) `String` - browser orientation (`portrait`, `landscape`) that will be set before each test run. Default value is `null`.
  * **waitTabInit** (optinal) `Number` - pause to wait until new tab will be initialized. Default value is `200` ms
  * **waitRequestCompleted** (optinal) `Number` - pause to wait until request completed. Default value is `20000` ms
  * **bodyLoadTimeout** (optinal) `Number` - timeout wait for visible 'body > *'. Default value is `20000` ms
  * **grantPermissions** (optinal) `String|Array(Stirng)` - [android permissions](https://developer.android.com/guide/topics/permissions/overview) which will be granted to the app before any request is executed
  * **targetHost** (optional) `String` - host on which application will go for data. Default value is `serp`. Available values can be found [here](https://wiki.yandex-team.ru/mobilesearch/app/android/tzdljarazrabotki/morda/links/#customhost)
  * **verticalTab** (optional) `String` - name of vertical tab (serp, images, video, ...) which will be opened after make request. Default value is `serp`.

Also there is ability to override plugin parameters by CLI options or environment variables
(see [configparser](https://github.com/gemini-testing/configparser)).
Use `hermione_searchapp_commands_` prefix for the environment variables and `--hermione-searchapp-commands-` for the cli options.

Add plugin to your `hermione` config file:

```js
module.exports = {
    // ...
    system: {
        plugins: {
            '@yandex-int/hermione-searchapp-commands': {
                enabled: true,
                browsers: {
                    searchapp: {
                        commands: [
                            'url',
                            'deleteCookie'
                        ],
                        webViewContext: 'context-name'
                    }
                }
            }
        }
    },
    //...
}
```

### Existing searchapp commands:

Wrappers over existing commands:

* **url** - replaces wdio "url" in order to make request inside native app, if wdio "url" command will be called then internal searchapp browser will be launched
* **click** - wrapper of wdio "click" in order to correct switch between tabs when opening a new one or closing the current. If you want to stay on the tab after click (do not switch), add second argument – `{ leavePage: false }` when calling click-command (by default `leavePage` is true), and the pure wdio-click-command will be called.

  Also this command takes into account if leavePage-option is set in hermione-context. For example, a complex command can set leavePage-option to false in hermione-context, so that any click-command running in its context would not try to switch a current tab to a new one. But if you specify `leavePage`-option in a click-command explicitly, a `leavePage`-value in hermione-context will be ignored.
* **touchAction** - wrapper of wdio "touchAction" in order to correct switch between tabs when opening a new or closing current
* **screenshot** - wrapper of wdio "screenshot" in order to cut the native header from the final image
* **orientation** - wrapper of wdio "orientation" in order to change device orientation in native context
* **deleteCookie** - wrapper of wdio "deleteCookie", because it does not work in native context

Commands to work with native elements:

* **appClickTab** - command to click on the native application tab buttons (first tab has number one, not a zero)
* **appClickHistoryBack** - command to click on native application "Back" button, which sends the user to the previous page of history
* **appClickOmnibox** - command to click on native omnibox (search bar)
* **appClickOmniboxClear** - command to click on the native cross in omnibox in order to clear the text query (works when the omnibox is in focus)
* **appGetOmniboxText** - command to get text from native omnibox
* **appGetHistReqText** - command to get text from a native list of query history (returns an array of strings with the entire query history)
* **deviceClickBack** - command to click back button on device
* **switchToSearchTab** - command to switch to search tab

### Commands usage:

#### appClickTab

```js
browser.appClickTab(1); // will be click on first tab (currently it is `sites`)
browser.appClickTab(2); // will be click on second tab (currently it is `images`)
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
