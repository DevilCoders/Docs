# Workflow

Различные сценарии, выполняемые в системе.

В workflow обязательно должен быть определен список подтверждающих роли (`approvers`). Список может быть либо пустым, либо содержать логины сотрудников, от которых требуется получить подтверждение. Роль считается подтвержденной, если получено одобрение хотя бы от одного сотрудника из списка.

Workflow описывается на языке Python. Изменения в workflow вносит либо сотрудник со стороны системы, либо сотрудник [Службы информационной безопасности](https://staff.yandex-team.ru/departments/yandex_mnt_security/). Полное описание всех переменных и функций представлено в разделе [Справочник workflow](https://doc.yandex-team.ru/idm/idm-owners-guide/concepts/workflow-list.md) документа [IDM. Руководство владельца системы](https://doc.yandex-team.ru/idm/idm-owners-guide/idm-owners-guide.ditamap#role-tree).

#### Примеры сценариев

- [получать подтверждение](https://doc.yandex-team.ru/idm/idm-owners-guide/concepts/add-confirmer.html) сотрудника или нескольких сотрудников при запросе роли;
- [отправлять уведомления](https://doc.yandex-team.ru/idm/idm-owners-guide/concepts/notifications.html) сотрудникам, подтверждающим роль;
- [показывать предупреждение](https://doc.yandex-team.ru/idm/idm-owners-guide/concepts/vista.html#warning) при запросе роли;
- [учитывать роли](https://doc.yandex-team.ru/idm/idm-owners-guide/concepts/vista.html#has_role) пользователя в других системах.

