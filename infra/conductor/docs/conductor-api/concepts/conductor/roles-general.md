# Доступы и роли

Доступ к {{ serviceName }}у осуществляется по доменным логину и паролю. Если вы уже авторизованы на внутреннем [Я.Паспорте](https://passport.yandex-team.ru), доступ предоставляется автоматически.

Все пользователи {{ serviceName }}а обладают одной из [базовых ролей](access.md):

- [Passerby](access.md#passerby), <q>Прохожий</q>.
- [Audience](access.md#audience), <q>Зритель</q>.
- [Musician](access.md#musician), <q>Музыкант</q>.
- [Soloist](access.md#soloist), <q>Солист</q>.
- [Conductor](access.md#conductor), <q>Дирижер</q>.

Базовая роль определяет права доступа пользователя по отношению к [объектам](package-props.md#package-props) {{ serviceName }}а.

Кроме базовых ролей, пользователи могут обладать [ролями в рамках проектов](./task/project-roles.md#project-roles):

- [администратор проекта](./task/project-roles.md#project-admin);
- [администратор группы хостов](./task/project-roles.md#group-admin);
- [одобрятор](./task/project-roles.md#approver).

Роли по проектам определяют возможности пользователей в рамках конкретного проекта.
