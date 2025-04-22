```
       __        __          __                 __
  ____/ /__  __ / /_ __  __ / /_ ____   ____   / /
 / __  // / / // __// / / // __// __ \ / __ \ / /
/ /_/ // /_/ // /_ / /_/ // /_ / /_/ // /_/ // /
\__,_/ \__,_/ \__/ \__, / \__/ \____/ \____//_/
                  /____/
```

Утилита для дежурного в SWAT.

### Quick start
```
make build
./dutytool --config ../dutytool.config.yaml dc-hosts --dc sas
```

Поддерживается возможность задать путь до конфига в переменной окружения:
```
DUTYTOOL_CONFIG=~/Workspace/arc/a.yandex-team.ru/mail/swat/dutytool.config.yaml
```

### Команды

* `dutytool dc-hosts --dc <DC>` — список хостов qloud окружений из конфига
* `dutytool db` — список хостов кластеров баз в YC, их состояние, роль и локация
* `dutytool yadeploy-template --stage-id <Ya.Deploy stage id>` — отрендерить шаблон stage Яндекс.Деплоя, подставив туда значения delegation token'ов.
* `dutytool drills` — план учений в wiki формате
    * `--dc <DC>` — создать план для конкретного DC (по-умолчанию для всех)
    * `--conductor` — генерировать команды для executor'a в кондукторном формате
    * `--open` или `--close` — выводит только команды открытия/закрытия сервисов
    * `--not-interactive` — генерирует команды для не интерактивного режима экзекьютера. Требует значение `--user`

#### Команда yadeploy-template
Мы уже очень давно хотим хранить описание инфраструктуры в коде. Когда пришёл Ya.Deploy, сначала показалось, что наша мечта наконец-то станет явью. Но, оказалось, что в спеке хранятся delegation token'ы для секретов. А, значит, хранить спеки в репозитории нежелательно.
Поэтому, была написана команда, которая:
* Ожидает на вход stage ID;
* Ожидает что в секции deploy конфига dutytool в разделе `stage_spec` описано, где находится шаблон спеки, и где находится секрет с delegation token'ами
    Например:
    ```
    {
        "deploy": {
            "projects": [{
                "name": "yandexpay",
                "stages": [{
                    "name": "yandexpay-testing"
                    "stage_spec": {
                        "template_arcadia_path": "/billing/yandex_pay/deploy/yandexpay-testing.deploy.yaml"
                        "delegation_token_secret": {
                            "secret_id": "sec-01esewye0nrn5f6q5nc7fme700",
                            "secret_version_id": "ver-01esf7tczn7gm01r6y4tf6p80p",
                        }
                    }
                }]
            }]
        }
    }
    ```
    Актуальную схему лучше посмотреть в коде config.go и в нашем dutytool.config.yaml;
* В секрет `delegation_token_secret` необходимо подложить все delegation token'ы секретов, которые используются в спеке. А имена, которые ты присвоишь ключам в этом секрете, нужно использовать в шаблоне спеки, примерно вот так:
    ```
    yandexpay-ssl-internal:
      delegation_token: {{ call .GetSecretValue "yandexpay-testing.api_yandexpay-ssl-internal" }}
      secret_id: "sec-01esenjn8fd31s2g8pwer0yfhs"
      secret_version: "ver-01esenjnaj2jg84wb5had2p8gy"
    ```

Использовать команду предполагается вот так:
dutytool yadeploy-template yandexpay-testing | ya tool dctl publish-draft stage -

Немного про то, как работают секреты в деплое, и что такое delegation token'ы.
У Ya.Deploy есть интеграция с секретницей yav.yandex-team.ru. В спеке stage есть отдельная секция, где ты описываешь, какие секреты
нужны твоей stage. По ID секрета и ID версии.
Вопрос: а как дать Ya.Deploy доступ до секрета?
Для того, чтобы читать секрет, сотруднику достаточно быть указанным в ACL этого секрета. Но для сервисов, т.е. автоматики
авторы секретницы разработали отдельный механизм аутентификации. Человек, имеющий доступ к секрету, должен зайти на страницу секрета,
выбрать вкладку "Токены" и выписать токен, указав (tvm id, password):
* В качестве tvm id указывается tvmid сервиса, который должен будет иметь доступ к секрету (в нашем случае это YP);
* О пароле вы заранее договариваетесь с сервисом (для YP это полный идентификатор deploy_unit, напр. yandexpay-testing.api)
При создании токена генерируется delegation token, который нужно передать сервису (в нашем случае - через спеку).
Так вот этот самый delegation token хоть и бесполезен, если ты не знаешь tvm secret Деплоя (пароль в случае деплоя знают все - он ведь конвенционален),
его по технике безопасности хранить не положено.

### Доступы
Для работы с API, необходимо получить доступы
1. [Получить](https://oauth.yandex-team.ru/authorize?response_type=token&client_id=40c7d52c1a024f7ab0fbd9e2c9ec51e7) OAuth-токен
2. Прописать токен в файл `~/.dutytool/token-oauth`

