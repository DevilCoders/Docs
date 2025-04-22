# archon-renderer

Report-renderer в качестве Archon-компонента, а также команда для его запуска со всеми необходимыми компонентами.

## Опции запуска

[renderer-start-mode](https://a.yandex-team.ru/arcadia/frontend/projects/infratest/packages/archon-renderer/commands/renderer.js?rev=r9379763#L73):
* development – код шаблонов загружается при первом обращении
* development-with-preload-templates – код шаблонов загружается при старте компонента, но при рестарте воркеров renderer шаблоны загрузятся только после первого обращения
* production – загружает шаблоны при каждом старте воркеров renderer
