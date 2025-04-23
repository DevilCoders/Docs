## Проект для документирования схемы БД в вики
Данный проект позволяет документировать схемы БД (таблицы, колонки, индексы и тд) в Wiki, после чего они попадают под индексацию и становятся доступны при поиске. 

### Использование
Для старта процесса документации надо использовать gradle-таску dbdoc с несколькими аргументами:
* schemas - список схем, которые будут документированы.
* target - ссылка на родительскую страницу в Wiki, на которой будет сгенерирован виджет с ссылками на страницы с описанием схем.
* database - jdbc-like URL до БД
* login - логин в бд
* password - пароль в бд
* wikiUploadToken - токен вики робота

Документация: https://wiki.yandex-team.ru/MBI/Development/dbdocs/

Team-city задача: https://teamcity.yandex-team.ru/viewType.html?buildTypeId=Market_Mbi_Documentation_DbSchemaDocumentation

Сейчас выкладывает документацию сюда: https://wiki.yandex-team.ru/Market/InformationArchitecture/billing/DBStructure/
