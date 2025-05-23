# qooker

HTTP deploy hook выкладок в Qloud

## Использование

Для использования Qooker, выполните следующее:
* __Укажите Qooker как deploy hook в Platform/Qloud__:
  * __Platform__: Зайдите в окружение, перейдите на таб `Policies`
  и там в поле `Deploy hook` пропишите адрес
  https://qooker.yandex-team.ru/hook
  * __Qloud__ (deprecated): Зайдите в окружение, нажмите кнопку `Create draft`,
  нажмите сверху кнопку `Settings` и там в поле `Deploy hook`
  пропишите адрес https://qooker.yandex-team.ru/hook
* __Укажите конфигурацию для окружения__: создайте ПР в данном
репозитории с необходимыми настройками в модуле [config.py](src/qooker/config.py)
в словаре `CONFIG`. Ваша конфигурация заработает после перевыкатки Qooker.
  * В качестве ключа укажите [регулярное выражение](https://docs.python.org/2/library/re.html) 
  для окружения в виде `<project>.<application>.<environment>`.
  * В качестве значения укажите JSON конфигурации.
  Ниже приведен пример с полным форматом конфигурации:
  ```json
  {
    "notify": {
        "email": {
            "recipients": ["wiki-deployment@yandex-team.ru"],
            "subject_format": "{environmentId} {status}",
            "message_format": "Окружение {env_link} перешло в статус {status}.\n\n{comment}",
            "on_statuses": ["DEPLOYED", "FAILED"]
        }
    },
    "tracker": {
        "transition": "testing",
        "set_version": {
            "enabled": true,
            "version_groups": 2,
            "field_name": "fixVersions"
        },
        "update_description": {
            "enabled": true,
            "section_name": "Стенд",
            "section_body": "{stand_link}",
            "stand_link_constructor": null
        },
        "on_statuses": ["DEPLOYED"],
        "comment": {
            "enabled": true,
            "text": "выкатилось",
            "dont_repeat": true
        }
    }
  }
  ```
    * Параметр `on_statuses` в конфигурации действия указывает, на какие статусы
    окружения должно срабатывать действие. Если параметр не указан, то
    действие будет срабатывать для всех статусов.
    * `notify.email`
      * Параметр `recipients` содержит список email-ов, на который
      будут разослано письмо с заголовком с форматом `subject_format`
      и телом с форматом `message_format`. Если аргументы `subject_format`
      или `message_format` не указаны, используются форматы по умолчанию
      (см. [config.py](src/qooker/config.py)). Для форматов доступны следующие аргументы:
        * `env_link` – ссылка на окружение в Qloud
        * `environmentId` – ID окружения
        * `status` – статус окружения (DEPLOYING, DEPLOYED, FAILED и т.д.)
        * `comment` – комментарий деплоя. Если вы используете
        [releaser](https://github.yandex-team.ru/tools/releaser), то
        в комментарий деплоя попадает changelog последней версии.
        * `version` – версия окружения
        * `statusChangeTs` – timestamp изменения статуса окружения
        * `installation` – инстанс Qloud
    * `tracker`
      * Параметр `transition` указывает transition тикетов из
      комментария деплоя, по которому они перейдут, когда
      окружение перейдет в статус DEPLOYED. Доступный список transition
      тикета можно посмотреть в ручке
      `https://st-api.yandex-team.ru/v2/issues/{TICKET-KEY}/transitions`
      в поле `id`. Например, при деплое в окружение testing можно
      указать `transition='testing'`, а при деплое в окружение
      production – `transition='close'`.
      * Набор параметров `set_version` отвечает за то, чтобы
      тикетам из комментария деплоя прописывать в поле стартрека 
      версию с тем же именем, что у версии выкладки в комментарии деплоя.
      Работает это так – если в комментарии деплоя есть подстрока,
      которая матчится по регулярному выражению
      `Releasing version ([0-9.-]+), changelog:`, то мы извлекаем из нее
      версию, и добавляем ее в указанное поле.
        * `enabled` – если равно `true`, то функциональность включена.
        * `version_groups` – сколько чисел версии нужно брать
        из версии в комментарии деплоя. Например, в комментарии может
        быть указана версия `10.13-4`, а нам нужно прописать в тикет версию
        `10.13`, т.е. первые два числа версии, в этом случае мы указываем
        `version_groups=2`. Если параметр не задан, то мы никак не
        меняем версию из комментария деплоя.
        * `field_name` - название поля стартрека для простановки в него версии, 
        поддерживаются не все поля, список поддерживаемых
        можно найти в `FIELDS_PROCESSORS_MAP`
      * Набор параметров `update_description` отвечает за обновление описания
      тикета, а именно обновляет содержимое секции с именем `section_name` 
      (то, что находится под заголовком `=={section_name}`) на `section_body`.
      В `section_body` можно указать параметр `{stand_link}`, который будет
      заменен на ссылку на стенд. Ссылка на стенд получается из ID окружения
      с помощью функции, имя которой задается параметром `stand_link_constructor`.
      * Набор параметров `comment` отвечает за то, чтобы в тикетах комментария к
      деплою появлялся произвольный информационный коментарий. Поле `text` - текст
      комментария. На данный момент параметризировать это поле нельзя. Поле
      `dont_repeat` - если равно `true`, то если в тикете уже есть такой коментарий
      (совпадает текст и автор комментария), он повторно не постится в тикет.

В будущем конфигурации окружений будут храниться в PGaaS и
редактироваться через Django-админку.

## Перевод тикетов

В данный момент Qooker ходит в API Стартрека роботом
https://staff.yandex-team.ru/robot-stendhal. У этого робота могут
быть проблемы с доступом к очередям тикетов, поэтому над итоговым
решением пока еще думаем.

## Разработка

Для выпуска новой версии введите
```
releaser release
```
