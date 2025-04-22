# CAuth server


Приложение живет в Y.Deploy:

- https://deploy.yandex-team.ru/stage/master-prod
- https://deploy.yandex-team.ru/stage/master-testing
- https://deploy.yandex-team.ru/stage/public-prod
- https://deploy.yandex-team.ru/stage/public-testing


Сборка и выкладка стандартно — катим релизером в Y.Deploy.
Находясь в каталоге cauth2-master или cauth2-public, в зависимости от того, что релизим:

 `ya tool releaser release`

Эта команда:
1. Апнет версию и подтянет коммиты в changelog, откроет changelog на редактирование. Нужно посмотреть глазами, при необходимости, отредактировать. Желательно убирать коммиты master-only из changelog'а public, и наоборот. Оставлять только коммиты, связанные с изенением кода сервиса.
2. Соберет docker-образ.
3. Запушит его в docker-registry.
4. Запушит changelog и тег новой версии в репозиторий.
5. Запустит деплой в stage Y.Deploy testing.

Если редактирование changelog завершить без сохранения файла, выполнение команды `releaser release` остановится.
На шаге 4 releaser в arc очень долго ждет прекоммитных проверок и может отвалиться по таймауту. Можно в выводе releaser найти ссылку на PR с апом changelog, перейти по ней в интерфейс arc и снять галку с прекоммитной проверки.

## Выкладка в продакшн

Для деплоя в продакшн заводим релизный тикет через шаблон "релиз" в очереди st/CAUTH. Шаблон проставляет `Tags: release` и `Components: Релиз`. В тикет записываем ченджлог, глядя на дифф между текущей версией в проде и версией подготавливаемого релиза. Можно указывать только ключи тикетов, если их достаточно для отражения изменений в релизе. Если при релизе нужна миграция, указываем это в тикете. Желательно пошагово описать последовательность выкладки и выполнения миграции (миграция до релиза/с выкладкой на временный контейнер/после релиза).
Пример тикета https://st.yandex-team.ru/CAUTH-2696.

Для CAuth включена политика sox, поэтому катить нужно с созданием Deploy-тикета и последующим аппрувом (опция `-dd`, `deploy-draft`). Необходимым условием для аппрува должно быть состояние всех привязанных тикетов в статусе "Протестировано" или комментарий в них с отметкой о тестировании.

По умолчанию releaser выкатывает в тестинг, поэтому указываем стейдж вручную с опцией `-e` (`environment`). В комментарии к релизу указываем релизный тикет:

```ya tool releaser deploy -e <stage-name> -v <version> -dd -dcf="https://st.yandex-team.ru/CAUTH-1234: Релиз master x.xx.x"```


## Тесты

Тесты master и public отделены друг от друга и выполняются независимо. Запускаются через `ya make` внутри каталога приложения:

```cd master; ya make -j6 -ttt .```

Если нужно провалиться в дебаггер:
```ya make -j6 -ttt . --regular-tests -D NO_FORK_TESTS=1 --test-debug --test-disable-timeout --test-stdout --test-stderr```

Запуск отдельного теста
```ya make -j6 -ttt . --regular-tests -D NO_FORK_TESTS=1 --test-debug --test-disable-timeout --test-stdout --test-stderr -F tasks.test_import_staff.py::test_import_staff```

Как сгенерировать миграцию:
------------

Собираем основной бинарик:

> ya make -j6 wsgi/

Запускаем собранный бинарик с нужными переменными окружения:
> Y_PYTHON_ENTRY_POINT="infra.cauth.server.master.manage" DJANGO_SETTINGS_MODULE=infra.cauth.server.master.settings YENV_TYPE=development.migration YENV_NAME=intranet ./wsgi/master.wsgi makemigrations

`YENV_TYPE=development.migration` нужен для подхватывания конфига базы с бэкендом sqlite
