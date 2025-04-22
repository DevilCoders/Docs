## Direct upload tanker translations

Задача для выгрузки переводов Java сервисов Директа в Танкер.

### Input parameters

1. Arcadia url - путь до репозитория аркадии
2. Path to script - путь до скрипта для загрузки переводов
3. Package to build path - путь до пакета, который реализует клиент Juggler'a
4. Vault User - юзер от которого будут записи из Секретницы Sandbox'а.
5. Tanker token vault name - имя записи в [секретнице Sandbox'а](https://sandbox.yandex-team.ru/admin/vault), которая содержит токен для работы с Танкером.
6. Enable Juggler Monitoring - включить, в случае успешного завершения задания, отправку нотификации в Juggler.
7. Juggler event host - хост Juggler события
8. Juggler event service - имя метрики Juggler события

#### How task works

1. Создает копию аркадии
2. В ней собрает пакет <i>@Package to build path</i> (direct/apps/direct-tanker-tool)
3. Запускает скрипт для выгрузки переводов в Танкер <i>@Path to script</i> (direct/bin/tanker.sh)<br/>
В скрипт передаются: команда sandbox_upload, путь до утилиты ya, токен для загрузки переводов
4. Если включена опция отправки событий в Juggler, при успешном выполнении предыдущих пунктов, отправляет событие, что переводы загружены.