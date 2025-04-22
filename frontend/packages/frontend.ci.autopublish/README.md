# frontend.ci.autopublish

Пакет реализует два скрипта prepublish и release. Обе команды нужны для работы
автопубликации npm-пакетов.

## prepublish

Выполняет роль обязательной проверки в репозиториях в которых включена
автопубликация npm-пакетов. В режиме dry-run скрипт не генерирует сайдэффектов и
проверяет, что сборка npm-пакета проходит без ошибок.

Без dry-run скрипт сгенерирует артефакты versions-artifact и npmtarball.

Подробнее о них можно прочитать [в документации](https://a.yandex-team.ru/arc_vcs/frontend/docs/faq/packages-autopublish.md#ustrojstvo-avtomaticheskoj-publikacii) про автопубликацию.

## release

Скрипт публикует предварительно собранные тарболы в npm registry и коммитит
изменения в VCS.
