## Как собрать пакет

1. Если на [странице с версиями](https://st.yandex-team.ru/MAYA/versions) в очереди нет нужного номера версии, создать её. Номер версии состоит из x.y., например 2.7
2. Пометить все тикеты, которые войдут в релиз, в поле "Исправить в версии" номер нужной версии
2. [Создать тикет](https://st.yandex-team.ru/createTicket?queue=MAYA) в очереди MAYA, заполнить в названии и в поле "Исправить в версии" номер нужной версии. Указать в поле "исполнитель" - тестировщика вашей команды.
3. Отвести релизную ветку от ветки `dev`, саму ветку назвать `maya-release/{{версия}}`, [пример](https://github.yandex-team.ru/personal-services/frontend/pull/8854)
4. Запустить в релизной ветке:
```bash
npm run package <version> <task_id>
# version - номер версии(будет создан тег),
# task_id - номер релизного таска, созданного на шаге 3
# Пример:
# npm run package 2.7.0 MAYA-100
```
5. Убедиться, что создалась джоба со сборкой пакета: открыть [New CI](https://a.yandex-team.ru/projects/mail_frontend/ci/actions/launches?dir=yandex360%2Ffrontend&id=release), в поле `Select branch` указать `releases/psfront/maya/vX.Y.Z`
6. Дождаться сборки пакета и комментария робота в тикет

## Как установить пакет

```bash
npm run deploy <version> <task_id>
# version - номер версии (для поиска SB-ресурса),
# task_id - номер релизного таска
# Пример:
# npm run deploy 1.2.0 MAYA-100
```

В результате для каждого qloud-окружения из [конфига](../../.config/ps-deploy.yaml) будет создана и задеплоина версия с новым ресурсом.

- testing: deploy
- prestable: deploy
- production: comitted

Когда работа над тестирование релиза завершена:
- вливаем драфт продакшена в qloud для паблика и корпа
- вливает релизную ветку

profit!

Установить пакет на бету:

```bash
npm run deploy-beta <version> <task_id>
```
