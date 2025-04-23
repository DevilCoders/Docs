В задаче `HELLO_%LOGIN%` есть параметр `self.Parameters.login`. Хочется проверить, что введённый логин — действующий, а также использовать в приветствии настоящее имя сотрудника.

Получить эту информацию можно одним запросом в [Staff API](https://staff-api.yandex-team.ru/v3/persons?_doc=1), но он не будет работать без аутентификации: необходим OAuth токен. Передавать токены через параметры задачи или коммитить их напрямую в репозиторий — [запрещено](https://wiki.yandex-team.ru/passport/yav-usage/).

В Sandbox есть два способа безопасно использовать секретные данные в задаче:

* **[Интеграция с Яндекс.Секретницей](https://wiki.yandex-team.ru/sandbox/yav)** — рекомендуемое решение.
* [Sandbox Vault](https://wiki.yandex-team.ru/sandbox/vault/) — встроенное хранилище секретов, считается устаревшим, не следует использовать в новом коде.

Ниже приведён пример работы с Секретницей:

* [Получите OAuth-токен](https://sandbox.yandex-team.ru/oauth) в интерфейсе Sandbox (кроме самого Sandbox он даёт доступ к Staff API).
* Заведите новый секрет на [yav.yandex-team.ru](https://yav.yandex-team.ru/create/secret). Добавьте новую версию с единственным ключом `"token"`.
* Следуя [документации](https://wiki.yandex-team.ru/sandbox/yav/#enable-yav), разрешите задаче `HELLO_%LOGIN%` доступ к Секретнице и проделегируйте этот секрет в Sandbox.
* Используйте секрет в коде задачи:

```python
def on_execute(self):
    ...
    import requests

    login = self.Parameters.login
    token = sdk2.yav.Secret("sec-0000000").data()["token"]

    resp = requests.get(
        "https://staff-api.yandex-team.ru/v3/persons",
        params={"_one": 1, "_fields": "name", "login": "volozh"},
        headers={"Authorization": "OAuth {}".format(token)}
    )
    if resp.status_code == requests.codes.NOT_FOUND:
        raise errors.TaskFailure("Login `{}` does not exist".format(login))

    first_name = resp.json()["name"]["first"]["en"]
    text = (
        "# Hello, {}!\n\n"
        "Thanks for using Sandbox!"
        .format(first_name)
    )
    ...
```

Запустите задачу и убедитесь, что в файл теперь попадает настоящее имя адресата.
