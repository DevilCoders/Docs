# Проблемы с уведомлениями

## Не приходят письма на подтверждение роли {#no-letter}

Письмо на подтверждение роли должно приходить от [robot-tools@yandex-team.ru](robot-tools@yandex-team.ru). Если в [очереди](https://doc.yandex-team.ru/idm/idm-users-guide/concepts/confirm-role.html#queue) вы видите запросы на роли, а письма при этом не получаете, то вы являетесь не единственным подтверждающим.

{% include [confirm-role-notifications-2](../_conref/confirm-role/id-confirm-role/notifications-2.md) %}


## Приходят письма на подтверждение неизвестных ролей  {#letters}

IDM присылает уведомления на подтверждение роли, если: 
- Вы добавлены в список подтверждающих эту роль.
- Вы подписаны на рассылку, которая добавлена в список подтверждающих (при этом прав на подтверждение ролей у вас нет).

Чтобы решить проблему, проверьте адрес получателя в письме от [robot-tools@yandex-team.ru](robot-tools@yandex-team.ru):

- Если указан адрес рассылки, вы можете отписаться от нее на странице [Мои подписки](https://ml.yandex-team.ru/).
- Если указан адрес вашей электронной почты, обратитесь к ответственному [системы](https://idm.yandex-team.ru/systems). Список ответственных перечислен на странице системы. В письме подробно опишите проблему и вставьте скриншот уведомления.

## Приходит слишком много писем на подтверждение роли {#too-many-letters}

На вашу почту может приходить большое количество писем, связанных с запросом, выдачей, отклонением или отзывом ролей. Чтобы сократить количество писем, вы можете:

- [Добавить правило](notifications.md#import_random) перемешивания подтверждающих.
- [Удалить свой адрес](vista.md#email-cc) электронной почты из параметра `email_cc`.

