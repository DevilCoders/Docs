# Файлы сервиса

Каждый экземпляр сервиса (инстанс) на хосте распаковывается в каталог с набором файлов. Список файлов задается в разделе Files. Файлы скачиваются либо по HTTP(S), либо по rbtorrent: (skynet). Внутри контейнера файл сохраняется под именем из поля `Local Path`. Внимание: нельзя сохранять файлы в подкаталоги, все файлы будут скачаны в один каталог.

##  Статичный текстовый файл {#static-file}
Можно создавать и редактировать простые текстовые файлы прямо в интерфейсе Няни. Файл будет сохранён в кодировке `UTF-8`.
![static](https://jing.yandex-team.ru/files/sshipkov/service_files_static.f7797ec.png)

## Ресурс с одним файлом из Sandbox {#sandbox-file}

Нужно указать идентификатор ресурса из Sandbox'a или url-адрес страницы с этим ресурсом. Предпочтительный вариант для распространения файлов, т.к. протокол Torrent внутри Sandbox'a оптимизирует нагрузку на сеть.

Можно настроить [интеграцию sandbox + nanny](../how-to/sandbox-integration.md), тогда при создании новой версии ресурса в sandbox, nanny будет автоматически обновлять версию ресурса.
![files](https://jing.yandex-team.ru/files/sshipkov/Files__slonnn-yp-test-xxx__Services__Home_2018-03-30_01-56-15.708189d.png)

{% note warning %}

При первой выкладке sandbox-ресурса Nanny закеширует его rbtorrent в собственном хранилище данных. При последующих выкладках Nanny не будет извлекать метаинформацию об этом ресурсе из sandbox [мотивация)]((https://st.yandex-team.ru/SPI-8020). Отсюда возникает side effect: при удалении ресурса из sandbox его выкладка в Nanny продолжит работать.

{% endnote %}

## Файл доступный по URL'у {#url-file}

Можно указать URL файла для http(s) или для rbtorrent протоколов. Не рекомендуем использовать http(s) для больших сервисов т.к. при скачивании по URL нельзя проверить целостность файла из-за отсутствия контрольных сумм. Плюс скачивание происходит не так эффективно, как при скачивании по Torrent-протоколу из Sandbox, т.к. скачивание на много хостов ведется всего с одного сервера.

Причины скачивать файл по URL:

- протестировать какую-либо тестовую сборку, доступную только с разработческой машины через skynet;
- файлы раздаются сторонним сервисом, поддерживающим только http.

![url-file](https://jing.yandex-team.ru/files/sshipkov/Files__slonnn-yp-test-xxx__Services__Home_2018-03-30_01-58-18.5672313.png)

## Расширенные свойства (ISS properties) {#file-iss-properties}
Доступные свойства:

* `Is dynamic` – является ли ресурс динамическим [подробнее](https://wiki.yandex-team.ru/iss3/Specifications/configuration/resource/#dinamicheskijjresurs)
* `Download speed limit` – ограничение скорости скачивания ресурса [подробнее](https://wiki.yandex-team.ru/iss3/specifications/configuration/resource/#resurs)
* `Time between resource check` – период перепроверки контрольной суммы ресурса. 0d0h0m – проверить 1 раз после скачивания. Другое значение задаёт периодичность [подробнее](https://wiki.yandex-team.ru/iss3/specifications/configuration/resource/#resurs)
* `Storage for resource` – место хранения ресурса [подробнее](../how-to/storage/move-to-ssd.md)
* `Is juggler bundle` – является ли ресурс juggler bundle [подробнее](../how-to/monitoring/juggler-subagent.md)

![iss](https://jing.yandex-team.ru/files/sshipkov/nanny_iss_properties_place.828925d.png)
![iss](https://jing.yandex-team.ru/files/sshipkov/nanny_iss_properties.0ae7af3.png)

## InstanceСtl

Непосредственно на хосте управлением контейнерами занимается супервизор. В qloud это [qloud-init](https://wiki.yandex-team.ru/qloud/doc/qloud-init/), в Няне это [instancectl](https://wiki.yandex-team.ru/JandeksPoisk/Sepe/instancectl/).

Когда iss-агент готовится запускать контейнер, на самом деле сначала запускается супервизор, который читает файл конфигурации и дальше сам супервизор уже запускает приложения из конфигурации Няни внутри контейнера. Супервизор отвечает за инициализацию контейнеров, установку системных свойств, взаимодействие с iss-агентом, занимается контролем работы контейнеров. В зависимости от версии instancectl меняется и поведение самого контейнера.

При создании сервиса автоматически устанавливается последняя stable-версия instancectl. Чтобы изменить её, нужно открыть `Instance Spec` сервиса и выбрать соответствующую версию.
![select.png](https://jing.yandex-team.ru/files/sshipkov/select.1dce449.png)

Есть два способа сформировать файл с описанием контейнера для instancectl:

1. loop.conf. Устаревший plain-text формат описания. Формат файла loop.conf [описан здесь](https://wiki.yandex-team.ru/jandekspoisk/sepe/instancectl/).
1. [instancespec](../how-to/structured-instancectl-config.md). Текущий формат описания контейнеров. В нем можно описать поведение контейнера через веб-интерфейс.
![spec](https://jing.yandex-team.ru/files/sshipkov/Instance_Spec__slonnn-yp-test-golovan2__Services__Home_2018-04-02_01-26-54.e7db6d1.png)

Также в новых сервисах автоматически настроено оповещение о новых версиях InstanceCtl. Подробнее о нём можно почитать [тут](instance-ctl/versioned-instancectl.md).
