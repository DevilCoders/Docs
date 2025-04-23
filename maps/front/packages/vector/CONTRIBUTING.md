# Guidelines

Here's description of different conventions used in this project.

## Starting a working copy

After checkout in directory with the project run `make all tools dev`. After that
runner will serve the vector engine on `http://localhost:8080/out/vector.js` and basic API 3.0 with raster engine on `http://localhost:8080/out/ymaps3.js`. You can use
your own copy with JS API by [redefining](https://github.yandex-team.ru/maps/hosts#Переопределения-конфигов)
`vectorIndex` host. For example, it may look [like this](https://github.yandex-team.ru/mapsapi/jsapi-v2/blob/4de2afb5a49a0b2df72675b74840650feb3cf504/src/vectorEngine/vector.case.html#L18).

## Handy running TS code in browser

After `npm install` run `make all`, then run `make tools` to rebuild dev server and `make dev` to fire
it up. More about the runner in it's own [readme](./tools/runner/readme.md).

A new stand can be create very easily. Just create a HTML file (preferably, in
`tools/stand` directory), create a TS file with stand-related code (preferably,
not very far for the HTML file), include it as a `script` tag into the HTML file,
but with `.js` suffix instead of `.ts`, e.g.
[our main stand HTML](./tools/stand/index.html) and [TS](./tools/stand/index.ts).

## Style guide

The style guide used is based on [ymaps](https://github.com/ymaps/codestyle)
style guide with following additions:

  * constructor should always be in the begining of a class regardless of its
    access modifier:

    **Good:**

    ```ts
    class Foo {
        protected constructor() {}

        public foo(): void {}

        protected bar(): void {}

        private baz(): void {}
    }
    ```

    **Bad:**

    ```ts
    class Foo {
        public foo(): void {}

        protected constructor() {}

        protected bar(): void {}

        private baz(): void {}
    }
    ```

  * if a class has `destroy` method, its implementation should immediately follow
    class' constructor:

    **Good:**

    ```ts
    class Foo {
        constructor() {}

        public destroy(): void {}

        public foo(): void {}
    }
    ```

    **Bad:**

    ```ts
    class Foo {
        constructor() {}

        public foo(): void {}

        public destroy(): void {}
    }
    ```

  * properties and methods in classes should be arranged in the following order
    in respect of access modifiers:
    * `public`;
    * `protected`;
    * `private`;

    **Good:**

    ```ts
    class Foo {
        public numericProp: number;

        protected _methodToOverloadInASubclass(): void {}

        private _internalState: {}
    }
    ```

    **Bad:**

    ```ts
    class Foo {
        protected _methodToOverloadInASubclass(): void {}

        public numericProp: number;

        private _internalState: {}
    }
    ```

  * non-static properties and methods should always precede static ones with the
    same access modifier;

    **Good:**

    ```ts
    class Foo {
        public numericProp: number;

        public static staticProp: string;
    }
    ```

    **Bad:**

    ```ts
    class Foo {
        public static staticProp: string;

        public numericProp: number;
    }
    ```

  * within an access and a storage modifier properties should always precede
    methods;

    **Good:**

    ```ts
    class Foo {
        public numericProp: number;

        public computeStuff(): void;

        private static stringProp: string;

        private static initStaticStuff(): void;
    }
    ```

    **Bad:**

    ```ts
    class Foo {
        public computeStuff(): void;

        public numericProp: number;

        private static initStaticStuff(): void;

        private static stringProp: string;
    }
    ```

  * getters and setters should be considered methods, not properties;

    **Good:**

    ```ts
    class Foo {
        public numericProp: number;

        constructor() {}

        public get stringProp(): string;
    }
    ```

    **Bad:**

    ```ts
    class Foo {
        public numericProp: number;

        public get stringProp(): string;

        constructor() {}
    }
    ```

  * constructor should always precede other methods within its access modifier.

    **Good:**

    ```ts
    class Foo {
        constructor() {}

        public computeStuff(): void {}
    }
    ```

    **Bad:**

    ```ts
    class Foo {
        public computeStuff(): void {}

        constructor() {}
    }
    ```

  * parameters of generics are named with `T` suffix: `GenericParameterT`.

## File naming

* Files and directories should be named in lower case, with underscores (`_`) as
  word delimiters.

  **Good:**

  ```
  foo/bar_baz.ts
  ```

  **Bad:**

  ```
  foo/barBaz.ts
  foo/bar-baz.ts
  ```

* Names should be short, preferably one or two words.

* Names may be different from names of exported entities.

* Repeating name of a directory in names of files in that directory should be
  avoided.

  **Good:**

  ```
  polygon/buffer_writer.ts
  ```

  **Bad:**

  ```
  polygon/polygon_buffer_writer.ts
  ```

## Workflow

We use workflow heavily inspired by [git flow](https://nvie.com/posts/a-successful-git-branching-model/).
Following branches exist permanently or intermittently in the repository:

* `master` — stable source tree, corresponds to production;
* `dev` — branch the on-going work happens in, features are merged (via PRs) into
  that branch;
* `rc` — branch for reading code for shipment to production, mainly for bug
  fixes (the name of the branch is an abbreviation of "release candidate");
* `hotfix` — for fixing mishaps in production.

### Development

If you don't have local `dev` simply create it and set it to track the remote one:

```sh
git checkout -b dev origin/dev
```

If you commit a change, don't forget to add `dev` to `Fix Version` in corresponding
Startrek ticket.

### Release

All release related work happens in `rc` branch. A new `rc`'s created from `dev`:

```sh
git checkout -b rc dev
make minor # bump version, a new tag is created
git push -u origin rc --follow-tags # assuming that origin remote is github.y-t.ru
```

If there already is a remote `rc`, you'll need to create a local `rc` and set it
to track the remote one:

```sh
git checkout -b rc origin/rc
```

If you commit a change, don't forget to add `rc` to `Fix Version` in corresponding
Startrek ticket.

To deploy `rc` to testing you'll need:

```sh
git pull # to ensure you have latest changes
make patch
git push --follow-tags
```

When `rc` stabilized, it's merged into `master` and `dev` and deleted:

```sh
# master
git checkout master
git merge --no-ff rc
git push

# dev
git checkout dev
git merge --no-ff rc
git push

# delete rc
git branch -d rc
git push origin :rc
```

After that a new `rc` may be created.

### Hotfix

If something bad happend and a fix need right away. Here's steps to take:

1. create `hotfix` branch from `master`: `git checkout -b hotfix master`;
2. do not forget to actually fix the problem:)
3. bump patch number: `make patch`;
4. push changes: `git push --follow-tags`;
5. after deploying the fix, merge `hotfix` into `master`, `dev` and current `rc`
   if deems needed:
6. delete `hotfix` branch (both local and remote one).


## Deploy and CI

`Vector` built static is tagged with release version and uploaded into `S3 MDS` bucket. There are also resources
containing actual version of `Vector` for specified env and major version, e.g. `testing_version_1` refers to a `1.x`
version for `testing`. `JSAPI` fetches those resources at intervals hence the process of deploying `Vector` comes down
to simply updating those version resources.

### Release
Release is essentially uploading built static to the S3 MDS bucket. Normally release is created by the CI, when a new
tag is created. Public URL is [https://yastatic.net/s3/mapsapi-v3/vector/{{version}}/out/vector.min.js]().

### Deploy
Deploy for `Vector` is updating version resource that will be fetched by `JSAPI` at given intervals. Version resources
are stored in the same bucket as static, differ by env (`testing`, `production`) and major version (`1.x`, `2.x`, ...)
and named like `testing_version_1`. CI automatically deploys testing after release is created. Production is to be
deployed manually. **Before deploy, version must be released**. You'll need [access keys](#access-keys) for `MDS S3` to
do it.
```sh
# You don't need to set keys if you have `yav` installed
MAPSAPI_V3_S3_ACCESS_KEY_ID="<key_id>" MAPSAPI_V3_S3_SECRET_ACCESS_KEY="<access_key>" make deploy-production
```


### Trendbox CI

[Trendbox CI](https://github.yandex-team.ru/search-interfaces/trendbox-ci) is a CI based on
[Sandbox](https://sandbox.yandex-team.ru).

The build is done automatically on `push` and `pull request` events in `dev` branch and on `push tag` event in any
branch. The steps that are performed during the build:
* [Install dependenices](#install-dependencies)
* [Lint](#lint)
* [Unit testing](#unit-testing)
* [Build](#build)
* [Functional testing](#functional-testing)
* [Release the build](#release-the-build) (only when tag is created)
* [Deploy testing](#deploy-testing) (only after release)

The build runs in the LXC (Linux containers) container with `node.js` and `Chromium` which is needed for `Karma` unit
tests to run.

#### Install dependencies
Install dependencies for Vector and functional tests.

#### Lint
Run `tslint` against source and unit tests code.

#### Unit testing
Run `Karma` unit tests in headless `Chromium`.

#### Build
Build production version of Vector.

#### Functional testing
Run functional tests with remote `selenium` grid comparing actual local build with production vector. To make local
vector build available for remote grid it needs to be published which is achieved with `sandbox` helper tool
`synchrophazotron`. Functional testing is currently unstable so it doesn't affect the build.

#### Release the build
The build is released when a git tag (with version) is created and pushed (normally it would happen in `rc`).

#### Deploy testing
After built version of `vector` is released, the testing for current major version is deployed.


### Access keys
Operations such as [deploy](#deploy) have to be done with access keys for `MDS S3`. There are few ways you can get them:
* Get your own pair by querying
`curl -XPOST -H"Authorization: OAuth <oauth_token>" "https://s3-idm.mds.yandex.net/credentials/create-access-key" --data "service_id=3463" --data "role=admin"`
(`AccessKeyId` and `AccessSecretKey` in the response, respectively).
Your `oauth_token` can be obtained in
[application](https://oauth.yandex-team.ru/authorize?response_type=token&client_id=6797456f343042aabba07f49b478c49b).
**Care to store `AccessSecretKey` as it can't be received more than once**.
* Get existing pair in `ya vault` [secret](https://yav.yandex-team.ru/secret/sec-01cxcr7akjnh3p501henp42y5y). About
`ya vault`: https://wiki.yandex-team.ru/passport/yav-usage.
* Install [yav app](https://vault-api.passport.yandex.net/docs/#cli) via `pip` and keys will be obtained and used
automatically. Installation command: `pip install yandex-passport-vault-client -i https://pypi.yandex-team.ru/simple`.
Access keys are simply fetched from the same secret mentioned in an option above using `yav` and used in case env vars
haven't been provided.

### Uploading static (releasing) manually
At first, make sure you know what are you doing. Now that you bear a responsibility, you'll need [keys](#access-keys):
```sh
# bump version, a new tag is created
make patch
# build static
YENV=production make all
# upload it, the version is taken from `package.json`
MAPSAPI_V3_S3_ACCESS_KEY_ID="<key_id>" MAPSAPI_V3_S3_SECRET_ACCESS_KEY="<access_key>" make upload-static
```
