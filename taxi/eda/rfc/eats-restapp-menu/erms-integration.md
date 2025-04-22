# Переезд с коры на erms

## Текущая концепция eats-restapp-menu

eats-restapp-menu минимально использует содержимое меню для своих операций,
он не хранит каждое поле индивидуально (например: имя, описание и пр.), все хранится
в базе двумя JSON'ами (один для полей проходящих модерацию, второй для
остального). Поля options/options_group/images хранятся отдельно, с ними аналогично.

![now](./img/db_scheme.png)

## Сравнение полей:
```
По блюдам:
+--------------------------------+----------------------+----------------------------------+
| erms                           | eats-restapp-menu    | remarks                          |
+--------------------------------+----------------------+----------------------------------+
| origin_id                      | id                   |                                  |
| category_origin_ids[]          | categoryId           | optional array vs required id    |
| name                           | name                 |                                  |
| description                    | description          |                                  |
| price                          | price                |                                  |
| vat                            | vat                  | decimal64::Decimal<2> vs integer |
| weight.value                   | measure              | decimal64::Decimal<3> vs double  |
| weight.unit                    | measureUnit          |                                  |
| sort                           | sortOrder            |                                  |
| options_groups                 | modifierGroups       | см. options_groups               |
| pictures[].url                 | images[].url         |                                  |
| pictures[].avatarnica_identity | ?                    |                                  |
| pictures[].ratio               | ?                    |                                  |
| pictures[].sort                | ?                    |                                  |
| ?                              | thumbnails           |                                  |
| reactivate_at                  | reactivatedAt        |                                  |
| available                      | available            |                                  |
| legacy_id                      | menuItemId           |                                  |
| nutrients                      | nutrients            |                                  |
| adult                          | ?                    |                                  |
| shipping_types                 | ?                    |                                  |
| inner_options                  | ?                    |                                  |
| promo_price                    | ?                    |                                  |
| ordinary                       | ?                    |                                  |
| choosable                      | ?                    |                                  |
| deleted_at                     | ?                    |                                  |
| stock                          | ?                    |                                  |
| short_name                     | ?                    |                                  |
+--------------------------------+----------------------+----------------------------------+

По категориям:
+--------------------------------+----------------------+----------------------------------+
| erms                           | eats-restapp-menu    | remarks                          |
+--------------------------------+----------------------+----------------------------------+
| origin_id                      | id                   |                                  |
| parent_origin_id               | parentId             |                                  |
| name                           | name                 |                                  |
| sort                           | sortOrder            |                                  |
| reactivate_at                  | reactivatedAt        |                                  |
| available                      | available            |                                  |
| legacy_id                      | ?                    |                                  |
| pictures                       | ?                    |                                  |
| schedule                       | ?                    |                                  |
| deleted_at                     | ?                    |                                  |
+--------------------------------+----------------------+----------------------------------+

По options_groups:
+--------------------------------+-----------------------+---------------------------------+
| erms                           | eats-restapp-menu     | remarks                         |
+--------------------------------+-----------------------+---------------------------------+
| origin_id                      | id                    |                                 |
| name                           | name                  |                                 |
| options                        | modifiers             | см.options                      |
| min_selected_options           | minSelectedModifiers  |                                 |
| max_selected_options           | maxSelectedModifiers  |                                 |
| sort                           | sortOrder             |                                 |
| legacy_id                      | menuItemOptionGroupId |                                 |
| is_required                    | ?                     |                                 |
| deleted_at                     | ?                     |                                 |
+--------------------------------+-----------------------+---------------------------------+

По options:
+--------------------------------+----------------------+----------------------------------+
| erms                           | eats-restapp-menu    | remarks                          |
+--------------------------------+----------------------+----------------------------------+
| origin_id                      | id                   |                                  |
| name                           | name                 |                                  |
| price                          | price                | decimal64::Decimal<2> vs double  |
| vat                            | vat                  | decimal64::Decimal<2> vs integer |
| min_amount                     | minAmount            |                                  |
| max_amount                     | maxAmount            |                                  |
| reactivate_at                  | reactivatedAt        |                                  |
| available                      | available            |                                  |
| multiplier                     | ?                    |                                  |
| promo_price                    | ?                    |                                  |
| sort                           | ?                    |                                  |
| deleted_at                     | ?                    |                                  |
+--------------------------------+----------------------+----------------------------------+
```

## Схема связей сервисов

При обновлении: 
eats-restapp-menu ---> core
      |
      +--------------> eats-rest-menu-storage

Отправляем изменения меню и в кору, и в erms, в качестве updated_at отсылаем created_at от ревизии

При получении:
eats-restapp-menu ---> core
      .
      +..............> eats-rest-menu-storage

Получаем меню из коры, по конфигу альтернативный вариант получение из erms



## Проблема
1) Полей в erms больше чем в текущей схеме коры, т.е. erms схема более детальная
2) Название многих полей не совпадает
3) Инкрементальный формат обновления с передачей удаленных с полными записями не предусмотрен в eats-restapp-menu (нужно будет реализовывать)

## Решение
Решение общее такое, всегда во всех алгоритмах eats-restapp-menu работаем
в новом формате меню (erms), в базе хранится может как старый, так и новый формат.
В ревизию меню зашита версия схемы, поэтому нет проблемы отличить JSON'ы в базе.
При получении из базы сразу конвертировать в новый (с потерей, т.к. нехватает нескольких полей),
при получении из коры также конвертировать в новый и сохранять в базу в новом формате.
Этот метод оставит совместимость со старыми данными в базе.
По поводу коллизий с обновлениями пришедшими из eats-restapp-menu и синхронизации с корой, все
они будут решаться за счет передачи поля updated_at. В eats-restapp-menu оно будет иметь значения
created_at ревизии, т.е. на ручку обновления придут только новые блюда с updated_at меньше коровой.


## План переезда
1) Получаем из коры поля необходимые для erms и в текущей(старой) схеме eats-restapp-menu
2) Храним в новом формате и отдаем на фронт в старом формате схемы (для совместимости),
   при обновлении с фронта доп.поля дописываем из базовой ревизии (ревизия на основе которой
   производилось редактирование), так мы не потеряем новые поля.
3) При обновлении сохраняем паралельно и в кору, и в erms, эти данные повторно придут
   при синхронизации, но это не проблема
4) Делаем получение данных по флагу (конфиг 3.0) или из коры, или из erms