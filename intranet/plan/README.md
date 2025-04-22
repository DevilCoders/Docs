Описание
=======
Каталог сервисов Яндекса

|Окружение |                            URL|
|----------|------------------------------:|
|Production|     http://abc.yandex-team.ru/|
|Testing   |http://abc.test.yandex-team.ru/|

- [Deploy Production](https://deploy.yandex-team.ru/stages/tools-abc-back-production)
- [Deploy Testing](https://deploy.yandex-team.ru/stages/tools-abc-back-testing)
- [Аминка Production](http://abc-back.yandex-team.ru/admin/)
- [Аминка Testing](http://abc-back.test.yandex-team.ru/admin/)
- [Wiki](http://wiki.yandex-team.ru/intranet/abc/dev)
- [Проект в танкере](https://tanker.yandex-team.ru/?project=abc)

Процесс работы над тикетом и релиз
=========
- взять тикет в работу назначить на себя
- отвести ветку от develop, написать код/тесты
- сделать ПР, дождаться прохождения тестов, при необходимости
можно самостоятельно проверить работоспособность стенда
- запустить процесс ревью `/start`
- после того как внутренний ревьюер закончил ревью - можно отдавать в тестирование (если требуется)
- после тестирования смерджить ПР в develop
- вызвать `ya tool releaser release`
- написать в слак канал `#abcdv_releases` сообщение о том, что катится в тестинг
- тикет выкатится в тестинг
- при необходимости (в тестинг катится несколько задач, которые могут влиять друг
на друга) - запросить тестирование в тестинге (или самому проверить, в зависимости от задачи)
- если проблем в тестинге не обнаружено - выкатить в прод командой `ya tool releaser deploy --stage tools-abc-back-production --deploy-draft`
- написать в слак канал `#abcdv_releases` сообщение вида
```
Релиз 20.73.8
https://deploy.yandex-team.ru/stages/tools-abc-back-production/deploy-tickets/92f0d5c3-cb64-4f36-b56c-94fc74314af4-ticket
https://st.yandex-team.ru/ABC-9713
- ABC-9678: Обновленная валидация слага
@abc-back
```
после чего другой разработчик сервиса запустит процесс выкладки в прод
- после выкладки - проверить, что проблем нет (в логах нет связанных ошибок, на дашборде нет всплеска 5хх) и закрыть тикет


Запуск тестов
=========
Находясь в папке plan/intranet запускать `run_tests.sh` передавая туда нужные аргументы, первым должна
идти маска для фильтрации тестов, примеры вызовов

```
./run_tests.sh unit.services.api.test_services.py::test_percents_round --pdb
./run_tests.sh unit.api.suggest.*
./run_tests.sh unit.services.api.test_services.py::test_edit_oebs_flags_fail*
./run_tests.sh unit.services.api.test_services.py::test_edit_oebs_flags_fail[False-api-v4-metaservice]
```


Запуск без `run_tests.sh`
`ya make -ttt -AF unit.api.idm.test_hooks.py::test_notify_staff_on_remove_role -DNO_FORK_TESTS tests`
или так
`ya make -ttt -AF unit.api.idm.test_hooks.py::test_notify_staff_on_remove_role --test-filename unit/api/idm/test_hooks.py -DNO_FORK_TESTS tests`
второй способ быстрее

Запуск через pycharm:
 - закрыть pycharm, выполнить `ya ide pycharm`
 - поставить постгрю локально, например с https://postgresapp.com/, запустить
 - добавить `export NO_FORK_TESTS="1"` в `pycharm_python_wrapper` файл
 - запускать тесты через зеленую стрелочку в pycharm

Стенды
=========
1. собираются командой `make stand name=abc-1234`, где `abc-1234` - тикет над которым работаешь
2. если нужно пересобрать образ и перевыкатить стенд - используй `make stand-redeploy name=abc-1234`
3. для удаления стендов и фронта и бека - `make delete-stand name=abc-1234`

Если нужно собрать и выкатить новую версию на тестинг без изменения changelog
(например для выкатки пробной версии из ветки) используй команду
`ya tool releaser release -v <ABC-smth> --skip changelog,version,vcs-commit,vcs-tag,vcs-push`

