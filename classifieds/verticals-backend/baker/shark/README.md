```
███████╗██╗  ██╗ █████╗ ██████╗ ██╗  ██╗
██╔════╝██║  ██║██╔══██╗██╔══██╗██║ ██╔╝
███████╗███████║███████║██████╔╝█████╔╝
╚════██║██╔══██║██╔══██║██╔══██╗██╔═██╗
███████║██║  ██║██║  ██║██║  ██║██║  ██╗
╚══════╝╚═╝  ╚═╝╚═╝  ╚═╝╚═╝  ╚═╝╚═╝  ╚═╝
```

*Shark* is *Yandex Verticals* credit broker service.

#### Projects wiki
https://wiki.yandex-team.ru/vertis/shark/


#### Structure
  * `core`    - dao, services, clients
  * `api `    - api
  * `tms`     - scheduler, consumers
  * `extdata` - extdata uploader


#### Local run
Download [latest release of shiva-conf](https://github.com/YandexClassifieds/shiva-conf/releases/latest), unarchive
and place binary into `/usr/local/bin`.
Next get [Vault OAuth token](https://vault-api.passport.yandex.net/docs/#oauth) and place it info ~/.zshrc or ~/.bashrc

```
VAULT_TOKEN=[YOUR-TOKEN]
export VAULT_TOKEN
```

Also set environment variables from [development-environment](https://yav.yandex-team.ru/secret/sec-01fyyb9hzny5wsyqqjere9m3t8)

Run command:
```
bazel run //baker/shark/api:service
```


#### Unit tests

Run command:
```
bazel test //baker/shark/core:core-test --test_output=streamed --test_filter=PhoneSpec
```


#### Deployment
  * [api](https://a.yandex-team.ru/projects/verticals/ci/releases/timeline?dir=classifieds%2Fverticals-backend&id=shark-api-release)
  * [tms](https://a.yandex-team.ru/projects/verticals/ci/releases/timeline?dir=classifieds%2Fverticals-backend&id=shark-tms-release)
  * [extdata](https://a.yandex-team.ru/projects/verticals/ci/releases/timeline?dir=classifieds%2Fverticals-backend&id=shark-extdata-release)

API deployed from branch is available at:
http://shark-api-pull-XXX-main.vrts-slb.test.vertis.yandex.net

[Manual release task](https://a.yandex-team.ru/projects/verticals/ci/actions/launches?dir=classifieds%2Fverticals-backend&id=service-manual-release)
More detailed instructions see [here](https://wiki.yandex-team.ru/users/darl/arcadia-pervye-shagi/#relizizvetki)


#### IntelliJ IDEA
Recommended plugins:
  * [ZIO for IntelliJ](https://plugins.jetbrains.com/plugin/13820-zio-for-intellij)
  * [Arc for Intellij](https://docs.yandex-team.ru/devtools/intro/quick-start-guide#jb-plugin-setup)

#### Scalaxb code generation
  1) install [coursier](https://get-coursier.io/docs/cli-installation)
  2) install scalaxb running: `cs install --contrib scalaxb`
  3) run `make generate-scalaxb` from shark root directory 
