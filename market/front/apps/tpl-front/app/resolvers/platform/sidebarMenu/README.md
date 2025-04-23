# Боковое меню
При заходе на каждую страницу приложение автоматически проверяет, доступна ли фича `hasCampaignSidebar` на этой странице (про кокон читать [здесь](https://github.yandex-team.ru/market/partner-cookbook/blob/master/docs/COCON.md#конфиг-пример)):
 - Если доступна, получаем конфигурацию меню и строим его, отображая в меню только доступные текущему пользователю/текущей кампании пункты (это определяется по конфигурации страниц в коконе).
 - Если недоступна, ничего не делаем и не отображаем меню

## Меню кабинета (для всех кабинетов кроме SHOP и SUPPLIER)
Для каждого кабинета в соответствующей ему [директории](https://github.yandex-team.ru/market/partnernode/tree/master/configs/platforms) может быть указана схема меню.

Например, DELIVERY:
- Схема меню в конфигурации: https://github.yandex-team.ru/market/partnernode/blob/master/configs/platforms/delivery/index.json#L4
- Фича в коконе: https://a.yandex-team.ru/arc/trunk/arcadia/market/mbi/cocon/cabinet-configs/src/main/resources/cabinets/delivery.json?rev=r7613936#L10

## Единое меню маркетплейса (только для кабинетов SHOP и SUPPLIER)
Внедрено в рамках проекта Единая навигация маркептплейса. Схема меню для них общая и лежит в https://github.yandex-team.ru/market/partnernode/blob/master/app/resolvers/platform/sidebarMenu/menu/index.ts

В меню [можно добавить](https://github.yandex-team.ru/market/partnernode/blob/2021.3.12/app/resolvers/platform/sidebarMenu/menu/index.ts#L314-L319) страницу на уровне бизнеса.
Если в меню есть страница на уровне бизнеса, то при переходе на неё пользователь увидит то же самое меню, которое видел до перехода, если в коконе [указана фича меню](https://a.yandex-team.ru/arc/trunk/arcadia/market/mbi/cocon/cabinet-configs/src/main/resources/cabinets/business.json?rev=r8424188#L379)

#### ADV
Для ADV отображается кабинетное меню, т.е. доступность каждого пункта определяется [по конфигу shop.json](https://a.yandex-team.ru/arc/trunk/arcadia/market/mbi/cocon/cabinet-configs/src/main/resources/cabinets/shop.json)

#### Маркетплейсы
Для всех DBS и FBx отображается новое меню маркетплейса, т.е. доступность каждого пункта определяется по [общему конфигу бизнеса](https://a.yandex-team.ru/arc/trunk/arcadia/market/mbi/cocon/cabinet-configs/src/main/resources/cabinets/business.json) в коконе.
Главные особенности этого меню:
- Оно не зависит от того, в каком магазине находится пользователь, а зависит только от того, в каком бизнесе он находится
- Если пользователь находится в магазине DBS и переходит из меню в пункт Поставки (доступный только FBY), он увидит заглушку с предложением перейти в FBY через переключалку магазинов или зарегистрироваться по недостающей модели. За это отвечает поле `page[].params.placementTypes` в [конфигурации конкретной страницы](https://a.yandex-team.ru/arc/trunk/arcadia/market/mbi/cocon/cabinet-configs/src/main/resources/cabinets/business.json?rev=r8424188#L386) в коконе, **Поэтому важно держать его актуальным**
- Хотя в меню доступность пунктов и проверяется по [общему конфигу бизнеса](https://a.yandex-team.ru/arc/trunk/arcadia/market/mbi/cocon/cabinet-configs/src/main/resources/cabinets/business.json) в коконе, при переходе на сами страницы доступ определяется уже по конфигу конкретного кабинета - shop.json для DBS и supplier.json для FBx.
  - В связи с этим получается, что 2 разных конфига нужно держать синхронизированными: `page[].params.placementTypes` из предыдущего пункта в конфиге бизнеса и поле `page[].states` в конфиге конкретного кабинета. Например, одна и та же страница в [конфиге бизнеса](https://a.yandex-team.ru/arc/trunk/arcadia/market/mbi/cocon/cabinet-configs/src/main/resources/cabinets/business.json?rev=r8431179#L608) и в [конфиге кабинета](https://a.yandex-team.ru/arc/trunk/arcadia/market/mbi/cocon/cabinet-configs/src/main/resources/cabinets/supplier.json?rev=r8424188#L1812)
  - По мере переезда страниц на уровень бизнеса таких мест, где нужно синхронизироваться, будет всё меньше.
- Если пользователь не имеет доступа к странице по ролям, то при переходе на неё из меню он увидит заглушку с предложением запросить доступ
