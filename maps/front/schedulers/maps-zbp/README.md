# maps-zbp
Calculates and set severity and ZBP weight for tracker issues.

## General information
| Key | Value |
|---|---|
| Reactor | https://reactor.yandex-team.ru/browse/resolve?path=/maps/front/maps/infra/maps-zbp |

## What happens when scheduler is down
Severity and ZBP weights are stopped to updating. QA dashboards will show wrong information. It also can affect some internal process like management issues and sprint planning.

## Quick start
```
$ npm i
$ npm start // run all projects
$ PROJECTS=web-maps,maps-front-jsapi npm start // run specific projects
$ NO_DRY_RUN=1 npm start // run in production mode
```

## Run tests
```
$ npm test
```

## Add new project
First of all, add a new config for your project. See more details about format in [src/config.ts](src/config.ts).
```
$ arc checkout -b maps-zbp.ISSUE-KEY
$ touch configs/my-new-project.json
```
Then specify weights for all components and fields in config file. See other examples in [configs](configs) directory.

Debug your new project.
```
$ PROJECTS=my-new-project npm start
```

Create a pull request with your changes.
```
$ arc add .
$ arc commit -m "Use issue title as commit message"
$ arc pr create --push
```

When review is finished, update scheduler and add changes to your pull request.
```
$ npm version minor
$ arc push
```

Merge your pull request and wait some time when new version is applied.

See also:
* https://st.yandex-team.ru/MAPSINFRA-1712
