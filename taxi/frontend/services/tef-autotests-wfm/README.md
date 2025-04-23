# WFM Autotests (UI + API)

## About project

| Entity         |                                                       Link                                                       |
|----------------|:----------------------------------------------------------------------------------------------------------------:|
| Docs           |              [Wiki WFM](https://wiki.yandex-team.ru/users/dborovikov/wfm-dlja-kontaktnogo-centra/)               |
| App envs links | [Ссылки на стенды](https://a.yandex-team.ru/arc_vcs/taxi/frontend/services/tef-wfm-frontend/README.md?rev=trunk) |

## Install deps

1. Install nvm, https://nodejs.org/ru/download/package-manager/#nvm
2. Setup nodejs v14 `nvm install v14`
3. Make arc mount
```shell
# If you don't have any dir /Users/$USER/arcprojects and /Users/$USER/arc -> create it with: mkdir -p /Users/$USER/arc и mkdir -p /Users/$USER/arcproject
arc mount --mount=/Users/$USER/arcprojects/tef-autotests-wfm --store=/Users/$USER/arc/tef-autotests-wfm --path-filter=taxi/frontend/services/tef-autotests-wfm
```
4. Install deps `npm install`.
5. Append credentials to `.env` file. You need to change WFM_USERNAME / PASSWORD values to real user (for example, bot or yours account with access to wfm)
```dotenv
WFM_USERNAME=username
WFM_PASSWORD=password
ENV=testing
```

## Getting Started

Run test with following command:
```bash
npm run test
```

Run linting:
```bash
npm run lint
```

Run autofixer problems (linting):
```bash
npm run fix
```

## Folder Structure

```
.
├── ...
├── allure-results                  # Generated reports
├── debian                          # For internal automatic, you do not need to touch this
├── docker                          # Dockerfiles for build testing app
├── .env                            # Environment of testing (usernames, app env etc)
├── test/
│     ├── config/
│           ├── **/*.ts             # JavaScript objects with urls by env, links and other constants, that depends on env
│     ├── dist/                     # App build (already in arcignore), you do not need to touch this
│     ├── fixtures/
│           ├── **/*.json           # JSON Mock data. You can import it by javascript "import"
│     ├── page-objects/
│           ├── index.ts            # Base import with every page object. Also you can import not core object, you can import just specify page-object from import
│           ├── page.ts             # Implementation of base page functionality (the same pattern used to WFM and LOGIN sub dirs. This is about common urls and actions
│           ├── **/*.page.ts.ts     # Custom page or element (for eexample, catalog Skills is decomposed for list.page and card.page. So you can implement atonmic classes for atomic UI.
│     ├── specs/
│           ├── ui                  # For UI-tests (frontend)
│           ├── api                 # For API tests (backend)
│     ├── utils/
│           ├── **/*.ts             # Custom helpers for writing autotests
│     ├── wdio/
│           ├── *.ts                # Atomic sub-config scripts for all config of wdio
```

## Learn More

To learn more about Selenium, take a look at the following resources:
- [WDIO Documentation](https://webdriver.io/docs/gettingstarted)
