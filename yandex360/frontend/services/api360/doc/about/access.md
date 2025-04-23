# Доступ к API

Все запросы к API выполняются к хосту `https://api360.yandex.net/`.

Яндекс 360 для бизнеса авторизует приложения с помощью [OAuth-токенов](https://yandex.ru/dev/oauth/doc/dg/concepts/ya-oauth-intro.html). Чтобы получить OAuth-токен:

1. [Авторизуйтесь на Яндексе](https://passport.yandex.ru). Укажите логин и пароль администратора организации, от имени которого будут выполняться запросы к API.

1. [Зарегистрируйте](https://yandex.ru/dev/id/doc/dg/oauth/tasks/register-client.html) приложение на OAuth-сервере Яндекса. При регистрации укажите необходимые права доступа.

   На текущий момент в API поддерживаются следующие права:

   * Чтение данных о подразделениях (`directory:read_departments`);
   * Чтение данных о группах (`directory:read_groups`);
   * Чтение данных о сотрудниках (`directory:read_users`);
   * Управление подразделениями (`directory:write_departments`);
   * Управление группами (`directory:write_groups`);
   * Управление сотрудниками (`directory:write_users`).

1. Реализуйте получение OAuth-токена одним из [доступных способов](https://yandex.ru/dev/id/doc/dg/oauth/concepts/about.html).

   Токены для отладки приложения можно получать [вручную](https://yandex.ru/dev/id/doc/dg/oauth/tasks/get-oauth-token.html).

Полученный токен следует передавать в HTTP-заголовке `Authorization` при каждом вызове API, указывая тип токена перед его значением:

```bash
--header 'Authorization: OAuth <OAuth-токен>'
```

Подробнее об OAuth-авторизации читайте в разделе [Протокол OAuth 2.0](https://yandex.ru/dev/id/doc/dg/oauth/concepts/about.html) документа [Вход через Яндекс. Руководство разработчика](https://yandex.ru/dev/id/doc/dg/index.html).
