# Все вопросы на одной странице

#|
||**Роли**

[Не могу перезапросить роль](#cant-recall)

[Сотрудник покинул группу, однако роль все еще активна](#left-group)

[Не могу отозвать роль](#cant-delete)

[Не могу найти ранее выданную роль](#cant-find)

[Кнопка «Перезапросить» неактивна](#inactive-button)

[В тестинге отозвались все роли](#testing-role)

[Не могу понять, какие роли у группы отзовутся после организационных изменений](#org-changes)

[Поменять политику системы в отношении перезапроса ролей при смене сотрудником подразделения](#change-politic) | **Уведомления**

[Не приходят письма на подтверждение роли](#dont-have-notifications)

[Приходят письма на подтверждение неизвестных ролей](#unknown-notifications)

[Приходит слишком много писем на подтверждение роли](#too-much-notifications)||
||**Ошибки**

[Сообщение «Внимание! Следующие системы сломаны и временно недоступны для IDM»](#system-errors) ||
|#


## Проблемы с ролями {#roles}

### Не могу перезапросить роль {#reorder-role}

Если при попытке выполнить действие с [ролью](https://doc.yandex-team.ru/idm/idm-guide/entities/user-role.html) (например, перезапросить роль) вы получаете сообщение «Для этой роли вы не можете выполнить действие», напишите на рассылку [tools@yandex-team.ru](tools@yandex-team.ru).

Ошибка может возникнуть, если в [workflow](https://doc.yandex-team.ru/idm/idm-guide/entities/workflow.html) для пользователя прописан запрет на запрос доступов (например, если сотрудник является внешним консультантом). Обратитесь к владельцу системы.

### Не могу отозвать роль {#close-role}

Если при попытке отозвать роль вы получаете сообщение «Для этой роли вы не можете выполнить действие», скорее всего, вы пытаетесь отозвать одну из следующих ролей:

- Персональную групповую роль.
    Чтобы отозвать групповую роль, необходимо покинуть группу. По истечении семи дней роль автоматически отзовется.
    
- Связанную роль.
    Чтобы отозвать связанную роль, необходимо отозвать основную роль.
    
- Удаленную роль (или систему).
    Чтобы узнать, есть ли аналогичная роль, обратитесь к владельцу системы.
    

### Не могу найти ранее выданную роль {#not-found}

Скорее всего, роль была отозвана. Отозванные роли можно [перезапросить](https://doc.yandex-team.ru/idm/idm-users-guide/concepts/query-role.html#recall-role).

### Кнопка «Перезапросить» неактивна {#recall}

[Склонируйте](https://doc.yandex-team.ru/idm/idm-users-guide/concepts/query-role.html#clone-role) нужные роли.

### В тестинге отозвались все роли {#testing-role}

В тестинге IDM все действия над ролями запускаются принудительно (например, перевод роли в другое состояние). При этом IDM не отправляет ответственному за систему уведомления о событиях с ролью.

Ответственный может перезапросить роль, однако тестинг IDM не рекомендуется использовать как стабильную систему управления доступом. Для постоянной и стабильной работы [подключите вашу систему](add-system-to-idm.md) к продакшн IDM.

### Не могу понять, какие роли у группы отзовутся после организационных изменений {#group-roles}

Напишите на рассылку [tools@yandex-team.ru](tools@yandex-team.ru).

### Как поменять политику системы в отношении перезапроса ролей при смене сотрудником подразделения {#politics}

При подключении системы к IDM можно указать правила (политики), согласно которым система будет работать. Подробное описание политик см. в разделе [[!TITLE add-system-common.md]](add-system-common.md) документа [IDM. Руководство владельца системы](../index.md).

<!-- add-system-common.md -->

Чтобы поменять политику, напишите на рассылку [tools@yandex-team.ru](tools@yandex-team.ru).

### Сотрудник покинул группу, однако роль все еще активна {#left-group}

Роль выдается на группу, в которой состоит пользователь. Все участники группы получают связанную персональную роль. Если пользователь покидает группу, роль автоматически отзывается по истечении семи дней.


## Проблемы с уведомлениями {#notifications}

### Не приходят письма на подтверждение роли {#no-letter}

Письмо на подтверждение роли должно приходить от [robot-tools@yandex-team.ru](robot-tools@yandex-team.ru). Если в [очереди](https://doc.yandex-team.ru/idm/idm-users-guide/concepts/confirm-role.html#queue) вы видите запросы на роли, а письма при этом не получаете, то вы являетесь не единственным подтверждающим.

{% include [confirm-role-notifications-2](../_conref/confirm-role/id-confirm-role/notifications-2.md) %}


### Приходят письма на подтверждение неизвестных ролей  {#letters}

IDM присылает уведомления на подтверждение роли, если: 
- Вы добавлены в список подтверждающих эту роль.
- Вы подписаны на рассылку, которая добавлена в список подтверждающих (при этом прав на подтверждение ролей у вас нет).

Чтобы решить проблему, проверьте адрес получателя в письме от [robot-tools@yandex-team.ru](robot-tools@yandex-team.ru):

- Если указан адрес рассылки, вы можете отписаться от нее на странице [Мои подписки](https://ml.yandex-team.ru/).
- Если указан адрес вашей электронной почты, обратитесь к ответственному [системы](https://idm.yandex-team.ru/systems). Список ответственных перечислен на странице системы. В письме подробно опишите проблему и вставьте скриншот уведомления.

### Приходит слишком много писем на подтверждение роли {#too-many-letters}

На вашу почту может приходить большое количество писем, связанных с запросом, выдачей, отклонением или отзывом ролей. Чтобы сократить количество писем, вы можете:

- [Добавить правило](notifications.md#import_random) перемешивания подтверждающих.
- [Удалить свой адрес](vista.md#email-cc) электронной почты из параметра `email_cc`.


## Ошибки {#errors}

### Сообщение «Внимание! Следующие системы сломаны и временно недоступны для IDM» {#interrupt}

Сообщение появляется при появлении [неконсистентностей](https://doc.yandex-team.ru/idm/idm-guide/entities/nonconsist.html). Способ решения проблемы зависит от среды, в которой оно появилось. 

{% list tabs %}

- Сообщение появилось в продакшн

  Решить проблему может только ответственный за систему. Список ответственных перечислен на странице системы.

  ![](../image/controllers.png)

  Ответственный должен проверить список неконсистентностей на странице системы: 
  - Если расхождение в таблицах ролей IDM и системы ожидаемое, нажать кнопку **Включить**.
  - В противном случае [воспользуйтесь](close-neconsist.md) одним из способов разрешения неконсистентностей.

- Сообщение появилось в тестинге

  Чтобы решить проблему, нажмите кнопку **Включить** для нужной системы.

  ![](../image/system-error.png)

  Тестинг IDM не рекомендуется использовать как стабильную систему управления доступом. Для постоянной и стабильной работы [подключите вашу систему](add-system-to-idm.md) к продакшн IDM.

{% endlist %}
