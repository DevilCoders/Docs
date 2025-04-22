# Bishop configuration engine

[Bishop](https://bishop.mtrs.yandex-team.ru) - система для создания и управления конфигурациями.

В основе лежит шаблонизатор [Jinja2](https://jinja.palletsprojects.com)

Основные возможности системы:
 - Получение конфига по http
 - Валидация синтаксиса конфига (xml/yaml/json)
 - Наличие диффа изменений перед применением новой версии конфига
 - UI для изменения параметров конфигураций

Доступ к системе выдаётся через [IDM](https://idm.yandex-team.ru/).
