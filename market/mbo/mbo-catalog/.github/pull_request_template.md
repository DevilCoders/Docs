### Что изменялось:
(Опишите ту коротко, что изменялось в задаче, особенности изменений и т.п.)

### Что нужно обязательно проверить на кодревью:
- наличие тестов: если их нет, должны быть веские основания, если есть - должны проверять важное
- проверьте [изменения в БД, что мы не будем 500-тить при выкладке](https://wiki.yandex-team.ru/market/mbo/sql-migrations/) 
- правильно используется [Spring и конфигурация бинов](https://wiki.yandex-team.ru/Market/MBO/Spring/)

### [Подробнее про то, что смотрим на кодревью](https://wiki.yandex-team.ru/users/yuramalinov/chto-smotrim-na-kod-revju/)

Важно! Нужен не идеальный код, а достаточно хороший. Если код покрыт тестами и не содержит критичных для работоспособности и поддержки кода проблем - вероятно его стоит катить. Т.е. стоит разделять проблемную часть (которую надо точно поправить) и "желательную" часть, где ревьювер считает, что можно ещё улучшить код. В то же время это не значит, что вторую можно всегда игнорировать.


### [Процесс код ревью - как создать PR](https://wiki.yandex-team.ru/market/MBO/code-review-process/)
Прочитайте внимательно, хотя бы один раз :).
