# Skutcher

Компонент, привязывающий предложения к SKU

wiki: https://wiki.yandex-team.ru/Market/Development/DataPreparation/Skutcher/
информация про шардирование: https://wiki.yandex-team.ru/market/development/datapreparation/Как-работает-шардирование-в-Скутчере-и-Матчере/

### Сборка и деплой
Сборку и выкладку компонента выполняет релизная машина в ЦУМе: https://tsum.yandex-team.ru/pipe/projects/ir/delivery-dashboard/skutcher2-cd-arc
Pipeline: https://tsum.yandex-team.ru/pipe/projects/ir/pipelines/skutcher2-cd-arc

### Dashboards
Testing: https://grafana.yandex-team.ru/d/3L20UAVnz/skutcher2_sharded_testing?orgId=1&from=now-1h&to=now
Stable: todo

### Открываем из Idea:

- Установка/настройка arc: https://doc.yandex-team.ru/arc/setup/arc/install.html
- Конфигурация IDE: https://doc.yandex-team.ru/arc/setup/arc/ide.html
  Там-же много другой полезной информации по работе с arc

По документации устанавливаем arc, монтируем, ставим плагин для idea.

Выполняем `scripts/create-project.sh` (чтобы сборка прошла удалённо можно выполнить `scripts/create-idea.sh --dist`). В этом же скрипте есть более детальная команда, если хочется особенного.

После чего проект можно будет открыть идеей из папки `idea ~/IdeaProjects/mbo-category/`.
Можно настроить путь `IdeaProjects` через `export ARC_PROJECTS_ROOT=...` в `~/.profile`).
