# Jest-Allure-Image-Snapshot

> This is a clone of the external repository, which you can find at the [link](https://github.com/zaqqaz/jest-allure-image-snapshot).

Plugin for image comparison use [jest-image-snapshots](https://github.com/americanexpress/jest-image-snapshot/blob/master/examples/image-reporter.js) and beateaful allure reports using [jest-allure](https://github.com/zaqqaz/jest-allure-image-snapshot)

# Installation

```
yarn add -D @yandex-market/jest-allure-image-snapshot
```
or

```
npm install --save-dev @yandex-market/jest-allure-image-snapshot
```


You also should configure `setupTestFrameworkScriptFile`  if you don't have yet your own it will look so:

```
const registerAllureReporter = require("jest-allure/dist/setup").registerAllureReporter;
const registerAllureImageSnapshot = require("jest-allure-image-snapshot").registerAllureImageSnapshot;
registerAllureReporter();
registerAllureImageSnapshot({
    useCustomSnapshotsDir: false, 
});
```
If you want to use custom directory, you can change props:
```
registerAllureImageSnapshot({
    useCustomSnapshotsDir: true,
    customSnapshotsDir: '__image_snapshots__', 
});
```
