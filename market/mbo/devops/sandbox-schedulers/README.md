# Регулярные запуски mbo шедулеров в sandbox

В данном документе описаны все шедулеры MBO в sandbox.
Если вы нашли шедулер, которого нет в этом документе, его стоит добавить сюда.

[Поиск шедулеров в sandbox](https://sandbox.yandex-team.ru/schedulers?tags=mbo&owner=MARKET&limit=20).


## Рассылка ошибок шедулеров

Если при выполнении шедулера произошла ошибка, на рассылку [market-mbo-schedulers-prod@](https://ml.yandex-team.ru/lists/market-mbo-schedulers-prod/)
должно придти уведомление.
Подписка на рассылку доступна всем желающим.


## Шедулеры

Ниже приведен список шедулеров с группировкой по типу:

### Очистка tmp папок YT

#### production
- [//home/market/production/mbo/robot-mbo-stable/java-yt-wrapper/tmp](https://yt.yandex-team.ru/hahn/navigation?path=//home/market/production/mbo/robot-mbo-stable/java-yt-wrapper/tmp) ([Scheduler](https://sandbox.yandex-team.ru/scheduler/42304/view))
- [//home/market/production/mbo/mboc/java-yt-wrapper/tmp](https://yt.yandex-team.ru/hahn/navigation?path=//home/market/production/mbo/mboc/java-yt-wrapper/tmp) ([Scheduler](https://sandbox.yandex-team.ru/scheduler/43575/view))

#### test
- [//home/market/testing/mbo/mboc/java-yt-wrapper/tmp](https://yt.yandex-team.ru/hahn/navigation?contentMode=resources&sort=asc-true,field-modification_time&path=//home/market/testing/mbo/mboc/java-yt-wrapper/tmp) ([Scheduler](https://sandbox.yandex-team.ru/scheduler/44686/view))
- [//home/market/testing/mbo/mboc/java-yt-wrapper/jars](https://yt.yandex-team.ru/hahn/navigation?path=//home/market/testing/mbo/mboc/java-yt-wrapper/jars) ([Scheduler](https://sandbox.yandex-team.ru/scheduler/45044/view))
- [//home/market/testing/mbo/mboc/jars](https://yt.yandex-team.ru/hahn/navigation?path=//home/market/testing/mbo/mboc/jars) ([Scheduler](https://sandbox.yandex-team.ru/scheduler/45040/view))

#### dev
- [//home/market/development/mbo/integration-test/model-storage](https://yt.yandex-team.ru/hahn/navigation?path=//home/market/development/mbo/integration-test/model-storage) ([Sheduler](https://sandbox.yandex-team.ru/scheduler/697705/view))

### Сжатие чанков в YT

### production

- [//home/market/production/mbo/backup](https://yt.yandex-team.ru/hahn/navigation?path=//home/market/production/mbo/backup) ([Sheduler](https://sandbox.yandex-team.ru/scheduler/630454/view))
- [//home/market/production/mbo/mdm/dq/dq_result/ssku](https://yt.yandex-team.ru/hahn/navigation?path=//home/market/production/mbo/mdm/dq/dq_result/ssku) ([Sheduler](https://sandbox.yandex-team.ru/scheduler/698463/view))

## Чеклист заведение шедулера

1. Проверить, что такого шедулера нет
2. Добавить `MBO` в теги шедулера.
3. Добавить рассылку `market-mbo-schedulers-prod@yandex-team.ru` в раздел **Scheduler notification settings** при статусе FAILURE.
4. Добавить рассылку `market-mbo-schedulers-prod@yandex-team.ru` в раздел **Task notification settings** при статусе FAILURE.
5. Если для работы задачи требуются токены, их необходимо добавить на вкладке [Vault](https://sandbox.yandex-team.ru/admin/vault). В качестве owner необходимо прописать sandbox-группу MARKET.

Список уже заведенных токенов:
- [robot-mbo-stable-yt-token](https://sandbox.yandex-team.ru/admin/vault?name=robot-mbo-stable-yt-token&owner=MARKET&limit=20) - YT токен для robot-mbo-stable.
- [robot-mbo-test-yt-token](https://sandbox.yandex-team.ru/admin/vault?name=robot-mbo-test-yt-token&limit=20) - YT токен для robot-mbo-test.
- [robot-mbo-dev-yt-token](https://sandbox.yandex-team.ru/admin/vault?name=robot-mbo-dev-yt-token&limit=20) - YT токен для robot-mbo-dev.
