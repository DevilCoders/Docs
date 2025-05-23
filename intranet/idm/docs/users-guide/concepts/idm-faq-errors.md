# Ошибки

## Не могу понять, что означает ошибка {#unknown-error}

Ошибки при запросе роли в большинстве случаев исходят от самой системы, а не от IDM. Названия ошибок самостоятельно задают ответственные за [систему](https://doc.yandex-team.ru/idm/idm-guide/entities/system.md).

Чтобы расшифровать ошибку, обратите внимание на ее текст:

- Если текст содержит выражение «PluginFatalError», обратитесь к владельцу системы. Список систем, подключенных к IDM, представлен на странице [IDM. Все системы](https://idm.yandex-team.ru/systems).
- Если текст содержит только код ошибки, напишите письмо на рассылку [tools@yandex-team.ru](tools@yandex-team.ru).

## Ошибка «login <паспортный_логин> already have role: <название_роли>» {#already-have-role}

Ошибка может возникнуть в следующих случаях:

- Если вы пытаетесь запросить в Директе вторую роль на тот же паспортный логин.
    Например, ошибка: "login yuliya-k already have role: manager" означает, что у сотрудника уже есть роль Менеджер, привязанная к логину yuliya-k.
    
    Чтобы решить проблему, запросите роль заново на другой логин.
    
- Если в Директе на ваш паспортный логин все еще записана ранее отозванная роль.
    Чтобы решить проблему, напишите запрос на удаление отозванной роли в службу поддержки Директа: [direct@yandex-team.ru](mailto:direct@yandex-team.ru).
    

## Ошибка «Role with such system_specific already exists» {#already-exists}

Ошибка может возникнуть, если вы пытаетесь запросить в Маркете вторую роль на тот же паспортный логин.

Чтобы решить проблему, запросите роль заново на другой логин.

## Ошибка «Не удалось добавить роль в систему» {#cant-add-role}

В некоторых системах при запросе роли необходимо создать новый логин. После отправки запроса на вашу электронную почту придет письмо со ссылкой для установки нового пароля. Установка нового пароля необходима для завершения регистрации логина. Ссылка действительна в течение одной недели.
Если логин не зарегистрировать, после подтверждения роли возникнет ошибка «Не удалось добавить роль в систему». 
![](../image/role-error.png)

Чтобы решить проблему: 
1. Найдите письмо от **Яндекс.Паспорт**.
1. Перейдите по ссылке из письма.
1. Завершите регистрацию логина, если срок действия ссылки не истек. В противном случае напишите на рассылку [sp-passport@yandex-team.ru](mailto:sp-passport@yandex-team.ru).
    После регистрации логина заново запросите на него роль.

