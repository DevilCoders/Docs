# eats-deeplink

Бибилиотека для формирования ссылок на
различные экраны приложения Яндекс.Еда.

## Quick Start

Чтобы воспользоваться бибилиотекой, необходимо подключить файл `deeplink_builder.hpp`.
Далее, в зависимости от нужной ссылки, задать параметры в билдере.
Например, собрать ссылку на ресторан со слагом `<SLUG>` можно так:

```(cpp)
eats_deeplink::DeeplinkBuilder().Restaurant(<SLUG>).Build()
```

На категорию `<CATEGORY>` в магазине со слагом `<SLUG>`:

```(cpp)
eats_deeplink::DeeplinkBuilder().Shop(<SLUG>).Category(<CATEGORY>).Build()
```

Так же можно собрать ссылку для веба, если в начале использовать
функцию `WebLinkBuilder()`.

Остальные примеры можно посмотреть в файле `src/tests/deeplink_builder_test.cpp`.
