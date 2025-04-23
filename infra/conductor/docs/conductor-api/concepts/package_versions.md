# Версии пакетов

Запросы позволяют получить список версий пакетов и подробную информацию по любой из них.

#### Список версий

```
{{ host }}/{{ api-ver }}/package_versions
```

#### Параметры определенной версии

```
{{ host }}/{{ api-ver }}/package_versions/<id версии>
```

## Связанные объекты {#section_iwr_4lr_gbb}

#### Идентификатор пакета

```
{{ host }}/{{ api-ver }}/package_versions/<id версии>/relationships/package
```

#### Параметры пакета

```
{{ host }}/{{ api-ver }}/package_versions/<id версии>/package
```

#### Идентификатор репозитория

```
{{ host }}/{{ api-ver }}/package_versions/<id версии>/relationships/repo
```

#### Параметры репозитория

```
{{ host }}/{{ api-ver }}/package_versions/<id версии>/repo
```

