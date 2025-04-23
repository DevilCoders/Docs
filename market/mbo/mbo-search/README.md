##### Открываем из Idea:
- Установка/настройка arc: https://doc.yandex-team.ru/arc/setup/arc/install.html
- Конфигурация IDE: https://doc.yandex-team.ru/arc/setup/arc/ide.html
  Там-же много другой полезной информации по работе с arc

По документации устанавливаем arc, монтируем, ставим плагин для idea.

Выполняем `scripts/create-idea-project-with-libs.sh` (чтобы сборка прошла удалённо можно выполнить `scripts/create-idea-project-with-libs.sh --dist`). В этом же скрипте есть более детальная команда, если хочется особенного.

После чего проект можно будет открыть идеей из папки `idea ~/IdeaProjects/mbo-category/`.
Можно настроить путь `IdeaProjects` через `export ARC_PROJECTS_ROOT=...` в `~/.profile`).

##### Локальная сборка, запуск тестов:
- **ya make** - собрать модуль, в директории которого в данный момент находимся
- **ya make -t** - запустить тесты модуля, в директории которого в данный момент находимся (-t: small, -tt small+medium, -ttt small+medium+large)

##### Пайплайн и релизная машина
https://tsum.yandex-team.ru/pipe/projects/mbo/pipelines/mbo-search-arc
https://tsum.yandex-team.ru/pipe/projects/mbo/delivery-dashboard/mbo-search-arc
