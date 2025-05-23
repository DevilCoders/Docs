## Настройки аудитории в админке коммуникаций Go

Это - альтернативный план для настройки аудитории через CRM. 
Пока не началась интеграция, реализуем необходимый минимум в нашей админке 
и даём доступ маркетологам к странице с настройками.

Требуемый минимум:

1. Показать фильтры в админке коммуникаций. Делаем ручку, предложенную для 
CRM, но вызываем у нас. Заодно обкатываем api, + решение переиспользуемое. 
На фронте поддерживаем ручку.
2. Прокидываем с фронта фильтры в эксперимент, привязанный к коммуникации, 
или заводим новый. На странице для маркетологов ссылки на эксперимент нет, но 
она остаётся на обычной странице публикации.
3. Ограничение на создание коммуникаций (объектов на карте, возможно, ещё каких-то) по приоритетам. 
Не должно быть возможности создать коммуникацию с высоким приоритетом, 
если уже есть с приоритетом 1 (здесь уточнить продуктовые требования).
4. Починенная тестовая публикация.

После этого доступ к страничке можно будет давать маркетологам, 
публиковать любые объекты можно будет через нашу админку.

Делаем на этой страничке в админке:

![](../img/admin_publish_fullscreen.png)

Заодно проверяем, работает ли она, чиним, если нет, и актуализируем.
