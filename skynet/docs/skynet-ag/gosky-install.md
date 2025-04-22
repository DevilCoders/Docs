# Утилита gosky

{% note warning %}

Версия утилиты gosky должна быть не ниже 2.2.

{% endnote %}

Установка и последующая поддержка актуальной версии {{ serviceName }} на Linux-серверах обеспечивается утилитой gosky. Сведения о [требуемой версии](skynet-version.md) {{ serviceName }} и [конфигурации сервисов](configuration.md) запрашиваются в {{ deploy-and-configService }}.

Установите утилиту gosky на сервере. Установочный пакет `yandex-gosky` доступен в репозитории:

```
deb http://common.dist.yandex.ru/common stable/all/
```

После установки автоматически выполняется первичный запуск утилиты gosky.

Пакет содержит файл `crontab`, который обеспечивает в дальнейшем запуск утилиты gosky с заданной периодичностью. При запуске утилита проверяет актуальность и, при необходимости, обновляет:

* [версию {{ serviceName }}](skynet-version.md);
* [конфигурации сервисов](services-configuration.md).

## Узнайте больше

* [Процедура обновления версии Skynet (Вики)](https://wiki.yandex-team.ru/Skynet/HowToUpdate/)
