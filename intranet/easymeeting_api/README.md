# easymeeting

Документация разработчика: https://wiki.yandex-team.ru/intranet/easymeeting/developer-docs/

## Перед началом разработки
Пожалуйста, обратитесь к разработчикам для получения необходимых файлов с "секретами":
```
# 022-auth.conf.local
# 050-oauth.conf.local
```

## Разработка
Проект написан на ```python 2.7```

Если вы только начинаете разрабатывать, нужно всё приготовить.
Для этого нужно выполнить:
```(bash)
make dev-install
```
Команда соберёт нужные докер-образы и настроит БД.

Теперь можно запустить бэкенд: 
```(bash)
make dev-run
```

Бэкенд будет доступен на порту 9000. 
Сменить порт на другой можно через переменную окружения `EASYMEETING_PORT`

## Тесты
Тесты запускаются при каждом PR через trendbox.

Чтобы прогнать тесты локально, нужно выполнить:
```
make test
```

### Как перезаписать vcr-кассеты
Т.к. мы сейчас ± во все сервисы ходим по TVM2, нам при запросах нужно получать TVM-тикеты.
Поэтому кассеты без проблем можно перезаписать только в контейнере Deploy.
Для этого можно использовать, например, бокс `console` тестинга

1. Выкатываемся в `console`, см.  https://wiki.yandex-team.ru/tools/dev/deploy/schi/#kakrelizit
    
    TODO: починить `make console-pytest`, когда срастется https://st.yandex-team.ru/COMMONPY-270.
2. Запускаем там `pytest --vcr-record [once|new_episodes|all] tests` - [подробнее здесь](https://vcrpy.readthedocs.io/en/latest/usage.html#record-modes)
3. Скачиваем новые кассеты

Если используете для этого другой стэнд, не забудьте задать переменную окружения `ENABLE_PYTEST_TVM=1`,
без неё pytest использует моки и не ходит за TVM-тикетами.

## Релиз
Необходим [releaser](https://a.yandex-team.ru/arc/trunk/arcadia/library/python/releaser) >= 0.66.
Если у вас стоит старый releaser python-пакетом -- удалите его, он более не обновляется: `pip uninstall releaser`.

"Установка": 
* `alias releaser="ya tool releaser"`.
* ya, установленный или слинкованный в систему: `ln -s ~/arc/arcadia/ya /usr/local/bin/ya`. Алиас не подойдет, так как releaser исполняет команды dctl через sh.

Релиз:
* releaser release
* releaser deploy --stage easymeeting-production

> [Подробнее про релизы в Деплой](https://wiki.yandex-team.ru/tools/dev/deploy/schi/#kakrelizit)

## Редактирование окружения
Не редактируйте stage через веб-интерфейс, пока не срастется https://st.yandex-team.ru/DEPLOY-1531.
Иначе затрутся переменные окружения box, и сервис ляжет.
Для редактирования параметров стейджа используйте [dctl](https://wiki.yandex-team.ru/deploy/docs/dctl/) и текстовый редактор:
```bash
alias dctl="ya tool dctl"

dctl get stage easymeeting-testing > testing.yaml
open -a PyCharm testing.yaml  # отредактируйте его
dctl put stage testing.yaml
```

## Календарь
- Документация по API https://wiki.yandex-team.ru/Calendar/api/new-web/
- Веб-интерфейс тестинга https://calendar.testing.yandex-team.ru
(осторожно, он шлет письма в продакшн-почту — не создавайте встречи Воложу)

## Сети
* `_EASYMEETING_TEST_NETS_`
* `_EASYMEETING_PROD_NETS_`

## Админка
В админку можно попасть по прямому url бекенда. Нода запрос не пропускает.
