# Паспортный логин

Идентификатор сотрудника (пользователя). К паспортному логину привязывается роль.

{% include [roles-login-standart](../_conref/conref-faq/id-roles/login-standart.md) %}


{% include [roles-idm-login](../_conref/conref-faq/id-roles/idm-login.md) %}


{% note alert %}

IDM выдает доступы как для внутренних, так и для внешних паспортных логинов. Однако рекомендуется использовать внутренние логины («префикс yndx» + «доменный_логин»). На внешние логины распространяется [усиленная политика безопасности (wiki)](https://wiki.yandex-team.ru/intranet/idm/sid67/). После подключения системы к IDM и синхронизации ролей пользователям необходимо сменить пароль на более сложный, а затем обновлять его каждые три месяца.

{% endnote %}

