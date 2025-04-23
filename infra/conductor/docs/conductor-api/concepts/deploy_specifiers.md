# Деплой-пары

Запросы позволяют получить список деплой-пар, для которых настроены особенности выкладки.

#### Список деплой-пар

```
{{ host }}/{{ api-ver }}/deploy_specifiers
```

#### Параметры определенной деплой-пары

```
{{ host }}/{{ api-ver }}/deploy_specifiers/:id
```

## Связанные объекты {#section_zr4_w5l_gbb}

#### Идентификатор деплой-группы, входящей в пару

```
{{ host }}/{{ api-ver }}/deploy_specifiers/:deploy_specifier_id/relationships/deploy_group
```

#### Параметры деплой-группы, входящей в пару

```
{{ host }}/{{ api-ver }}/deploy_specifiers/:deploy_specifier_id/deploy_group
```

#### Идентификатор пакета, входящего в пару

```
{{ host }}/{{ api-ver }}/deploy_specifiers/:deploy_specifier_id/relationships/package
```

#### Параметры пакета, входящего в пару

```
{{ host }}/{{ api-ver }}/deploy_specifiers/:deploy_specifier_id/package
```

#### Идентификатор настроек выкладки, к которые применяются к паре

```
{{ host }}/{{ api-ver }}/deploy_specifiers/:deploy_specifier_id/relationships/deploy_settings
```

#### Параметры настроек выкладки, к которые применяются к паре

```
{{ host }}/{{ api-ver }}/deploy_specifiers/:deploy_specifier_id/deploy_settings
```

