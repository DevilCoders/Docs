# Что это
Обработчик гитхабных хуков, который умеет:
- парсить номера задач трекера из заголовка пулл-реквеста
- проставлять в задачах поля "ветка" и "стенд"
- при медже пулл-реквеста переводить статус задачи

Для репозитория `morda/main` дополнительно обрабатываются события `push`:

1. пределяется пулл-реквест, соответствующий ветке
2. для пулл-реквеста определяются связаные задачи в трекере
3. в пулл-реквест проставляется статус `schema-guard`
   - `success`, если у задачи нет тега `need_schema_tests` или есть изменения в схема тестах
   - `failure`, если у задачи есть тег `need_schema_tests` и нет изменений в схема тестах

## Где развёрнут
В я.деплое тестинг и прод
https://deploy.yandex-team.ru/stages/gitworker-test
https://deploy.yandex-team.ru/stages/gitworker

## Как обновить
1. Проверить локально, запустив командой

`APP_PORT=8080 GITHUB_TOKEN=... STARTREK_OAUTH_TOKEN=... node ./app/index.js`

2. Поднять версию и запушить коммит

`npm version patch`

3. Собрать докер образ

`npm run build`

3. Запушить образ в реестр

`npm run push`

Для пуша нужно залогиниться [по инструкции](https://wiki.yandex-team.ru/tools/dev/qloud/docker/#vpervyjjraznachinaemrabotatsdokeromvtulzax)

4. [В тестинге](https://deploy.yandex-team.ru/stages/gitworker-test) поменять версию, проверить что приложение работает
5. [В продакшне](https://deploy.yandex-team.ru/stages/gitworker) поменять версию, проверить что приложение работает

