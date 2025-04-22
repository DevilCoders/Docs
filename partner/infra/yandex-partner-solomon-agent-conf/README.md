The Debian Package yandex-partner-solomon-agent-conf
----------------------------------------

Пакет с конфигурационными файлами для solomon-agent Партнёрского интерфейса РСЯ.

 -- Evgenii Maksimenko <evmaksimenko@yandex-team.ru>

----------------------------------------

configs/partner-main.conf - основная конфигурация для solomon-agent

configs/sys.conf - подключаемая конфигурация для сбора системных метрик

upstart/solomon-agent.conf - upstart скрипт

--------------
Сборка и выкладка

{% note alert %}

Пакет собранный из этого кода под precise не поставится под bionic и наобарот

Поэтому путать нельзя - на какой версии Ubuntu собираете, в такой репозиторий и нужно заливать

{% endnote %}

Подробно тут:
 - [Сборка пакетов с использованием ya package](https://wiki.yandex-team.ru/partner/w/dev/howto/create-and-deploy-debian-package/#sborkapaketovsispolzovaniemyapackage)
 - [Заливка пакета на dist](https://wiki.yandex-team.ru/partner/w/dev/howto/create-and-deploy-debian-package/#zalivkapaketanadist)

```bash
# заходим на dev сервер
> ssh dev4.partner.yandex.ru
# обязательно делаем обновление версии (автоматически это не происходит) см. Сборка пакетов ya package
> dch -i 
# собираем deb пакет
> ya package --debian --change-log=debian/changelog ./pkg.json
# разархивируем
> tar -xzvf yandex-partner-solomon-agent-conf.*.*-*.tar.gz
# заливаемн на dist
#    если собирали на precise
> dupload -t partner-precise yandex-partner-solomon-agent-conf_*.*-*_amd64.changes
#    если собирали на bionic
> dupload -t partner-bionic yandex-partner-solomon-agent-conf_*.*-*_amd64.changes
# заходим и проверяем
> ssh dupload.dist.yandex.ru
> find_package.sh yandex-partner-solomon-agent-conf
```
<details>
<summary>вывод</summary>

```bash
Searching in Cacus/MDS:

+-----------------+----------+-------------------------------------------------------+
| repo            | env      | package                                               |
+-----------------+----------+-------------------------------------------------------+
| partner-precise | stable   | yandex-partner-solomon-agent-conf_0.1-2_amd64.deb     |
| partner-precise | stable   | yandex-partner-solomon-agent-conf_0.1-2_amd64.changes |
| partner-precise | stable   | yandex-partner-solomon-agent-conf_0.1-3_amd64.deb     |
| partner-precise | stable   | yandex-partner-solomon-agent-conf_0.1-3_amd64.changes |
| partner-precise | stable   | yandex-partner-solomon-agent-conf_0.1-4_amd64.deb     |
| partner-precise | stable   | yandex-partner-solomon-agent-conf_0.1-4_amd64.changes |
| partner-precise | unstable | yandex-partner-solomon-agent-conf_*.*-*_amd64.deb     |
| partner-precise | unstable | yandex-partner-solomon-agent-conf_*.*-*_amd64.changes |
+-----------------+----------+-------------------------------------------------------+
> sudo dmove partner-precise  stable yandex-partner-solomon-agent-conf *.*-* unstable
```
</details>
