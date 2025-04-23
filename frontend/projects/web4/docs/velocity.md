# Скоростные оптимизации

В web4 есть множество способов улучшить производительность ваших фичей / компонентов с помощью различных подходов.

## entry-optimizer
Удаление из js-бандла ненужного клиентского кода для статичной/негидрируемой части фичи.

![Схема entry-optimizer](https://jing.yandex-team.ru/files/kholstinin/entryOptimizerOnlyStatic.png)

[Подробнее](../src/components/Root/README.md)

## Минируты
Позволяют гидрировать лишь часть колдунщика.

![Схема минирутов](https://jing.yandex-team.ru/files/kholstinin/createSubRoot.png)

![entry-optimizer + miniroot](https://jing.yandex-team.ru/files/kholstinin/entryOptimizerWithSubRoot.png)

[Подробнее](../src/components/Root/README.md)

## Ванильные компоненты
Позволяют добавлять к негидрируемым компонентам простые сценарии интерактивности.

![entry-optimizer + vanilla](https://jing.yandex-team.ru/files/kholstinin/entryOptimizerWithVanilla.png)

[Подробнее](../src/vendors/vanillaInReact/README.md)

## LazyLoader
Инструмент для отложенной загрузки синглтон компонентов для страницы (попапов, тултипов).

[Подробнее](../src/features/LazyLoader/README.md)

## ProgressiveRenderer
Позволяет рендерить элементы списка при попадании элементов во вьюпорт.

[Подробнее](../src/components/ProgressiveRenderer/README.md)

## PushModule
Позволяет пушить статику только при реальном рендере компонента на сервере

[Подробнее](../src/components/PushModuleRenderer/README.md)
