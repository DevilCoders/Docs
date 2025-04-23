```
███████ ██  ██████  ███    ██ ███████ ██████  
██      ██ ██       ████   ██ ██      ██   ██ 
███████ ██ ██   ███ ██ ██  ██ █████   ██████  
     ██ ██ ██    ██ ██  ██ ██ ██      ██   ██ 
███████ ██  ██████  ██   ████ ███████ ██   ██ 
```

*Signer* is *Yandex Verticals* document signing service

#### Projects wiki
https://wiki.yandex-team.ru/vertis/signer/


#### Structure
  * `core`    - dao, services, clients
  * `api `    - api
  * `tms`     - scheduler, consumers


#### Local run
Download [latest release of shiva-conf](https://github.com/YandexClassifieds/shiva-conf/releases/latest), unarchive
and place binary into `/usr/local/bin`.
Next get [Vault OAuth token](https://vault-api.passport.yandex.net/docs/#oauth) and place it info ~/.zshrc or ~/.bashrc

```
VAULT_TOKEN=[YOUR-TOKEN]
export VAULT_TOKEN
```

And run `./tools/local-config-update.sh` in projects home directory to update config `./core/src/main/resources/common.local.conf`.

Also set environment variables from [development-environment](https://yav.yandex-team.ru/secret/sec-01fyyb9hzny5wsyqqjere9m3t8)

Run command:
```
bazel run //baker/signer/api:api
```


#### Unit tests

Run command:
```
bazel test //baker/signer/core:core-test --test_output=streamed --test_filter=PhoneSpec
```


#### Deployment
  * [api](https://a.yandex-team.ru/projects/verticals/ci/releases/timeline?dir=classifieds%2Fverticals-backend&id=signer-api-release)
  * [tms](https://a.yandex-team.ru/projects/verticals/ci/releases/timeline?dir=classifieds%2Fverticals-backend&id=signer-tms-release)

API deployed from branch is available at:
http://signer-api-pull-XXX-grpc.vrts-slb.test.vertis.yandex.net

[Manual release task](https://a.yandex-team.ru/projects/verticals/ci/actions/launches?dir=classifieds%2Fverticals-backend&id=service-manual-release)
More detailed instructions see [here](https://wiki.yandex-team.ru/users/darl/arcadia-pervye-shagi/#relizizvetki)


#### IntelliJ IDEA
Recommended plugins:
  * [ZIO for IntelliJ](https://plugins.jetbrains.com/plugin/13820-zio-for-intellij)
