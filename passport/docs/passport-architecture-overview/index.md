# Общая схема архитектуры

Яндекс.Паспорт и сопутствующие внутренние и внешние сервисы объединяются в единую систему авторизации. Система авторизации обеспечивает аутентификацию и авторизацию пользователей Яндекса, а также хранят личные данные пользователей.

Сервисам Яндекса система позволяет:
- выдавать и проверять аутентификационные данные (куки для доменов Яндекса, OAuth-токены, пароли);
- отправлять информационные и проверочные SMS;
- управлять учетными записями пользователей и получать доступ к их данным (ФИО, электронные адреса, социальные профили и т. д.);
- хранить личные данные пользователей.


Общая схема системы авторизации представлена ниже. Помимо схемы в документе приведены функциональные описания отдельных компонентов системы — [Яндекс.Паспорта](concepts/passport.md) (как веб-сервиса), [Социализма](concepts/social.md) и [остальных подсистем](concepts/the-rest.md).

{% note info %}

Чтобы перейти к описанию подсистемы, кликните на ней на схеме.

{% endnote %}

![passport-arch](_assets/passport-arch.png "Схема архитектуры")


