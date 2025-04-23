# Управление секретами в Огороде

Для хранения секретов нужно использовать [Секретницу](https://yav.yandex-team.ru/).

## Как создать

1. Создайте секрет в Секретнице по [инструкции от паспортистов](https://wiki.yandex-team.ru/passport/yav-usage/). Ключ напишите `ЗАГЛАВНЫМИ_БУКВАМИ`.
2. Для секретов, которые будут использоваться в контурах `stable`, `datatesting` или пользовательских контурах, выдайте роботу `robot-maps-sandbox` право на чтение секрета:

    ![](img/secrets_access_stable.png)

3. Для секретов, которые будут использоваться в песочницах (актуально только для разработчиков Огорода), выдайте право на чтение секрета на ABC-сервис `maps-qyp-garden`:

    ![](img/secrets_access_development.png)

### Как доставить до Огорода

1. Впишите плейсхолдеры для ваших секретов в шаблоны для настроек окружения:

    * в контуре `stable` в файл [environment_settings.stable.json](https://a.yandex-team.ru/arc/trunk/arcadia/maps/garden/scheduler/config/environment_settings.stable.json);
    * в контуре `datatesting` в файл [environment_settings.datatesting.json](https://a.yandex-team.ru/arc/trunk/arcadia/maps/garden/scheduler/config/environment_settings.datatesting.json);
    * в пользовательских контурах в шаблон [environment_settings_user_template.stable.json](https://a.yandex-team.ru/arc/trunk/arcadia/maps/garden/scheduler/config/environment_settings_user_template.stable.json).

    Пример:
    ```json
    {
        "my_module": {
            "my_secret": "{{ ENV.MY_MODULE_SECRET_FROM_YAV }}"
        }
    }
    ```

2. Впишите имена и версии секретов в [sedem_config](https://arcanum.yandex-team.ru/arc/trunk/arcadia/maps/garden/scheduler/sedem_config/secrets.yaml) в нижнюю половину файла: секция `stable` - для любых контуров в стабильном инстансе Огорода.

    Пример:
    ```yaml
    - name: sec-01csh4mfdftcb4rpfss8nyckc9
      version: ver-01es0zztg7qfte37es329m7yeq
      field: MY_SECRET
      env: MY_MODULE_SECRET_FROM_YAV
    ```

3. Для секретов, которые будут использоваться в песочницах (актуально только для разработчиков Огорода), выставите тег `maps_garden_development`:

    ![](img/secrets_tags_development.png)

### Как читать

Словарь с настройками окружения будет передан в метод `Task.load_environment_settings` перед запуском задачи.

```py
class MyTask(Task):
    def load_environment_settings(self, environment_settings):
        super().load_environment_settings(environment_settings)
        self._my_secret = environment_settings["my_module"]["my_secret"]
```
