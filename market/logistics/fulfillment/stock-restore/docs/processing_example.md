# Пример обработки потока событий

Ниже приведен порядок изменения состояние восстановленного стока в процессе применения записей аудите и записи из корректного стока.


**1. Начальное состояние**

Начальное состояние восстанавливаемой записи содержит только данные Unit ID.

*Восстановленная запись*

```
sku_id:                  null
sku:                     sku1 *
vendorId:                   1 *
warehouseId:                1 *
fit:                     null
freezed:                 null
defect:                  null
defect_freezed:          null
expired:                 null
expired_freezed:         null
quarantine:              null
quarantine_freezed:      null
surplus:                 null
surplus_freezed:         null
прочие колонки стока:    null
```

**2. Событие аудита "STOCK_FREEZE_APPLIED"**

В событиях, связанных с фризами, содержится количество обычное и количество фризов для одного типа стока (fit, surplus, defect и так далее).
Они применяются к восстанавливаемой записи и замещают предыдущее значение.

Так обрабатываются все записи аудита, связанные с изменением количества.

```
"unitId": {"sku":"sku1", "vendorId":1, "warehouseId":1},
"stock":{
    "TYPE": "FIT",
    "AMOUNT": 4,
    "FREEZE_AMOUNT": 2
}
```

*Восстановленная запись*

```
sku_id:                  null
sku:                     sku1
vendorId:                   1
warehouseId:                1
fit:                        4 *
freezed:                    2 *
defect:                  null
defect_freezed:          null
expired:                 null
expired_freezed:         null
quarantine:              null
quarantine_freezed:      null
surplus:                 null
surplus_freezed:         null
прочие колонки:          null
```

**3. Событие аудита "SKU_CREATED"**

События создания стока не содержат сумм и могут появляться в истории после событий изменений стока, фризов.
Считаем, что все не означенные еще количества равны 0.

Также у этих записей колонка target_it содержит значение sku_id.

```
(колонка target_id = 638643356)
"unitId":{
    "sku": "sku1",
    "vendorId": 3358375,
    "warehouseId": 165565
}
```

*Восстановленная запись*

```
sku_id:             638643356 *
sku:                     sku1
vendorId:                   1
warehouseId:                1
fit:                        4
freezed:                    2
defect:                     0 *
defect_freezed:             0 *
expired:                    0 *
expired_freezed:            0 *
quarantine:                 0 *
quarantine_freezed:         0 *
surplus:                    0 *
surplus_freezed:            0 *
прочие колонки:          null
```

**4. Запись из доверенного стока**

Данные записи будут присутствовать в истории всего один раз и берутся из таблицы корректного стока.
Из них заполняются все колонки, которые мы еще не определили при помощи событий аудита.
В данном случае меняются только прочие колонки, так как ранее уже было событие создание SKU, которое обнулило суммы.

> :warning: Важно учесть, что эти "прочие колонки" мы определяем только один раз на этапе обработки записи в доверенном стоке.
То есть если габариты SKU обновлялись в последующие дни, в восстановленной записи это не отразится.

Восстановленная запись 

```
sku_id:             638643356
sku:                     sku1
vendorId:                   1
warehouseId:                1
fit:                        4
freezed:                    0
defect:                     0
defect_freezed:             0
expired:                    0
expired_freezed:            0
quarantine:                 0
quarantine_freezed:         0
surplus:                    0
surplus_freezed:            0
прочие колонки:      означены *
```

**5. Событие аудита "STOCK_UPDATED"**

Аналогично записи аудита о фризах, указанное в событии количество стока применяется к восстанавливаемой записи.

```
"unitId": {"sku":"sku1", "vendorId":1, "warehouseId":1},
"stock":{
    "TYPE": "SURPLUS",
    "AMOUNT":4
}
```

Восстановленная запись 

```
sku_id:             638643356
sku:                     sku1
vendorId:                   1
warehouseId:                1
fit:                        4
freezed:                    0
defect:                     0
defect_freezed:             0
expired:                    0
expired_freezed:            0
quarantine:                 0
quarantine_freezed:         0
surplus:                    4 *
surplus_freezed:            0
прочие колонки:      означены
```

**6. Финальное состояние**

В конце обработки в восстанавливаемой записи должны быть означены все поля, но возможна ситуация, при которой часть из них останется в значении null.
Такие ситуации надо будет разбирать отдельно.
