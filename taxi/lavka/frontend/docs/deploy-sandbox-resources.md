Sandbox-ресурсы, загружаемые в няню при выкатке
----

### Конфигурация на уровне проекта

В конфиге по пути `projects/<project_name>/service.yaml` в поле `sandbox.resources` можно указать ресурсы, которые проект будет использовать после выкатки на стенды. Можно указать разные конфигурации для разных окружений: `unstable`, `testing` и `production`.

> <span style="color:red;">Важно! При изменении конфигураций `service.yaml` необходимо соответствующим образом добавлять/изменять/удалять prestart-скрипты в директории `projects/webview/scripts/prestart_scripts`</span>.

**Формат описания ресурсов**

Ресурсы передаются в виде массива в одно из допустимых окружений. Список параметров ресурса:

- `local_path` - **обязательный** - путь, в который ресурс будет помещен на машинке
- `resource_id` - **обязательный, если не указан `resource_type`** - айди ресурса
- `resource_type` - **обязательный, если не указан `resource_id`** - тип ресурса - <u>запрошен будет последний, подходящий под параметры поиска (фильтры)</u>, если они заданы (см. ниже). 
- `owner` - имя [группы](https://docs.yandex-team.ru/sandbox/groups) - **рекомендуется к использованию** - добавляет поисковой фильтр имени группы. <span style="color:red;">Важно</span>: если ресурс с указанным `resource_id` будет иметь `owner`, отличного от заданного, этот ресурс не будет включен в сборку; при указании `resource_type` будет возвращен последний ресурс с указанным `resource_type` выложенный `owner`.
- `attributes` - массив `название_атрибута: значение_атрибута` - является опциональным, к параметру применяются все замечания, указанные для параметра `owner`.

### Примеры

В следующем примере два ресурса будут подтянуты только на стенды с окружением `unstable`:

```yaml
sandbox:
  resources:
    unstable:
      - local_path: geodata6.bin
        resource_type: GEODATA6BIN_STABLE
      - local_path: uatraits-data.tar.gz
        resource_type: UATRAITS_DATA_BUNDLE
```

Здесь же будет выбран последний ресурс типа `GEODATA6BIN_STABLE`, заваренный группой `GEOBASE`, а второй ресурс будет последним опубликованным ресурсом, соответсвующий перечисленным ниже атрибутам.

```yaml
sandbox:
  resources:
    unstable:
      - local_path: geodata6.bin
        resource_type: GEODATA6BIN_STABLE
        owner: GEOBASE
      - local_path: uatraits-data.tar.gz
        resource_type: UATRAITS_DATA_BUNDLE
        attributes:
          - released: stable
          - platform: Linux-4.19.183-42.2mofed-x86_64-with-Ubuntu-12.04-precise
```
