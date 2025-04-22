# `qtools`

![version](https://badger.yandex-team.ru/npm/@yandex-int/qtools/version.svg)

Toolchain for working with [Yandex Deploy](https://deploy.yandex-team.ru), [Docker](https://www.docker.com/) and other cloud technologies.

<details><summary><b>Table of contents</b></summary>

- [`qtools`](#qtools)
  - [Prerequisites](#prerequisites)
  - [Installation](#installation)
  - [Configuration](#configuration)
    - [Authorization](#authorization)
    - [Yandex Deploy configuarion file](#yandex-deploy-configuarion-file)
  - [Basic Usage](#basic-usage)
    - [`build`](#build)
    - [`push`](#push)
    - [`deploy <environment>`](#deploy-environment)
      - [Manual](#manual)
      - [Staging](#staging)
    - [`release <environment>`](#release-environment)
    - [`init`](#init)
    - [`fire`](#fire)
      - [Notes](#notes)
      - [Monitoring](#monitoring)
      - [Override options](#override-options)
      - [Custom config](#custom-config)
      - [Regression tests](#regression-tests)
    - [`get-config <tag>`](#get-config-tag)
    - [`hosts [environment]`](#hosts-environment)
    - [`tag <release_type>`](#tag-release_type)
    - [`tags [image_name]`](#tags-image_name)
    - [`undeploy <environment>`](#undeploy-environment)
    - [`pull-config [environment]`](#pull-config-environment)
    - [`validate`](#validate)
    - [`image-exists`](#image-exists)
    - [`stand`](#stand)
  - [Advanced Usage](#advanced-usage)
    - [Debugging](#debugging)
    - [Microservices](#microservices)
  - [Troubleshooting](#troubleshooting)
    - [no basic auth credentials](#no-basic-auth-credentials)
    - [qtools deploy failed: Cannot resolve docker image](#qtools-deploy-failed-cannot-resolve-docker-image)
    - [self signed certificate in certificate chain](#self-signed-certificate-in-certificate-chain)
</details>

## Prerequisites

* `node` >= 8
* `ya` (should be executable, [how to get](https://wiki.yandex-team.ru/yatool/distrib/))

## Installation

```
npm install --registry http://npm.yandex-team.ru --save-dev @yandex-int/qtools
```

## Configuration

`qtools` uses `json` for storing its configuration. You should store the config in a file named `.qtools.json` in the current working directory.

To setup the config file run [`qtools init`](#init) or you can do it manually by creating a configuration file:

```json
{
    "abcServiceName": "<abcServiceName>",
    "registry": {
        "tag": "<tag>",
        "prefix": "<registryPrefix>",
        "repository": "<registryRepository>"
    }
}
```

Also you can find `qtools` [schemas](./configs/schema.yaml) in this repository.

Parameters:

* `abcServiceName` — ABC slug of your service.
* `tag` — tag for docker image.
* `registryPrefix` – docker registry's prefix where the image will be pushed (for example, `maps`). Optional field, by default it's empty.
* `registryRepository` – docker registry's image name where the image will be pushed (for example, `your-name`).

### Authorization

You should provide OAuth token via environment variable `QTOOLS_TOKEN`.

You can get token via next [application](https://oauth.yandex-team.ru/authorize?response_type=token&client_id=4dd38b9acbb44ad8a7ece163ddf1c53a), or you can create your own application:

1. Create new application: https://oauth.yandex-team.ru/client/new.
1. Add rules for Docker Registry, YP, AWACS, Vault, Juggler, ABC and Startrek.
1. Open link with new `client_id`: `https://oauth.yandex-team.ru/authorize?response_type=token&client_id=<client_id>`.
1. Copy and paste the token to your shell environment configuration.

**Note:** If you want to use a robot you should get OAuth token under the robot user. Your robot should have access to your Deploy project.

### Yandex Deploy configuarion file

`qtools` modified only `image_for_boxes` and secrets `delegation_token` fields in your stage configuration file. All other fields refers to [official docs](https://wiki.yandex-team.ru/deploy/docs/).

By default, `qtools` takes stage configs from `.configs/deploy/<env>.yml`. You can change it:

```json
{
    "deploy": {
        "environments": {
            "testing": {
                "configPath": "./path/to/your/stage.yml"
            }
        }
    }
}
```

## Basic Usage

### `build`

Builds a docker image.

```sh
node_modules/.bin/qtools build
```

Also you can pass [`docker build` options](https://docs.docker.com/engine/reference/commandline/build/#options) to this command. Just separate them from the `qtools build` parameters with a double dash (`--`). For example:

```sh
node_modules/.bin/qtools build -- --no-cache
```

### `push`

Pushes a prebuild image to the docker registry.

```sh
node_modules/.bin/qtools push
```

### `deploy <environment>`

Deploys a draft with `registry.tag` from config to the specified stage in Deploy. Uploading `.qtools.json` file to [sandbox](https://sandbox.yandex-team.ru/resources?type=QTOOLS_DATA) with ``QTOOLS_DATA`` type. 

```sh
# Testing environment
node_modules/.bin/qtools deploy testing

# Production environment
node_modules/.bin/qtools deploy production
```

**Options**:

* `--force` (`-f`) — deploy overriding possible remote configuration changes,
* `--wait` (`-w`) — wait before environment deploying wont stop.
* `--comment` — comment for deployment.
* `--draft` — deploy a [draft](https://deploy.yandex-team.ru/docs/reference/tools/dctl#drafts), useful for approval policy.

#### Staging

> Worked only for Qloud. For YDeploy this functionality will be supported in [MAPSINFRA-3515](https://st.yandex-team.ru/MAPSINFRA-3515).

You can configure staging environments with sorted array:

```json
{
    "deploy": {
        "staging": [
            "testing",
            "prestable",
            "production"
        ]
    }
}
```

For example, you want deploy `production`. But you will get error because name of images in components are not equal to remote images from `prestable` environment. So firstly you should deploy `prestable` environment with the same docker image.

### `release <environment>`

Builds, pushes and deploys an image to the specified stage. If the image does exist in the registry, this command only deploys it.

```sh
# Testing environment
node_modules/.bin/qtools release testing

# Production environment
node_modules/.bin/qtools release production
```

For passing [`docker build` options](https://docs.docker.com/engine/reference/commandline/build/#options) to this command read [`build` section](#build). For example:

```sh
node_modules/.bin/qtools release testing -- --no-cache
```

### `init`

Initializes `.qtools.json` configuration file, if not present.

```sh
node_modules/.bin/qtools init --abc <abc_id>
```

For details see `qtools init --help`.

### `fire`

Make sure that your have `shooting` section in qtools config in the project root.

```json
{
    "shooting": {
        "phantom": {
            "ammofile": "<urlToYourAmmofile>",
            "load_profile": "{@see https://yandextank.readthedocs.io/en/latest/tutorial.html}"
        },
        "uploader": {
            "task": "<startrekTicket>"
        }
    }
}
```

where `shooting` is the presentation of the [tank config](https://yandextank.readthedocs.io/en/latest/configuration.html#advanced-configuration).
You need to specify at least `phantom.ammofile`, `phantom.load_profile` and `uploader.task` to perform shooting.

Then you can start shooting:

```sh
node_modules/.bin/qtools fire
```

Use `-e` (`--environment`) option to change environment name (default: `stress`) for shooting ground. For example:

```sh
node_modules/.bin/qtools fire -e load-env
```

Stress environment will be set up automatically before first shooting. However, you need to manually to undeploy stress environment when you finish shooting.

To see all options execute

```sh
node_modules/.bin/qtools fire --help
```

#### Notes

For using the tank's image name in the config field `properties.repository` you should have access to the image in the registry. Just check out your role in [IDM](https://idm.yandex-team.ru/reports/roles#f-is-expanded=true,f-status=requested,f-system-type=all,f-role=docker/distribution/load%7Cyandex-tank-pip/viewer). Alternatively you can use the tank image's hash in `properties.hash`. This method doesn't require special access to the image.

Also use `tank` as separate deploy unit.

#### Monitoring

To enable target monitoring:

1. Make sure you're using the latest version of the `yandex-tank-pip` image for the `tank` component. At the time of writing it was `registry.yandex.net/load/yandex-tank-pip:1.10.1`.

2. Add a section named `yasm` to your `.qtools.json#shooting` config:
```json
{
    "shooting": {
        "yasm": {
            "enabled": true,
            "package": "yandextank.plugins.YASM",
            "panels": {
                "resources": {
                    "host": "ASEARCH",
                    "tags": "itype=deploy;stage=<stage-id>;deploy_unit=target"
                }
            }
        }
    }
}
```

`stage-id` is in the following format `<sbc-slug>_<environment>`, e.g. `maps-front-metro-data-api_stress`.

3. Delete and deploy your `stress` environment.

4. Start a shooting and wait for it to finish. The shooting may take a some extra time to finish, because `lunapark` needs time to download the data from `yasm`. After the shooting is finished, you will see a tab named `Monitorings`.

For more information and graph customization please check out [wiki page](https://wiki.yandex-team.ru/nagruzochnoetestirovanie/sbor-metrik-iz-yasm/) and [the post on Etushka](https://clubs.at.yandex-team.ru/tanks/1033).

#### Override options

Also you can override or add shooting configuration via the option `-o` (or `--option`):

```sh
node_modules/.bin/qtools fire -o "uploader.component=MAPSHTTPAPI-182" -o "phantom.load_profile.schedule=line(1,5,10s)"
```

You can pass [qs-formated](https://github.com/ljharb/qs#parsing-objects) values to `-o`.

#### Custom config

Your can specify custom file for shooting configuration. This file should be the presentation of the [tank config](https://yandextank.readthedocs.io/en/latest/configuration.html#advanced-configuration). Use `-с` or `--config` option for this:

```sh
node_modules/.bin/qtools fire -с ./path/for/config.json
```

Supporting formats: `json` or `yaml`.

#### Regression tests

When you perform your first shooting, you will see it at [MAPSLOADTESTING](https://lunapark.yandex-team.ru/regress/MAPSLOADTESTING) root.

You need to group your service components with service name and specify SLA for your service as well.

1. Click to edit icon.
2. Add name from your `abcServiceName` to `Сервисы:`.
3. Add `RPS разладки` KPI for max rps shooting ([see example](https://lunapark.yandex-team.ru/regress/MAPSLOADTESTING/2857/edit)); `Кумулятивные квантили` and `HTTP код (количество ответов)` ([see example](https://lunapark.yandex-team.ru/regress/MAPSLOADTESTING/2858/edit)).
4. Add regression using [Regression Tests template](https://teamcity.yandex-team.ru/admin/editBuild.html?id=template:maps_RegressionLoadTests) in Teamcity.

### `get-config <tag>`

Gets .qtools.json from sandbox

```sh
#Get production config
node_modules/.bin/qtools get-config production

#Get config with a scpecific tag (example: 1.2.3)
node_modules/.bin/qtools get-config 1.2.3
```

### `hosts [environment]`

Gets information about hosts of instances for specified environment or for all at once.

```sh
# All environments
node_modules/.bin/qtools hosts

# Production environment
node_modules/.bin/qtools hosts production
```

### `tag <release_type>`

Ups `registry.tag` in qtools config via release type.

```sh
node_modules/.bin/qtools tag patch
```

You can use the output of this subcommand to generate commit and tag names for your favourite VCS:

```sh
VERSION="v$($(npm bin)/qtools tag $release_type)" &&
    git add .qtools.yaml &&
    git commit -m $VERSION &&
    git tag $VERSION
```

### `tags [image_name]`

Returns tags for `image_name` or for image from qtools config. `image_name` should have next format: `prefix/repository`.

```sh
node_modules/.bin/qtools tags

node_modules/.bin/qtools tags junk/some-project
```

Also you can get all used image names in `standard` components from your application by `--used` (`-u`) option:

```sh
node_modules/.bin/qtools tags --used
```

### `undeploy <environment>`

Undeploy `environment` from an application. This subcommand always requires the `--force` (`-f`) flag, as a way of confirming your action.

```sh
node_modules/.bin/qtools undeploy dev-stand --force
```

Also you can protect environments in your project by `deploy.protectedEnvironmentNames` field from qtools config:

```json
{
    "deploy": {
        "protectedEnvironmentNames": [
            "production",
            "testing"
        ]
    }
}
```

**Options**:

* `--wait` (`-w`) — wait before environment deploying wont stop.

### `validate`

Validate the local configuration.

```sh
node_modules/.bin/qtools validate
```

### `image-exists`

Check if image already exists in registry, based on configuration.

```sh
node_modules/.bin/qtools image-exists
```

### `stand`

Check separate [documentation](./docs/stand.md) about `qtools stand`.

## Advanced Usage

Add `scripts` section into `package.json`:

```json
"scripts": {
    "build": "qtools build",
    "push": "qtools push",
    "deploy": "qtools deploy testing",
    "deploy:stress": "qtools deploy stress",
    "deploy:production": "qtools deploy production"
}
```

Then call `qtools` without any `node_modules/.bin/`:

```sh
npm run build
npm run push
npm run deploy
npm run deploy:production
```

### Debugging

All commands support `verbose` and `debug` mode, just add `-v` or `-vv`. It helps to investigate problems, so add output to your bug report.

### Microservices

You can create a lot of microservices in your project. For that you should create own `Dockerfile` and `.qtools.yaml` in the desired directory. If you want to copy folders from the above level, you should set context in registry section of `.qtools.json`:

```json
{
    "registry": {
        "context": "../"
    }
}
```

To start commands from global `Makefile` you can use command like that:

```sh
cd microservice && ../node_modules/.bin/qtools build
```

## Troubleshooting

### no basic auth credentials

When pushing an image, you may get messages such as these:

```
The push refers to a repository [registry.yandex.net/maps/seourl-int]
d02070031597: Preparing
...
918b1e79e358: Waiting
no basic auth credentials
```

Most likely you're not logged in the internal docker registry. To solve this, please read [registry's documentation on authorization](https://wiki.yandex-team.ru/cocaine/docker-registry-distribution/#avtorizacija).

### self signed certificate in certificate chain

You can see next error when use `qtools upload-static`:

```
error: Upload static error: 'RequestError: self signed certificate in certificate chain'
```

You should add internal certificate to your machine: https://wiki.yandex-team.ru/security/ssl/sslclientfix/#vnode.js
