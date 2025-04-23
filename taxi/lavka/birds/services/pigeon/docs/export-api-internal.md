# Export API

* `/actual-products` - актуальные продукты
* `/actual-categories` - актуальные категории
* `/deleted-products` - удаленные продукты
* `/deleted-categories` - удаленные категории

> По смыслу:
> У нас есть связь с каждой сущностью в таблице history_subject.
> В этой таблице есть колонка revision, которая обновляется при обновлении сущности.
> Из дополнительных триггеров сущность product обновляем при обновлении product_attribute_value, front_category_product.
> Удаленные же сущности достаются по курсору из таблицы history.

## Доступ к API только с service ticket-ом

`ya tool tvmknife get_service_ticket sshkey --dst 2027174 --src 2013636`

## Сброс курсора

`ВАЖНО! Курсор сбрасывать только в экстренной ситуации. В остальных случаях идти к WMS-никам`

### products

```sql
UPDATE history_subject
SET revision = DEFAULT
WHERE id IN (SELECT history_subject_id FROM product);
```

### master categories

```sql
UPDATE history_subject
SET revision = DEFAULT
WHERE id IN (SELECT history_subject_id FROM master_category);
```

### front categories

```sql
UPDATE history_subject
SET revision = DEFAULT
WHERE id IN (SELECT history_subject_id FROM front_category);
```
