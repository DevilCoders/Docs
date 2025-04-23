# Вебхуки для работы с гитхабом и CI

### Доступы
Приложение обращается к гитхабу от имени виртуального зомби-пользователя [Подрик Пейн](https://staff.yandex-team.ru/zomb-podrick) через [OAuth](https://wiki.yandex-team.ru/intranet/dev/oauth/).
Доступ для зомбика можно выдать на всю организацию или на отдельный репозиторий.

## Что умеют вебхуки
- Удалять влитую в пулл реквесте ветку.
- Добавлять ссылки на задачи в Стартреке указанные в заголовке пулл реквеста.
- Обновить lama.yaml конфиги.

#### Удаление влитых веток
1. Настроить вебхук на адрес:
```
https://podrick.c.maps.yandex-team.ru/github/delete-merged-pr-branch
```
2. В настройках вебхука выбрать **Let me select individual events.** и выбрать событие **Pull request.**
3. Не забыть про доступы `zomb-podrick` к репозиторию.

При влитии пулл-реквеста удаляются все ветки, кроме тех, что начинаются с `protected`.

#### Ссылка на задачи в Стартреке
1. Настроить вебхук на адрес:
```
https://podrick.c.maps.yandex-team.ru/github/link-to-st
```
2. В настройках вебхука выбрать **Let me select individual events.** и выбрать событие **Pull request.**
3. Не забыть про доступы `zomb-podrick` к репозиторию.

Если задача не указана в заголовке PR - проверка не будет добавлена.

#### Обновление lama.yaml конфигов
1. Настроить вебхук на адрес:
```
https://podrick.c.maps.yandex-team.ru/github/lama-webhook
```
2. В настройках вебхука выбрать **Just the push event.**

При обновлении `lama.yaml` конфига в default-ветке репозитория (`master`/`dev`), он опубликуется [автоматически](https://github.yandex-team.ru/maps/infra/tree/master/packages/lama-webhook-parser#lama-webhook-parser).

Если ваш репозиторий находится в организации [maps](https://github.yandex-team.ru/orgs/maps), добавлять вебхук не нужно. Он включен на уровне организации.
