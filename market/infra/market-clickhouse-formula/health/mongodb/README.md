HowTow
======

Формула в режиме обкатки.

Формула написана для первичной наливки и настройки репликасета без настройки самой реплики.
Она умеет готовить одинаковый для всех, но в тоже время уникальный в рамках одного запуска ключик для авторизации монг между собой.

Формула запускается через орчестру по пути: satl://orch/mongodb-health-test.sls
Там же можно посмотреть пример для создания продового профиля наливки.

После применения формул не забудьте перезагрузить машины, что бы настройки в /etc/hostname вступили в силу, иначе с настройкой реплики будут проблемы.

После настройки репликации, включите авторизацию в конфигах, заведите пользователя в монге и перезагрузите монгу еще раз. Если хочется, вы можете завтоматизировать и это действие.

