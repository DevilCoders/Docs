# shiva-conf

Replace environment variables in HOCON `.conf` files from [deploy manifest](https://wiki.yandex-team.ru/vertis-admin/deploy/deploymanifest/) and [Yandex.Vault](https://yav.yandex-team.ru)

## Releases

Latest (1.6.0) [Linux](https://proxy.sandbox.yandex-team.ru/3325394356) [MacOS](https://proxy.sandbox.yandex-team.ru/3325395572)


## Usage

```shell
shiva-conf \
  --service=name \
  --conf=./application.conf \
  --token=token \
  > application.local.conf
```

* **service** - https://admin.vertis.yandex-team.ru/services
* **conf** - Path to HOCON file (e.g. `application.conf`)
* **token** - Vault OAuth token: https://vault-api.passport.yandex.net/docs/#oauth (at the bottom of a page)
* **quiet** - Do not print logs

## Example

From:

```properties
app {
  host = ${APP_HOST}
  port = ${APP_PORT}
}
```

Given:

```yaml
test:
  config:
    params:
      APP_HOST = ${sec-123:ver-456:host}
      APP_PORT = "80"
```

To:

```properties
app {
  host = "localhost"
  port = "80"
}
```

## Download

Executable is available in the [latest release](https://github.com/YandexClassifieds/shiva-conf/releases/latest) assets.

## FAQ

### shiva-conf cannot be opened because the developer cannot be verified

Click **Cancel**.

<img width="532" src="https://user-images.githubusercontent.com/2979521/109527056-4c775600-7ac4-11eb-806d-fb754c19e190.png">

Go to System Preferences -> Security & Privace -> General -> **Allow Anyway**.

<img width="780" src="https://user-images.githubusercontent.com/2979521/109527276-85afc600-7ac4-11eb-9101-4bc8bcc52cd3.png">

Finally click **Open**.

<img width="581" src="https://user-images.githubusercontent.com/2979521/109527321-8fd1c480-7ac4-11eb-92d3-3ba490d4a542.png">

