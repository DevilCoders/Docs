# Контроллеры, миксины, гейты

## Версионирование

Модуль использует semver, версии фиксируются тегами в репозитории.
Совместимость гарантируется только для публичного интерфейса модуля.

## Контрибьют

PR в ветку master. Ревьюеры: @kaero, @flack, @orion, @an9eldust.

## Сущности предоставляемые модулем

* Контроллеры
    * [Controller](/docs/Controller.md)
        – базовый контроллер;
    * [Page](/docs/Page.md)
        — типовой контроллер страницы;
    * [Gate](/docs/Gate.md)
        – контроллер обработчика AJAX-запросов;

* Миксины к Controller
    * [ProvidersMixin](/docs/ProvidersMixin.md)
        — добавляет декларативный метод описания иерархически связанных источников данных («провайдеров», data providers);
    * [TemplateMixin](/docs/TemplateMixin.md)
        – добавляет абстрактные методы рендеринга;
        * [BEMTemplateMixin](/docs/BEMTemplateMixin.md)
            – реализация с использованием BEM priv.js технологии;
    * [PageActionBuild](/docs/PageActionBuild.md)
        — при подмешивании к наследнику [Page](/docs/Page.md) добавляет [`#action_build()`](/docs/PageActionBuild.md#action_build);

* Другое
    * [ControllerParams](/docs/ControllerParams.md)
        – выделенная часть прототипа контроллера, которая может быть использована на клиенте.
