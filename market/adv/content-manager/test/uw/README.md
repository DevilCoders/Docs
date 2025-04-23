## Предварительно

Делается только один раз, если до этого не приходилось работать с YT через python.

1. Запросить права на **read,write,remove**
   в [content_manager на zeno](https://yt.yandex-team.ru/zeno/navigation?navmode=acl&path=//home/market/testing/market-adv-money/content-manager/moderation)
   .
2. Поставить ```python3```.
3. Выполнить ```pip install -i https://pypi.yandex-team.ru/simple/ yandex-yt```.
4. Выполнить ```pip install -i https://pypi.yandex-team.ru/simple/ yandex-yt-yson-bindings```.

## Эмуляция

1. В ```script/readTable.py``` и ```script/createTable.py``` указать в ```task_id``` идентификатор задачи, по которой
   будем завершать процесс модерации.
2. Запустить ```python3 script/readTable.py```.
3. Взять результаты выполнения предыдущего скрипта, заполнить в них дополнительно ```result_status``` (True или False)
   и ```result_info``` - dictionary из значений, например: ```{'TEST': 'Wrong data'}```.
4. Запустить ```python3 script/createTable.py```.
5. Подождать около 15 минут пока данные доедут до ```content-manager```.

## Как запустить quartz задачу, не дожидаясь времени ее выполнения

В тестинге есть возможность запустить задачу
через [API](https://a.yandex-team.ru/arc/trunk/arcadia/market/jlibrary/tms-core-quartz2/tms-web-quartz2/README.md), не
дожидаясь момента, когда она будет запущена. Чтобы запустить job получение результатов модерации, можно отправить
следующий запрос:

```shell
curl -v -H "Content-Type: application/json" -X POST 'http://adv-content-manager.tst.vs.market.yandex.net/tms/jobs/run' -d '{"jobName": "tmsModerationTaskSentToModeratedExecutor"}'
```

Порядок выполнения job в процессе модерации, которые можно запустить принудительно:

1. ```tmsModerationTaskCreatedToSentExecutor``` - отправка на модерацию.
2. ```tmsModerationTaskSentToModeratedExecutor``` - получение результатов модерации.
3. ```tmsModerationTaskModeratedToPublishedExecutor``` - публикация шаблона.
4. ```tmsModerationTaskPublishedToEndedExecutor``` - отправка нотификации по шаблону.

## Информация по заполнению result_info

[Ключи ошибок модерации](https://wiki.yandex-team.ru/advshop/shop-in-shop/intteraction-with-uw/#kljuchioshibokmoderaciiizpoljaresultinfo)
