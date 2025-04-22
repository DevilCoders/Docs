# Автоматика для почтовых стендов в Y.Deploy <img src="https://yd.yandex-team.ru/favicon_32x32.png" width="20" valign="middle">

Почтовые стенды устроены из несколько компонент (homer, webapi, liza, quinn, etc) и nginx над ними.

Автоматика запускается, когда готовы все джобы сборки тестовых ресурсов компонент в трендбоксе. Далее она проверяет, что в Sandbox есть все нужные ресурсы в статусе `READY`.

Локально собирает спеки для деплоя для всех компонент по рецепту `qa` (или `corp-qa` для корпа).

Для финальной спеки берет только `DU: nginx` и `DU` для изменившихся компонент.

Меняет настройки replica set на `MCRS` с одним случайным (или ранее опубликованным) ДЦ, количество подов проставляет `1`. ДЦ можно передать параметром `location`.

Меняет в спеке слои `front_app` на новые ресурсы.

Публикует спеку в Y.Deploy.

Добавляет комментарий в Стартрек и обновляет поле `testUrl` для тикета, если указан в заголовке пулл-реквеста.

В итоге имеем в Y.Deploy stage с нужными компонентами в отдельных деплой-юнитах + nginx над ними, который для остальных компонент ходит в коммунальные стейджи (`mail_liza_qa`, `mail_webapi_qa`, etc).


## Как попасть на стенд

Пример: `stageId: mail_frontend_pr-123` — https://pr-123.qa.mail.yandex.ru (или другой TLD).

Пример: `stageId: mail_frontend_pr-123-corp` — https://pr-123-corp.qa.mail.yandex-team.ru.

Пример: `stageId: mail_frontend_liza-rc-33-0` — https://liza-rc-33-0.qa.mail.yandex.ru.

Пример: `stageId: mail_frontend_liza-rc-33-0-corp` — https://liza-rc-33-0-corp.qa.mail.yandex.ru.

Если префикса в `standId` отличается от `mail_frontend_`, стенд не будет доступен.

После префикса должны быть буквы, цифры и `-`.


## Пример запуска CLI

```bash
node ./tools/ci/mail-deploy/deploy-stage.js '{"stageId": "mail_frontend_ub1","components":{"homer":{"front_app":"sbr:2732245011"}}}'

node ./tools/ci/mail-deploy/deploy-stage.js '{"isCorp":true,"stageId": "mail_frontend_ubcorp2","components":{"homer":{"front_app":"sbr:2732245011"},"liza":{"front_app":"sbr:2777788775"}}}'
```


## Перенос стендов на случай учений

```bash
./move-stages.js

# Syntax:
#     move-stages.js [stageId] FROM TO
#
# Available locations:
#     iva sas myt
#
# Example:
#     move-stages.js iva sas # will move all pr-* stages
#     move-stages.js pr-123-corp sas iva # will move pr-123-corp only

./tools/ci/mail-deploy/move-stages.js iva sas

# or

./tools/ci/mail-deploy/move-stages.js pr-123-corp iva sas
```
