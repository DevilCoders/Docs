# Functional Autotests

##  ENV Setup

It's necessary to have some environment variables: selenium grid `E2E_TESTS_API_TOKEN`, `API_URL`, `API_KEY`, `E2E_TEST_USER_PASSWORD` and testing `BRANCH_NAME`

Put same code in `./.env`
See example in `./.env.example`

```
NODE_ENV=development
API_URL=https://test.courier.yandex.ru/api/v1
E2E_TESTS_API_TOKEN='E2E_TESTS_API_TOKEN'
API_KEY='API_KEY'
E2E_TEST_USER_PASSWORD='E2E_TEST_USER_PASSWORD'
BRANCH_NAME=11171-r2021-09-09
TUS_OAUTH_TOKEN='TUS_OAUTH_TOKEN'
BASE_URL=https://l7test.yandex.ru/courier/11171-r2021-09-09/

```

- `BRANCH_NAME` - uniq key for generate data
- `API_KEY` - company token. You can get it from company settings in testing UI
<details>
  <summary>Link to Yav.E2E_TESTS_API_KEY</summary>
  https://yav.yandex-team.ru/secret/sec-01ej68yy1gb9zz3tysatv7438z/explore/versions
</details>

- `E2E_TESTS_API_TOKEN` - user OAuth token.
<details>
  <summary>Link to Ya.robot-b2bgeo-test-super_user</summary>
  https://yav.yandex-team.ru/secret/sec-01ddnqnfh237cr58aggnrknxfm/explore/versions
</details>

- `E2E_TEST_USER_PASSWORD` - test user passport passwords.
<details>
  <summary>Link to Yav.E2E_TEST_USER_PASSWORD</summary>
  https://yav.yandex-team.ru/secret/sec-01ed8y4pety32g7fv6vark1p1e/explore/versions
</details>

- `TUS_OAUTH_TOKEN` - Token for creating users
<details>
  <summary>Link for TUS_OAUTH_TOKEN</summary>
  https://oauth.yandex-team.ru/authorize?response_type=token&client_id=9052de6e4cf142039a7ee44ac03e4614
</details>

### Script for get `API_KEY`, `E2E_TESTS_API_TOKEN` and `E2E_TEST_USER_PASSWORD`

1. get `YAV_TOKEN` [Link to get yav oauth](https://oauth.yandex-team.ru/authorize?response_type=token&client_id=ce68fbebc76c4ffda974049083729982)
2. save `YAV_TOKEN` in your env (bash/ zsh)
3. `npm run get-secrets`

# Run

## Main scripts

### Run on exist stand

**Berore run** Edit your .env file

ex.

```bash
BASE_URL=https://l7test.yandex.ru/courier/11171-r2021-09-09/
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

**Berore run**

1. edit your .env file
   ex.

```bash
BASE_URL=https://https://localhost.msup.yandex.ru:8082/courier/
```

2. run local project (in other terminal)

```bash
cd ../
npm run magic
```

#### Run on terminal

```bash
npm run e2e:ci
```

#### Run with cypress view

```bash
npm run cypress-open
```

# Generate test data

Before each run need generate test data and after each - remove

## With handles

```bash
npm run e2e:generate-data # generate data
npm run e2e:remove-data #remove data
```

## Auto

Before each test run test data will be generate by `pre...` and `post...` scripts
Like

```bash
"precypress-open": "npm run e2e:generate-data", # generate data
"cypress-open": "...", # run e2e test
"postcypress-open": "npm run e2e:remove-data", # remove data
```

## How to add a new data generation for an e2e tests

1. Add a data type into the [types/schema.ts](../generate-data/src/types/schema.ts) and add a data into the [schema.ts](./src/generating-data/schema.ts)
2. Add a `create<YourData>`, `get<YourData>`, `delete<YourData>` methods into the [CourierClient](../generate-data/src/CourierClient.ts) class, to create/get/delete a data by an API
3. Add a `create<YourData>BySchema` into the [SchemaGenerator](../generate-data/src/SchemaGenerator.ts) class. And call this method into the `generateDataBySchema()` method in the same class, this method will called during a data creation
4. Add a deleting logic of a gererated data into `deleteCompanyWithDeps()` method of the [CourierClient](../generate-data/src/CourierClient.ts) class. This method will be called during a data deletion
5. Before a testing: call the `npm run e2e:generate-data` to a generate data
6. After a testing: call the `npm run e2e:remove-data` to delete generated data

**Note**: if you have a changes into the `generate-data` package, build this package again by calling the `npm run build` command to apply your changes

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
