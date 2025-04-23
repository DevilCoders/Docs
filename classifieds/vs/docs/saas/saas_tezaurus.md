**[Фактор](https://wiki.yandex-team.ru/jandekspoisk/saas/factorsinfo/)** - _key-value_ пара, используемая в полиноме/модели ранжирования. Различают следующие типы факторов:
- статический фактор -  зависит только от самого документа 
- пользовательский фактор - задается в запросе
- динамический фактор - предустановленная функция от документа и запроса, может быть посчитана для [текстовых атрибутов](https://wiki.yandex-team.ru/jandekspoisk/saas/factorsinfo/webdynamic/?from=%2Fjandekspoisk%2Fsaas%2Fquality%2Ffactors%2Fweb_dynamic%2F)
  и для [служебных атрибутов](https://wiki.yandex-team.ru/jandekspoisk/saas/factorsinfo/rtydynamic/?from=%2Fjandekspoisk%2Fsaas%2Fquality%2Ffactors%2Frty_dynamic%2F), например, времени жизни документа

**Свойство(Property)** - атрибут, хранимый в индексе. Не доступен для поиска

**[Поисковый атрибут](https://wiki.yandex-team.ru/jandekspoisk/saas/SearchAttrs/)** - литеральный или целочисленный атрибут, доступный для поиска по совпадению. 

**Группировочный атрибут** - частный случай поискового атрибута. [Специальным образом](https://wiki.yandex-team.ru/jandekspoisk/saas/GroupAttrs/) проиндексированный литеральный или целочисленный атрибут, над которым возможны следующие операции:
 - сортировка
 - подсчет статистик: фасеты, min-max и  т.д.
 - поиск по диапазону

**[Фасеты](https://wiki.yandex-team.ru/jandekspoisk/SaaS/stat/)** -  подсчет статистики значений по некоторому **группировочному** атрибуту для всех документов, попавших в выборку.
Выхлоп состоит из пар вида <значение атрибута документа>: <количество документов в выдаче c  данным значение>

**[Бустинг (Refine)](https://wiki.yandex-team.ru/JandeksPoisk/KachestvoPoiska/Basesearch/RefineFactor/)** - состоит из пары _<имя фактора>: <целевое значение>_ и условия. Если для документа условие верно, то указанному фактору этого документа будет присвоено целевое значение.

**[Прунинг](https://doc.yandex-team.ru/Search/saas/saas-overview/concepts/how-search-works.html?lang=ru)** -  динамически прекращаем обработку запроса, при накоплении такого количества документов (в ответе каждого шарда)

