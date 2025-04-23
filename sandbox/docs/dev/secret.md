# Использование секретов

Очень часто в задачах требуется использовать различные пароли, токены, SSH ключи и так далее. Все эти данные объединяет то, что их нужно хранить в секрете, поэтому их так и называют - **секреты**.

{% note warning %}

По умолчанию большинство разделов единого репозитория доступны на чтение всем пользователям,
поэтому хранить секреты в исходном коде категорически запрещено.
Существуют специальные сканеры безопасности, которые автоматически находят секреты в репозитории и заставляют владельцев перевыпускать скомпрометированные секреты.
Рекомендуемый способ хранения секретов в Яндексе - использование [секретницы](https://yav.yandex-team.ru/).

{% endnote %}

Исторически Sandbox имел собственное хранилище секретов под названием [Sandbox Vault](https://sandbox.yandex-team.ru/admin/vault).
Сегодня это хранилище признано устаревшим и все новые задачи должны использовать интеграцию с [Секретницей](https://yav.yandex-team.ru). Подробнее про Секретницу можно почитать по ссылкам:

* [Как создавать секреты через браузер](https://wiki.yandex-team.ru/passport/yav-usage/)
* [Работа с Секретницей через API](https://vault-api.passport.yandex.net/docs/)

Для понимания дальнейшего нам потребуется несколько понятий:

* **Секрет** - набор пар ключ-значение. Ключи в каждом секрете уникальны.
* **Идентификатор секрета** — строка вида `sec-<uuid>`.
* **Версия секрета** — строка вида `ver-<uuid>`. Каждый секрет имеет хотя бы одну версию. Любое изменение хотя бы одного из ключей секрета создаёт новую версию.
* **Файл с секретом** — Секретница позволяет сохранить файл, и хранит его в виде base64.

## Работа с секретами { #howto }

**Получить секрет**. Сделать это можно несколькими способами.

{% note warning %}

При получении секретов во время выполнения задачи нужно предварительно дать Sandbox право на чтение секрета (["делегировать" секрет](#delegate-secret)).

{% endnote %}

**Способ 1. Объявить параметр задачи.**

```python
from sandbox import sdk2

class MyTestTask(sdk2.Task):

    class Parameters(sdk2.Parameters):
        tokens = sdk2.parameters.YavSecret(
            "YAV secret identifier (with optional version)",
            default="sec-0abc@ver-0def"
        )

    def on_execute(self):
        tokens = self.Parameters.tokens.data()
        token = tokens["some_token"]
```

В режиме редактирования параметр отображается так:

![Редактирование параметра-секрета](img/secret-parameter.png "Редактирование параметра-секрета")

При выборе секрета показывается список его версий. Выбранный секрет можно делегировать, если этого ещё не было сделано:

![Делегирование секрета](img/secret-parameter-delegate.png "Делегирование секрета")

В значении параметра можно указать ключ по умолчанию, добавив к нему `#key_name`, который затем можно использовать в коде задачи:
```python
token = self.Parameters.tokens.data()[self.Parameters.tokens.default_key]
```

**Способ 2. Обратиться к секрету во время выполнения задачи.**

Для доступа к секретам из кода задачи важно учитывать, что

* Получение секретов возможно во всех методах с префиксом `on_`, кроме `on_create`, `on_save` и `on_enqueue`.
* Получив секрет, Sandbox не будет выводить его значение в логах задачи, но лучше стараться вообще не логировать секреты.
* Делегирование секрета в этом случае надо выполнить [вручную заранее](#delegate-secret):


Пример кода, работающего с секретами:
```python
import base64
from sandbox import sdk2

class MyTestTask(sdk2.Task):

    def on_execute(self):
        secret1 = sdk2.yav.Secret("sec-0abc", "ver-0def")  # Exact version
        oauth_token = secret1.data()["token"]

        secret2 = sdk2.yav.Secret("sec-0dead")  # Latest version
        password = secret2.data(auto_decode=True)["pwd"]
        file_content = secret2.data(True)["my_file"]  # file will be decoded from base64 automatically (recommended)

        secret3 = sdk2.yav.Secret("sec-0dead")  # Latest version without auto-decoding of 'file' secrets
        password = secret3.data()["pwd"]
        file_content = base64.b64decode(secret2.data()["my_file"])  # will NOT be decoded from base64 automatically

        secrets = sdk2.yav.Yav(  # Multiple secrets
            some_tokens=sdk2.yav.Secret("sec-0aab", "ver-1234"),
            some_passwords=sdk2.yav.Secret("sec-0aac", "ver-0001"),
        )
        some_token = secrets.some_tokens["oauth"]
```

### Делегировать секрет сервису Sandbox { #delegate-secret }
Делегирование секрета означает, что в Секретнице будет создан токен для доступа приложения `sandbox_production` и Sandbox будет запрашивать в Секретнице значение секрета от имени пользователя равного автору задачи.
Если задачу пытается запустить кто-то, у кого нет доступа на чтение секрета, он получит ошибку вида `Cannot fetch secret values: sec-01fhb0ra68f8069vk7zwp4hm06: code='access_error', message='Access denied'`

Для начала нужно получить sandbox-token [здесь](https://sandbox.yandex-team.ru/oauth).
Затем вызвать:
```bash
$ curl -X POST 'https://sandbox.yandex-team.ru/api/v1.0/yav/tokens' -H 'Content-Type: application/json' -H 'Authorization: OAuth <sandbox-token>'  -d '{"secrets": [{"id": "sec-<id-of-secret>"}]}'
```


### Классы для работы с секретами

1. `sdk2.yav.Secret` - основной sdk2 класс, обеспечивающий получение секрета в коде задачи. Принимает в конструктор:
   1. `secret` -  имя секрета в Yav
   2. `version` - версия секрета в Yav. По умолчанию берется последняя версия
   3. `default_key` - ключ в словаре секретов. Используется в методе `value` для получения конкретного секрета по ключу.

   Имеет методы:

   * `data(auto_decode: bool)` - получение секрета в виде словаря; параметр `auto_decode` позволяет указать, что необходимо автоматически декодировать содержимое секретов, если среди значений есть файлы
   * `value(auto_decode: bool)` - получение секрета в виде словаря если `default_key` не указан, или значение секрета по ключу `default_key`; параметр `auto_decode` - см. выше
2. `sdk2.parameters.YavSecret` - sdk2 класс для описания параметра типа YavSecret, наследующийся от параметра sdk2.parameters.String. Хранит описание секрета в виде строки `secret@version#default_key`, где `secret`, `version`(опционально) и `default_key`(опционально) аналогичны полям из `sdk2.yav.Secret`. В качестве `default` в параметр передается описанная ранее строка.

## Миграция из Sandbox Vault { #migration }

Если код вашей задачи использует секреты, хранящиеся в Sandbox Vault, то существует два способа переехать в Секретницу.

**Способ 1. Автоматически перенести секреты из Sandbox Vault в Секретницу.**

1. [Получите](https://oauth.yandex-team.ru/authorize?response_type=token&client_id=ce68fbebc76c4ffda974049083729982) OAuth-токен к API Секретницы.
2. Сохраните полученный токен в Sandbox Vault или в Секретницу. Если сохранили в секретницу, [делегируйте этот секрет](#delegate-secret).
3. [Создайте задачу](../tasks.md#launch-task) типа [MIGRATE_SECRETS](https://sandbox.yandex-team.ru/tasks?children=true&type=MIGRATE_SECRETS). В параметрах задачи укажите:
    * Cекрет с токеном.
    * Cписок секретов из Sandbox Vault, которые нужно перенести. В Sandbox Vault к секретам обращаются в формате `<owner>:<name>`. В Секретнице каждый такой секрет преобразуется в один из ключей в словаре. В параметрах задачи указывается новое и старое значение ключа.
    * Имя секрета в Секретнице, в который будут скопированы значения секретов.

    ![Автоматический перенос секретов](img/secret-migrate-parameters.png "Автоматический перенос секретов")

4. Запустите задачу. При успешном завершении на странице задачи появится ссылка на новый секрет в Секретнице:

    ![Секреты успешно перенесены](img/secret-migrate-result.png "Секреты успешно перенесены")

5. Удалите секрет с токеном API Секретницы.

**Способ 2. Использовать секреты из Секретницы через sdk2.Vault.**

Секреты из Секретницы можно начать использовать в уже существующих задачах с минимальными изменениями. Для обращения к секретам из Секретницы используется формат `sec-0abc@ver-0def[key]` или `sec-0abc[key]`.

```python
from sandbox import sdk2

class MyTestTask(sdk2.Task):

    class Parameters(sdk2.Parameters):
        token_parameter = sdk2.parameters.Vault("Some token parameter", default_value='sec-0aab@ver-1234[key]')

    def on_execute(self):
        secret1 = sdk2.Vault.data(None, "sec-0aab@ver-1234[key]")
        secret2 = sdk2.Vault.data("sec-0abc[key]")
```

В параметре `owner` можно передавать любое значение — он будет проигнорирован.
