# Тест jobHasOperationDoc (у джобы есть эксплуатационная документация)

Как разбираться с тестом `MonitorDocsTest/jobHasOperationDoc`.

## Теория

Чтобы дежурному по продакшену было проще разбираться с мониторингами, мы пишем эксплуатационную документацию на каждую джобу.  
Чтобы не забывать писать эксплуатационные доки, у нас есть тест, который проверяет их наличие (ищет файл с именем как у джобы в `market/billing/docs/reference/jobs/list/`).


## Когда тест падает

Вероятно, ты добавил новую джобу или переименовал старую и не добавил/не переименовал эксплуатационную документацию. 

## Что делать, если тест упал

Скопируй шаблон <https://a.yandex-team.ru/arc/trunk/arcadia/market/billing/docs/reference/jobs/list/template.md>  
в файл `market/billing/docs/reference/jobs/list/<имя джобы>.md`  
Заполни для своей джобы.  
Рекомендации, как писать полезную эксплуатационную документацию: [{#T}](../guide/dev/jobs-operation-doc.md)

Если еще никогда не отлаживал документацию локально: [{#T}](../guide/how-to-write-documentation.md).

Закоммить документацию.

Успех! Еще одна джоба получила эксплуатационную документацию.

{% note info %}

Если совершенно невозможно написать эксплуатационную документацию сразу: впиши джобу в список исключений.  
Файл <https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/test/java/ru/yandex/market/billing/monitor/model/MonitorDocsTest.java>, список `KNOWN_JOBS_WITHOUT_DOCS`.

{% endnote %}

## Ссылки

* [{#T}](../guide/dev/jobs-operation-doc.md)
* [{#T}](../guide/how-to-write-documentation.md)
* <https://a.yandex-team.ru/arc/trunk/arcadia/market/billing/docs/reference/jobs/list/template.md> -- Шаблон эксплуатационной доки в Аркануме
* <https://docs.yandex-team.ru/market-billing/reference/jobs/list/template> -- Шаблон эксплуатационной доки в документации

