# End-to-end tests

> Extensions in Chrome / Chromium currently only work in **non-headless** mode.
> It is not yet possible to test extension popups or content scripts.

## How to write tests

1. Use docs:
   - [Puppeteer](https://github.com/puppeteer/puppeteer#puppeteer)
   - [Jest](https://jestjs.io/docs/en/getting-started)
2. Put your tests in `__tests__` folder
3. Build chrome extension from *static* repo: `npm run unpack-chrome-extension`
4. Make sure `src/randomizer.js` is saving names (`this.saveNames = true;`)
5. Put your extension into `build/chrome` folder

## Setup

```sh
nvm use
npm i
```

## How to run

```sh
# run all tests
npm t

# run specific test
npm t <test_name>
```

### Watch mode

```sh
npm run test:watch
```

## Debug mode

Runs an actual browser.

```sh
npm run dbg
```
