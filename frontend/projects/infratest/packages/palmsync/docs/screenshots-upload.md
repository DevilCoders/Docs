# Настройка выгрузки скриншотов в S3-MDS

## Авторизация в S3-MDS

Для выгрузки скриншотов в S3-MDS необходимо проделать несколько шагов:

1. [Запросить роль в системе IDM](https://nda.ya.ru/t/jROxu2tQ3aGoCf).
    <details>
        <summary>Пример заполненной формы</summary>
        <img src="./images/s3-idm-form-example.png" width="500"/>
    </details>

    * Система: **S3-MDS** (prod)
    * Service: **CrowdTest Runner**
    * Request type: **Service account role**
    * Role: **Admin** (данная роль нужна для возможности загрузки скриншотов в бакет)
    * Сотрудник или группа: <пользователь, для которого запрашивается доступ>
    * В описании запроса укажите тикет, где производите настройку выгрузки скриншотов

2. После одобрения роли [получите OAuth токен в системе S3-MDS](https://wiki.yandex-team.ru/mds/s3-api/authorization/#upravlenieaccesskeys)
3. Создайте пару ключей `AccessKeyId` и `AccessSecretKey` c помощью API:
    * oauth_token – токен полученный в п.2
    * service_id – 31135 – это [ABC-сервис](https://abc.yandex-team.ru/services/crowdtest-runner/)
```bash
curl -XPOST -H"Authorization: OAuth <oauth_token>" "https://s3-idm.mds.yandex.net/credentials/create-access-key" --data "service_id=<service_id>" --data "role=admin"
```

4. Полученные `AccessKeyId` и `AccessSecretKey` используйте в конфигурации palmsync

> :warning: AccessSecretKey необходимо запомнить, получить его еще раз будет невозможно!

Более подробно и обобщенно процесс авторизации описан в [официальной документации S3-MDS](https://wiki.yandex-team.ru/mds/s3-api/authorization/)

## Конфигурация palmsync

 * `s3MdsUpload` – Включает выгрузку скриншотов в S3 и подмену ссылок на них в шагах. По умолчанию выгрузка отключена.
 * `s3MdsEndpointUrl` – S3 REST API URL. По умолчанию `https://s3.mds.yandex.net`.
 * `s3MdsPublicUrl` – URL публичного API. По умолчанию `https://s3.yandex.net"`.
 * `s3MdsBucketName` – Название S3-контейнера. URL публичного API. По умолчанию `crowdtest`.
 * `s3MdsAccessKeyId` – Идентификатор (логин) в S3-MDS.
 * `s3MdsAccessSecretKey` – Пароль в S3-MDS.
 * `s3MdsUploadJingScreenshots` - Включает выгрузку скриншотов из jing в S3. По умолчанию `true`.

Настройка `.palmsync.conf.js`:

```js
module.exports = {
    s3MdsUpload: false,
    s3MdsEndpointUrl: "https://s3.mds.yandex.net",
    s3MdsPublicUrl: "https://s3.yandex.net",
    s3MdsBucketName: "crowdtest",
    s3MdsAccessKeyId: "",
    s3MdsAccessSecretKey: ""
};
```

Аналогичные CLI-опции:

* `--s3-mds-upload`
* `--s3-mds-endpoint-url`
* `--s3-mds-public-url`
* `--s3-mds-bucket-name`
* `--s3-mds-access-key-id`
* `--s3-mds-access-secret-key`

Опции из CLI переопределяют значения из конфигурационного файла `.palmsync.conf.js`.

У Palmsync есть возможность выгружать скриншоты из сервиса **Jing** в **MDS**, для этого необходимо добавить портальный токен (любой токен полученный в oauth.yandex-team.ru) в переменную окружения `palmsync_jingToken`.
