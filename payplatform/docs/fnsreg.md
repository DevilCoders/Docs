Микросервис управления [пере]регистрациями ККТ в ФНС (FnsReg)
===============================================================

Хосты
-----

Хосты `testing`:

- [swagger-ui](https://fnsreg-test.in.yandex.net/swagger-ui) (`recommended!`)
- [redoc](https://fnsreg-test.in.yandex.net/redoc)
- [rapidoc](https://fnsreg-test.in.yandex.net/rapidoc)
- [API](https://fnsreg-test.in.yandex.net)

Хосты `production`:

- [swagger-ui](https://fnsreg.yandex.net/swagger-ui) (`recommended!`)
- [redoc](https://fnsreg.yandex.net/redoc)
- [rapidoc](https://fnsreg.yandex.net/rapidoc)
- [API](https://fnsreg.yandex.net)

[Окружение в Y.Deploy](https://yd.yandex-team.ru/stages/fnsreg)
[Проект в CI](https://a.yandex-team.ru/projects/spirit/ci/releases/timeline?dir=payplatform/fnsreg&id=fnsreg-release)
[Код](https://a.yandex-team.ru/arc/trunk/arcadia/payplatform/fnsreg)

Сборка
------

Сборка осуществляется стандартными средствами аркадии: `ya make` и `ya package`.

Генерация IDEA проекта
----------------------

Чтобы сгенерировать проект для IDEA необходимо:

- Поставить [arcadia-плагин](https://a.yandex-team.ru/arc/trunk/arcadia/devtools/intellij) если еще нет
- Выполнить следующую команду из директории `payplatform/fnsreg`:

```bash
ya ide idea -DMANUAL_TEST=ON --directory-based --group-modules=tree --iml-in-project-root --generate-junit-run-configurations --with-content-root-modules --separate-tests-modules -r %OUT_DIR%
```

- Импортировать настройки code-style по инструкции из выхлопа генератора

`OUT_DIR` - директория куда генератор сохранит проект.

Запуск интеграционных тестов
----------------------------

Интеграционные тесты ходят в тестовый стенд апи ФНС, поэтому их запуск в автосборке отключен. Для запуска тестов из IDE необходимо выполнить следующие шаги:

- Взять тестовый [tvm-токен](https://yav.yandex-team.ru/secret/sec-01et2w1e4kwp5cjma5t6va82fj/explore/version/ver-01et2w1e5qe07z4w5t7wxnc88q) и прописать его в файле `payplatform/fnsreg/service/src/integration-test/resources/tvmtool.conf` в секции `clients.me.secret`. Коммитить эту правку не нужно!
- Запустить тесты `RegistrationTest` и `ReregistrationTest`

{% note warning %}

Тестовый стенд ФНС жутко нестабильный и частенько отдыхает, поэтому не нужно удивляться, что тесты не проходят со странными ошибками. Уточнить состояние стенда можно в соответствующем [whatsapp-чатике](https://chat.whatsapp.com/DJ3lXqXp8f3A9NBS4VAxfY).

{% endnote %}
