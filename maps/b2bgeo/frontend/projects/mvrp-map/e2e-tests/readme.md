# Functional Autotests

For tests, [cypress](https://docs.cypress.io) is used

# Require

- `node@14`

# Run

## Main scripts

### Run on exist stand

**Berore run** Edit your .env file

ex.

```bash
CYPRESS_BASE_URL=https://l7test.yandex.ru/courier/mvrp-map/BBGEO-14697/
```

#### Run on terminal

```bash
npm run e2e:ci
```

#### Run with cypress view

```bash
npm run cypress-open
```

### Run on local stand

**Before run**

run local project (in other terminal)

```bash
cd ../
npm start
```

# Report

Report will be created by two ways:

1. in terminal
2. `cypress/report` in report directory

# What to do with failed test

If the reason is minor (new element's classname or something like that), it can be fixed right away (by putting new CSS-selector in `./src/constants/selectors.ts` for example).

# Other info

If test data is broken, it possible to regenerate it by `npm run generate-data`.
Be careful with this command, because it flushes current test data and running tests will fall.

# Debugging

Set `it.only` in testcase to debug.

# Testing hover events (native system events)

Cypress doesn’t provide any native commands like cy.hover() to hover over elements, instead it provides a [few workaround to achieve this](https://docs.cypress.io/api/commands/hover#Workarounds).

If trigger and invoke methods don't work, use [real-hover-events](https://github.com/dmtrKovalenko/cypress-real-events) for testing.

* Plugin added to the project
* [Another available real event commands](https://github.com/dmtrKovalenko/cypress-real-events#api)
