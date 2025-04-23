# Changelog

## 3.4.1
* Fixed alerts formatting (remove double escaping for arrays) [MAPSINFRA-3827](https://st.yandex-team.ru/MAPSINFRA-3827).

## 3.4.0
* Updated upstream template for stands.

## 3.3.0
* Added command `get-config` [MAPSINFRA-3536](https://st.yandex-team.ru/MAPSINFRA-3536).

## 3.2.0
* Support any deploy units [MAPSUI-21679](https://st.yandex-team.ru/MAPSUI-21679).

## 3.1.2
* Minor improvements in `alerts push` command log output [MAPSINFRA-2939](https://st.yandex-team.ru/MAPSINFRA-2939).

## 3.1.1
* Minor fixes in `alerts` creation [MAPSINFRA-2939](https://st.yandex-team.ru/MAPSINFRA-2939).

## 3.1.0
* Minor improvements in `alerts` command: [MAPSINFRA-2939](https://st.yandex-team.ru/MAPSINFRA-2939#619bb293834ce9073af49a37).

## 3.0.1
* Updated dependencies: `maps._yasm` and `maps._monitoring-utils`.

## 3.0.0
* Remove `qloud` mentions from the codebase: [MAPSINFRA-3505](https://st.yandex-team.ru/MAPSINFRA-3505).

## 2.0.0
* Added support for dynamic config storage in `qtools.js`: [MAPSINFRA-3533](https://st.yandex-team.ru/MAPSINFRA-3533).

## 1.5.1
* Bugfixes and minor code improvements for awacs alerts configuration: [MAPSINFRA-2939](https://st.yandex-team.ru/MAPSINFRA-2939).

## 1.4.0
* Added support for awacs alerts configuration: [MAPSINFRA-2939](https://st.yandex-team.ru/MAPSINFRA-2939).

## 1.3.0

* Added `--draft` flag for `qtools deploy`: [GEOADVTECHDEBT-139](https://st.yandex-team.ru/GEOADVTECHDEBT-139).

## 1.2.14

* Fixed generation for custom stand config: [MAPSINFRA-3243](https://st.yandex-team.ru/MAPSINFRA-3243).

## 1.2.7

* Fixed updating stand backends (`"meta.version" must be set`).

## 1.2.6

* Fixed command `stand` if upstream backends have changes for DC.
* Add IO limits for HDD.

## 1.2.4

* Fixed `ya tool` + `child_process` integration. `ya tool dctl put stage` was failing because of empty list of env variables (#493).

## 1.2.3

* Added retries to run `dctl put stage` because of conflicts: [MAPSINFRA-2977](https://st.yandex-team.ru/MAPSINFRA-2977).

## 1.2.2

* Added new required spec field `/meta/account_id`: [RTCSUPPORT-8609](https://st.yandex-team.ru/RTCSUPPORT-8609).

## 1.2.1

* Fixed deploying of multi deploy units stage if one of them had no changes: [MAPSINFRA-2929](https://st.yandex-team.ru/MAPSINFRA-2929).

## 1.2.0

* Used `DCTL_YP_TOKEN` as `QTOOLS_TOKEN` value: [MAPSINFRA-2757](https://st.yandex-team.ru/MAPSINFRA-2757).

  Now you can remove `env.DCTL_YP_TOKEN` from CI.

## 1.1.7

* Fixed replacement of `{{TLD}}`.

## 1.1.6

* Fixed scheme for `depoy.stand.balancer.host`.

## 1.1.5

* Fixed duty schedule creation if user has no permission for this action: [MAPSINFRA-2736](https://st.yandex-team.ru/MAPSINFRA-2736).

## 1.1.4

* Added duty schedule creation with pushing alerts: [MAPSINFRA-2205](https://st.yandex-team.ru/MAPSINFRA-2205).

## 1.1.3

* Allowed use other options for trending alerts: [MAPSUI-16786](https://st.yandex-team.ru/MAPSUI-16786).

## 1.1.2

* Removed `meta.acl` from stands: [MAPSINFRA-2642](https://st.yandex-team.ru/MAPSINFRA-2642).

## 1.1.1

* Fixed finding of delegation token for non-`app` deploy units.

## 1.1.0

* Changed juggler checks for Deploy: [MAPSINFRA-2487](https://st.yandex-team.ru/MAPSINFRA-2487).

## 1.0.12

* Fixed `qtools build --qloud` for stands: [MAPSINFRA-2482](https://st.yandex-team.ru/MAPSINFRA-2482).

## 1.0.11

* Fixed `qtools stand --qloud`: [MAPSINFRA-2482](https://st.yandex-team.ru/MAPSINFRA-2482).

## 1.0.10

* Decreased `max_pessimized_endpoints_share` for stands: [BALANCERSUPPORT-560](https://st.yandex-team.ru/BALANCERSUPPORT-560).

## 1.0.9

* Updated `max_pessimized_endpoints_share` for stands: [BALANCERSUPPORT-560](https://st.yandex-team.ru/BALANCERSUPPORT-560).

## 1.0.8

* Fixed error `self signed certificate in certificate chain`: [MAPSINFRA-2384](https://st.yandex-team.ru/MAPSINFRA-2384).
* Changed YP_ENDPOINT_SETS to YP_ENDPOINT_SETS_SD: [MAPSINFRA-2422](https://st.yandex-team.ru/MAPSINFRA-2422).

## 1.0.6

* Removed deploy unit revision from configurations to make diff clear: [MAPSINFRA-2331](https://st.yandex-team.ru/MAPSINFRA-2331).

## 1.0.5

* Fixed project creating.

## 1.0.4

* Fixed deploy stage without secrets.

## 1.0.2

* Fixed alerts logins, list should be uniq.

## 1.0.1

* Removed ACL from local and remote configurations to make diff clear.
* Fixed initial registry config with `repository`.

## 1.0.0

### Breaking changes

* Replaced global option `--yd` with `--qloud` (`-q`) for support Qloud. **By default all commands work for Yandex Deploy.**

## 0.18.15

* Fixed `--abc` option for `init` command. Now you can specify ABC slug instead of ID.

## 0.18.14

* Simplify working with projects.

## 0.18.13

### Breaking changes

* Rewrited `stand` command for YDeploy. Check our [documentation](./docs/stand.md).

## 0.18.12

* Added support for YDeploy in `alerts` command: `qtools alerts <action> --yd`.

## 0.18.10

* For Deploy `registry.repository` is required.

## 0.18.8

* Support new model Project for YDeploy: [MAPSINFRA-2268](https://st.yandex-team.ru/MAPSINFRA-2268)

## 0.18.3

* Changed old podrick-int host ([MAPSINFRA-2202](https://st.yandex-team.ru/MAPSINFRA-2202))

## 0.18.1

* Added support for YDeploy in `tags` command: `qtools tags --used --yd`.

## 0.18.0

* Added support for YDeploy in `init` command: `qtools init --yd --abc <NNN>`.
* Added support for YDeploy in `hosts` command: `qtools hosts --yd`.
* Added support for YDeploy in `undeploy` command: `qtools undeploy <env> --yd`.
* Added support for YDeploy in `fire` command: `qtools fire --yd ...`.

### Breaking changes

* Added required field in `.qtools.json` — `abcServiceName`. Use ABC slug for this field:
  - Using in `fire` as `uploader.component`.
  - Using in `upload-static` as `project` in path. Check our [documentation](./docs/geo-specific.md#upload-static).
  - Example: `abcServiceName=maps-front-infra` for "[Geo Frontend Inftrastructure](https://abc.yandex-team.ru/services/maps-front-infra)".

## 0.17.2

* [backport] Changed old podrick-int host ([MAPSINFRA-2202](https://st.yandex-team.ru/MAPSINFRA-2202))

## 0.17.0

* Added support for YDeploy in `deploy` command: `qtools deploy <env> --yd`.

### Breaking changes

* Added optional new field in `.qtools.json` — `deploy`.

## 0.16.7

* Added `--bucket=<bucket_name>` option to `upload-static` command.

## 0.13.0

* Changed logic for polling statuses from Qloud API ([a759470](https://github.yandex-team.ru/maps/infra/commit/a759470abe22151eeacf3325ab396cedce47e6d6)).

## 0.9.15

### Bug fixes

* Fix validation of `.geoSpecific.monitorings.components[].groups."access-tskv".total.graph.Options.Filters`
  field in `.qtools.json` ([#243](https://github.yandex-team.ru/maps/infra/pull/243/)).

## 0.9.8

### Bug fixes

* Fixed blocking of file descriptor when passing stdin config

## 0.9.7

### Bug fixes

* Added support to remove juggler checks via `qtools alerts remove` ([#216](https://github.yandex-team.ru/maps/infra/pull/216))

## 0.9.6

### Bug fixes

* Moved stands from `common` to `common-ci` hardware segment ([#219](https://github.yandex-team.ru/maps/infra/pull/219))

## 0.9.1

### New features

* Added option `--comment` for `deploy` command ([#198](https://github.yandex-team.ru/maps/infra/pull/198)).

## 0.9.0

### Breaking changes

* Dropped support for Node.js 6, now requires Node.js 8 ([#197](https://github.yandex-team.ru/maps/infra/pull/197)).

## 0.8.5

* Increased registry timeout up to 5s ([56fdbc9](https://github.yandex-team.ru/maps/infra/commit/56fdbc9ed90ec904da731d6e4912adebcd281f44)).

## 0.8.3

### Bug fixes

* Fix `qtools alerts push` command ([#186](https://github.yandex-team.ru/maps/infra/pull/186)).

## 0.8.2

### Bug fixes

* Fix monitorings schema validation ([#179](https://github.yandex-team.ru/maps/infra/pull/179)).

## 0.8.1

### Bug fixes

* Fixed schemas resolving ([MAPSINFRA-1224](https://st.yandex-team.ru/MAPSINFRA-1224))

## 0.8.0

* Moved to `maps/infra` repository ([MAPSINFRA-1211](https://st.yandex-team.ru/MAPSINFRA-1211)).

## 0.7.4

### Bug fixes

* Update `js-yaml` and `yargs` dependencies to fix vulnerabilities ([#277](https://github.yandex-team.ru/maps/qtools/pull/277)).

## 0.7.2

### geoSpecific.monitorings validation fix

* geoSpecific.monitorings validation fix ([reason](https://st.yandex-team.ru/MAPSINFRA-1180))

## 0.7.1

### geoSpecific.monitorings validation

* Added geoSpecific.monitorings validation ([reason](https://st.yandex-team.ru/MAPSINFRA-1180))

## 0.7.0

### Add Golovan alerts tools

* Added commands for push/remove Golovan alerts ([reason](https://st.yandex-team.ru/MAPSINFRA-1023))

# Changelog

## 0.6.1

### Bug fixes

* Added queue with `concurrency: 1` for Qloud provider ([reason](https://st.yandex-team.ru/QLOUDSUPPORT-3265), [#270](https://github.yandex-team.ru/maps/qtools/pull/270))

## 0.6.0

### New features

* Added option `--target-state` for `deploy` command ([#273](https://github.yandex-team.ru/maps/qtools/pull/273))

## 0.5.8

### Bug fixes

* Fixed `-vv` option ([#267](https://github.yandex-team.ru/maps/qtools/issues/267))

## 0.5.7

### Bug fixes

* Fixed hangup `deploy`, `undeploy` commands with `--wait` flag ([#262](https://github.yandex-team.ru/maps/qtools/issues/262)).

## 0.5.6

### Bug fixes

* Fixed stands in accordance with drills ([MAPSUI-8219](https://st.yandex-team.ru/MAPSUI-8219))

## 0.5.5

### Bug fixes

* Fixed `undeploy` command ([#261](https://github.yandex-team.ru/maps/qtools/issues/261))

## 0.5.4

### Bug fixes

* Fixed support for internal domain in `stand` command

## 0.5.3

### Bug fixes

* Fixed handle empty delta of comparison local and remote configurations ([#260](https://github.yandex-team.ru/maps/qtools/pull/260)).

## 0.5.2

### Bug fixes

* Fixed comparison local and remote configurations ([#214](https://github.yandex-team.ru/maps/qtools/pull/214)).

## 0.5.1

### Bug fixes

* Fixed default instance size for stands

## 0.5.0

### New features

* Added new command `stand <branch> <tag>` ([#258](https://github.yandex-team.ru/maps/qtools/pull/258)).

## 0.4.0

### New features

* Improved error message for missing locations in `qtools deploy` command ([#254](https://github.yandex-team.ru/maps/qtools/pull/254)).

## 0.3.0

### Breaking changes

* Added final newline to `.qtools.json` on save ([#253](https://github.yandex-team.ru/maps/qtools/pull/253)).

## 0.2.2

### Bug fixes

* Fixed `uris` schema in accordance with [Yandex.Tank API](https://yandextank.readthedocs.io/en/latest/config_reference.html#uris-list-of-string) ([#251](https://github.yandex-team.ru/maps/qtools/pull/251))

## 0.2.1

### Bug fixes

* Fixed a crash when finishing load tests ([c492cd9](https://github.yandex-team.ru/maps/qtools/issues/c492cd983a265e7cf28017dc63b4644f343e1dc4))

## 0.2.0

### Breaking changes

* Changed shooting configuration format in accordance with [Yandex.Tank API](https://yandextank.readthedocs.io/en/latest/tutorial.html) ([#238](https://github.yandex-team.ru/maps/qtools/pull/238))

### New features

* Now you can use monitorings for shooting without RSA keys and `shooting.monitoring.config` section in `.qtools.json`. Read ([docs](./README.md#monitoring)).

## 0.1.1

### New features

* Added global option `--stdin` (`-S`) for stdin config instead of `.qtools.json` ([#245](https://github.yandex-team.ru/maps/qtools/issues/245))

### Bug fixes

* Fixed stdin on Linux ([#245](https://github.yandex-team.ru/maps/qtools/issues/245))
* Fixed error in registry provider ([#247](https://github.yandex-team.ru/maps/qtools/issues/247))

## 0.1.0

### Breaking changes

* The configuration file is now in JSON format ([#204](https://github.yandex-team.ru/maps/qtools/pull/204)). To convert your old configuration file:
  ```sh
  node -p "JSON.stringify(require('js-yaml').safeLoad(fs.readFileSync('./.qtools.yaml',{encoding:'utf-8'})),0,4)" > .qtools.json
  ```

### New features

* Added support for `stdin` config in JSON format ([#204](https://github.yandex-team.ru/maps/qtools/pull/204))
* Improved validation for `domains` ([#237](https://github.yandex-team.ru/maps/qtools/issues/237))
* Added options `-f` for `undeploy` command ([9f6b8b1](https://github.yandex-team.ru/maps/qtools/commit/9f6b8b12980cb1dabcb70ab0d62a8c85437ba2fb))

### Bug fixes

* Fixed typos ([2d7999a](https://github.yandex-team.ru/maps/qtools/commit/2d7999a5b83247e06de9e1b2d497dc1232fc157d), [7fefaa6](https://github.yandex-team.ru/maps/qtools/commit/7fefaa6c7051ad96da02e97d7e89fa4f1b327899))

## 0.0.41

### Bug fixes

* Added error retries for pulling status from environment ([#236](https://github.yandex-team.ru/maps/qtools/pull/236))

## 0.0.40

### Bug fixes

* Used `applicationName` instead of `projectName` for upload static ([9a5f973](https://github.yandex-team.ru/maps/qtools/commit/9a5f973ba31a7f783053fd327c7feafe7796baaa))

## 0.0.39

### Bug fixes

* Removed upload-static from release command
* Added retries for uploading static files

## 0.0.38

### New features

* Add ability to deploy static files to cdn (just for geo)  ([#231](https://github.yandex-team.ru/maps/qtools/pull/231))

### Bug fixes

* In prepareRecipe or activateRecipe `recipe` is required ([#230](https://github.yandex-team.ru/maps/qtools/issues/230))

## 0.0.37

### New features

* Now `qtools` throw error if domains changes cannot be apply ([#224](https://github.yandex-team.ru/maps/qtools/pull/224))
* Turned off colorize of logger in not TTY environment (ex. CI) ([#225](https://github.yandex-team.ru/maps/qtools/pull/225))

## 0.0.36

### New features

* Changed validation library to [ajv](https://github.com/epoberezkin/ajv) ([44c1264](https://github.yandex-team.ru/maps/qtools/commit/44c1264af51ae3ffaaa13542f6c39db35319b87a))
* Improved validation for `components[].tvmConfig` ([#219](https://github.yandex-team.ru/maps/qtools/pull/219))
* Added retries for all requests to the Qloud API ([#218](https://github.yandex-team.ru/maps/qtools/pull/218))
* Added trendbox triggers for CI ([#217](https://github.yandex-team.ru/maps/qtools/pull/217))

## 0.0.34

### Bug fixes

* Fixed `fire` command ([#213](https://github.yandex-team.ru/maps/qtools/issues/213))

## 0.0.33

### Bug fixes

* Fixed removing domains
* Allowed `undefined` for `domains` field

## 0.0.32

### Bug fixes

* Fixed error `localCompare is not a function` ([#208](https://github.yandex-team.ru/maps/qtools/issues/208))

## 0.0.31

### New features

* Added validation for `components[].l3Config` ([#205](https://github.yandex-team.ru/maps/qtools/issues/205))

### Bug fixes

* Fixed unhandled promise rejection in some cases ([#207](https://github.yandex-team.ru/maps/qtools/issues/207))
* Fixed `pull-config` error: `Cannot read property 'domains' of undefined` ([#206](https://github.yandex-team.ru/maps/qtools/issues/206))

## 0.0.29

### New features

* Added command `pull-config [environment]` ([#182](https://github.yandex-team.ru/maps/qtools/pull/182))
* Added command `validate` ([#198](https://github.yandex-team.ru/maps/qtools/pull/198))
* Added full validation for `components[].*` ([#168](https://github.yandex-team.ru/maps/qtools/issues/168), [#200](https://github.yandex-team.ru/maps/qtools/issues/200), [fad065a](https://github.yandex-team.ru/maps/qtools/commit/fad065a77d8170c5a9be2260abf5e6bc2dfcf72b))
* Added support for [policies](https://wiki.yandex-team.ru/qloud/doc/environment/#policies) ([#194](https://github.yandex-team.ru/maps/qtools/pull/194))
* Added validation for availability of `instanceGroups[].location` in accordance with `properties.hardwareSegment` ([#199](https://github.yandex-team.ru/maps/qtools/pull/199))
* Added `debug` mode and improved `verbose` mode ([#196](https://github.yandex-team.ru/maps/qtools/pull/196))

### Breaking changes

* Now for deploy use API `/api/v1/environment/upload/return-header` instead of `/api/v1/environment/upload` ([#188](https://github.yandex-team.ru/maps/qtools/pull/188))
* Changed output for diffs ([#197](https://github.yandex-team.ru/maps/qtools/pull/197))
* Changed `init` command in accordance with `pull-config` ([#201](https://github.yandex-team.ru/maps/qtools/pull/201))

### Bug fixes

* Fixed losing fields from environment after deploy ([#160](https://github.yandex-team.ru/maps/qtools/issues/160))

## 0.0.28

### New features

* Increased timeouts to `registry.yandex.net` ([#190](https://github.yandex-team.ru/maps/qtools/pull/190))
* Added support to use staging workflow ([#151](https://github.yandex-team.ru/maps/qtools/pull/151))

## 0.0.27

### Bug fixes

* Added Qloud API error message to log ([#186](https://github.yandex-team.ru/maps/qtools/pull/186))
* Increased timeouts to `registry.yandex.net` ([#181](https://github.yandex-team.ru/maps/qtools/pull/181))
* shooting: Use property `td` for detect termination ([#178](https://github.yandex-team.ru/maps/qtools/pull/178))

### Breaking changes

* shooting: Removed default monitoring configuration ([#179](https://github.yandex-team.ru/maps/qtools/pull/179))
* Added full validation for `components[].routeSettings` ([#180](https://github.yandex-team.ru/maps/qtools/pull/180))

### New features

* Improve progress bar message for `fire` command ([#176](https://github.yandex-team.ru/maps/qtools/pull/176))

## 0.0.26

### Breaking changes

* Got rid of `components[].extends` ([#111](https://github.yandex-team.ru/maps/qtools/issues/111))

### Bug fixes

* Allowed any order of components in stress environment ([#172](https://github.yandex-team.ru/maps/qtools/pull/172))
* Removed redundant files from npm package ([#167](https://github.yandex-team.ru/maps/qtools/issues/167))

## 0.0.25

### Breaking changes

* Now the package is available by the name of `@yandex-int/qtools`. The package `ymaps-qloud-tools` will no longer be published. ([#158](https://github.yandex-team.ru/maps/qtools/issues/158))

### Bug fixes

* Increased timeout for `deploy` command with `--wait` option ([#156](https://github.yandex-team.ru/maps/ymaps-qloud-tools/issues/156))

## 0.0.24

### Breaking changes

* Now all changes with domains are applied to remote environment ([#149](https://github.yandex-team.ru/maps/ymaps-qloud-tools/pull/149))
* Option `--remove-stress-environment` of the `fire` command was removed in favor to `undeploy` command ([#147](https://github.yandex-team.ru/maps/ymaps-qloud-tools/pull/147))

### New features

* Added command `undeploy <environment>` ([#147](https://github.yandex-team.ru/maps/ymaps-qloud-tools/pull/147))
* Added options `--wait` (`-w`) for `deploy` and `release` commands ([#148](https://github.yandex-team.ru/maps/ymaps-qloud-tools/pull/148))
* Added validation for components with `componentType=component-proxy` ([#153](https://github.yandex-team.ru/maps/ymaps-qloud-tools/issues/153))
* Added validation for `components[].sandboxResources` ([#154](https://github.yandex-team.ru/maps/ymaps-qloud-tools/issues/154))

## 0.0.23

### Bug fixes

* Got rid of `docker pull` in `push` command ([#130](https://github.yandex-team.ru/maps/ymaps-qloud-tools/pull/130))

### New features

* Added command `tags [image_name]` ([#146](https://github.yandex-team.ru/maps/ymaps-qloud-tools/pull/146))
* Added validation for `components[].secrets` ([#137](https://github.yandex-team.ru/maps/ymaps-qloud-tools/pull/137))

## 0.0.22

### Bug fixes

* Fixed a bug in qtools build, where the extractra arguments were not passed properly to docker build ([#138](https://github.yandex-team.ru/maps/ymaps-qloud-tools/pull/138)).

## 0.0.21

### Bug fixes

* Now property `hardwareSegment` for components with `allocationStrategy='collocation'` is forbidden ([#131](https://github.yandex-team.ru/maps/ymaps-qloud-tools/pull/131))
* Now properties `hardwareSegment` and `network` are not required ([#131](https://github.yandex-team.ru/maps/ymaps-qloud-tools/pull/131))

### New features

* Added response message of deploy and lunapark errors in verbose mode ([#132](https://github.yandex-team.ru/maps/ymaps-qloud-tools/pull/132))
* Added information about tank image. See [`fire` docs](./README.md#notes) for more details ([#133](https://github.yandex-team.ru/maps/ymaps-qloud-tools/pull/133))
* Added end-to-end tests for `build` command ([#60](https://github.yandex-team.ru/maps/ymaps-qloud-tools/pull/60))

## 0.0.20

### Bug fixes

* Fixed `fire` command ([#126](https://github.yandex-team.ru/maps/ymaps-qloud-tools/pull/126))
* Fixed `tag` command ([#126](https://github.yandex-team.ru/maps/ymaps-qloud-tools/pull/126))

## 0.0.19

### Breaking changes

* Option `-i`, (`--inline-config`) of `fire` command was renamed to `-o` (`--option`). ([#121](https://github.yandex-team.ru/maps/ymaps-qloud-tools/pull/121))
* Now field `token` is forbidden for using. You should use environment variable `QTOOLS_TOKEN`. ([#122](https://github.yandex-team.ru/maps/ymaps-qloud-tools/pull/122))

### New features

* Now you can pass [`docker build` options](https://docs.docker.com/engine/reference/commandline/build/#options) to `qtools build` or `qtools release` commands. Just separate them from the `build`/`release` parameters with a double dash (`--`). See [`build` section](./README.md#build) for more details. ([#121](https://github.yandex-team.ru/maps/ymaps-qloud-tools/pull/121))
* Added support to [proxy](https://docs.qloud.yandex-team.ru/doc/platform-component#proxy) and [component-proxy](https://docs.qloud.yandex-team.ru/doc/platform-component#component-proxy) types of component. ([#118](https://github.yandex-team.ru/maps/ymaps-qloud-tools/pull/118))

### Bug fixes

* Now hash for docker image get from [registry API](https://docs.docker.com/registry/spec/api/#manifest), not from `dockinfo.yandex-team.ru`. ([#120](https://github.yandex-team.ru/maps/ymaps-qloud-tools/pull/120))
* Changed package [commander](https://github.com/tj/commander.js) to [yargs](https://github.com/yargs/yargs) for parsing CLI arguments. ([#121](https://github.yandex-team.ru/maps/ymaps-qloud-tools/pull/121))
* Got rid of `qloud-api` package. ([#117](https://github.yandex-team.ru/maps/ymaps-qloud-tools/pull/117))
* Got rid of `yarn.lock`. ([#74](https://github.yandex-team.ru/maps/ymaps-qloud-tools/issues/74))

## 0.0.18

### Breaking changes

* Now engine `qloud` is forbidden for using, you should use `platform`. ([#109](https://github.yandex-team.ru/maps/ymaps-qloud-tools/issues/109))
* Migrated to Platform's shooting. ([#109](https://github.yandex-team.ru/maps/ymaps-qloud-tools/issues/109), [MAPSINFRA-197](https://st.yandex-team.ru/MAPSINFRA-197)). See [platform docs](https://docs.platform.yandex-team.ru/doc/shooting) for more details.

### New features

* Now `domains` and `routeSettings` are not required for environment configuration. ([#109](https://github.yandex-team.ru/maps/ymaps-qloud-tools/issues/109))
* Now `routeSettings` can be filled by `null` value. ([#109](https://github.yandex-team.ru/maps/ymaps-qloud-tools/issues/109))

## 0.0.17

### New features

* Migrated to new environment engine `platform` on initialization. ([#110](https://github.yandex-team.ru/maps/ymaps-qloud-tools/pull/110))

### Bug fixes

* Increased the timeout and number of retries for dockinfo. ([b9ac452](https://github.yandex-team.ru/maps/ymaps-qloud-tools/commit/b9ac45257a2b40c94300f167fa717f9bc163c2b0))

## 0.0.16

### Bug fixes

* Increased number of retries for qloud ([#107](https://github.yandex-team.ru/maps/ymaps-qloud-tools/pull/107))
* Initialized `testing` if there aren't any environments in application ([#93](https://github.yandex-team.ru/maps/ymaps-qloud-tools/issues/93))
* Made some internal changes ([#97](https://github.yandex-team.ru/maps/ymaps-qloud-tools/issues/97))

## 0.0.15

### New features

* Added validation for stress environment ([#95](https://github.yandex-team.ru/maps/ymaps-qloud-tools/pull/95))
* Added support to customize `Dockerfile` and context for build image ([#99](https://github.yandex-team.ru/maps/ymaps-qloud-tools/pull/99))
* Added support to customize stress environment ([#102](https://github.yandex-team.ru/maps/ymaps-qloud-tools/pull/102))

### Bug fixes

* Fixed logging of dockinfo's errors ([#96](https://github.yandex-team.ru/maps/ymaps-qloud-tools/pull/96))
* Fixed help message ([#103](https://github.yandex-team.ru/maps/ymaps-qloud-tools/issues/103))

## 0.0.14

### Breaking changes

* Renamed command `upload` to `push` ([#87](https://github.yandex-team.ru/maps/ymaps-qloud-tools/pull/87))

### New features

* Added tag example ([#77](https://github.yandex-team.ru/maps/ymaps-qloud-tools/pull/77))
* Added type of value in diffs ([#79](https://github.yandex-team.ru/maps/ymaps-qloud-tools/pull/79))
* Now deploing of `stress` environment is not require shooting config ([#84](https://github.yandex-team.ru/maps/ymaps-qloud-tools/pull/84))

### Bug fixes

* Now `ammofile` can be replaced with `uris` as required properties for shooting ([#85](https://github.yandex-team.ru/maps/ymaps-qloud-tools/pull/85))
* Print help output if command unrecognized ([#86](https://github.yandex-team.ru/maps/ymaps-qloud-tools/pull/86))
* Typo in error message of `build` command

## 0.0.13

### Bug fixes

* Now field `domains` can be filled by `null` value. ([#75](https://github.yandex-team.ru/maps/ymaps-qloud-tools/pull/75))
* Option `-o` (`--options`) of `fire` command was renamed to `-i`, (`--inline-config`). ([#76](https://github.yandex-team.ru/maps/ymaps-qloud-tools/pull/76))

## 0.0.12

* `qtools tag` now only outputs the new tag string without any additional text ([#73](https://github.yandex-team.ru/maps/ymaps-qloud-tools/pull/73))

## 0.0.11

### Breaking changes

* It's now the clients responsibility to provide an authorization token for API interactions, see the [Authorization](./README.md#authorization) section for more details.
* Not using clients `package.json` anymore:
  * Instead of `package.json#name` the application name is stored in `.qtools.yaml#qloud.applicationName`.
  * Instead of `package.json#version` the image version is stored in `.qtools.yaml#registry.tag`.
* Qloud environments are now under the `qloud.environments` field.
* For the `deploy` and `release` commands, the argument `environment` now is required.
* Changes in `qtools fire`:
  * Instead of the argument `[rps_schedule]` you should use the option `-o, --options`. For example, `-o "phantom.rps_schedule=line(1,100,1m)"`.
  * Instead of the option `-c, --component <name>` you should use the option `-o, --options`. For example, `-o "meta.component=MAPSHTTPAPI-182"`.

### New features

* Added command `validate <environment>` ([#59](https://github.yandex-team.ru/maps/ymaps-qloud-tools/issues/59))
* Added command `hosts [environment]` ([#66](https://github.yandex-team.ru/maps/ymaps-qloud-tools/issues/66))
* Added command `tag <release_type>` ([#67](https://github.yandex-team.ru/maps/ymaps-qloud-tools/pull/67))
* Added options `-o, --options` and `-c, --config` for `fire` command.
* Added options `-p, --project`, `-a, --application` and `-H, --host` for `init` command.

[All changes from v0.0.10 to v0.0.11](https://github.yandex-team.ru/maps/ymaps-qloud-tools/compare/v0.0.10...v0.0.11)

## 0.0.10

### Breaking changes

* Option `dockerProject` in `.qtools.yaml` was renamed to `registryProject` ([#38](https://github.yandex-team.ru/maps/ymaps-qloud-tools/pull/38)).

### New features

* Added option `qloudHost` to `.qtools.yaml` ([#41](https://github.yandex-team.ru/maps/ymaps-qloud-tools/pull/41)).

## 0.0.9

* The configuration file is now in YAML ([#33](https://github.yandex-team.ru/maps/ymaps-qloud-tools/pull/33)). To convert your old configuration file:
  ```
  cd your-project-root
  wget https://github.yandex-team.ru/raw/gist/dodev/918e52b2800ccd120305b3bca7b34b6e/raw/4329b2684fac74ff0d0361bc1915f33c857d898b/convert-js-to-yaml.js
  ```
  For a .js config run:
  ```
  node -p "JSON.stringify(require('./.qtools.js'))" | node convert-js-to-yaml.js > .qtools.yaml
  ```
  For a JSON config run:
  ```
  cat .qtools.json | node convert-js-to-yaml.js > .qtools.yaml
  ```

## 0.0.8

* Added `qtools init` option which initializes a ymaps-qloud-tools configuration file, if not present ([#30](https://github.yandex-team.ru/maps/ymaps-qloud-tools/pull/30)).
  Also downloads the configurations from all environments on qloud, if they weren't present in the configuration file.
* MAPSINFRA-91: `qtools release` ([#20](https://github.yandex-team.ru/maps/ymaps-qloud-tools/pull/20))
* Added support for domains in qloud config ([#23](https://github.yandex-team.ru/maps/ymaps-qloud-tools/issues/23))
* Added test project ([#26](https://github.yandex-team.ru/maps/ymaps-qloud-tools/pull/26))
* Used new lunapark API for `qtools fire` ([#32](https://github.yandex-team.ru/maps/ymaps-qloud-tools/pull/32))

## 0.0.7

* MAPSINFRA-77: Отказаться от cit в ymaps-qloud-tools ([#7](https://github.yandex-team.ru/maps/ymaps-qloud-tools/pull/7))
    * Don't use field `domains`, since this version you should add domains to your application manually.
    * Instead of `component` you should use `components` as array of objects.
        * Field `name` should be renamed to `componentName`.
        * Section `image` will be omitted. If you want use this field you should add url of docker image with tag (e.g. `registry.yandex.net/maps/project:latest-tag`) to field `properties.repository`.
        * Field `type` should be renamed to `componentType`.
        * Properties of component should be moved to field `properties`, e.g. `size`, `network`, `hardwareSegment`, `deployPolicy`, etc.
    * Section `routes` should be renamed to `routeSettings`.
        * Don't forget to add field `componentName` with value from `components[].componentName`.
    * Fields `esIndexTtl` and `esShipAccessLog` should be moved to `settings` section.
    * Section `envVars` should be renamed to `userEnvironmentMap`.
