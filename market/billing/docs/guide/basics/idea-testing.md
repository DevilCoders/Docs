# Настройки тестирования в IDEA


## Тестирование

В первую очередь открываем проект arc/market/mbi/mbi/ в IDEA.

Открываем меню настроек конфигурации. Создаем новую конфигурацию типа JUnit.
В настройках выбираем следующие параметры:

-cp: `mbi-billing`

VM Options (не забудьте заменить PATH_TO_PROJECT на путь в вашей системе):
```
-Djava.library.path=PATH_TO_PROJECT/arc_mbi/dlls
-Djna.library.path=PATH_TO_PROJECT/arc_mbi/dlls

```
main class: `ru.yandex.market.billing.fulfillment.FulfillmentOrderBillingServiceDbUnitTest`

Working directory: `$MODULE_WORKING_DIR$` - оставляем дословно как написано.

После этих действий можете запускать тест. Если он внезапно упал - значит надо обновить проект до серверной
версии(`arc pull`).
