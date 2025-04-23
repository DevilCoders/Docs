# Датацентры

С помощью запросов вы можете получить список датацентров и подробную информацию по любому из них.

#### Список датацентров

```
{{ host }}/{{ api-ver }}/datacenters/
```

#### Параметры определенного датацентра

```
{{ host }}/{{ api-ver }}/datacenters/<id датацентра>/
```

## Связанные объекты {#section_hz3_m4l_gbb}

#### Идентификаторы хостов датацентра

```
{{ host }}/{{ api-ver }}/datacenters/<id датацентра>/relationships/hosts/
```

#### Развернутый список хостов датацентра

```
{{ host }}/{{ api-ver }}/datacenters/<id датацентра>/hosts/
```

#### Идентификаторы дочерних датацентров

```
{{ host }}/{{ api-ver }}/datacenters/<id датацентра>/relationships/children/
```

#### Развернутый список дочерних датацентров

```
{{ host }}/{{ api-ver }}/datacenters/<id датацентра>/children/
```

#### Идентификаторы родительских датацентров

```
{{ host }}/{{ api-ver }}/datacenters/<id датацентра>/relationships/parent/
```

#### Развернутый список родительских датацентров

```
{{ host }}/{{ api-ver }}/datacenters/<id датацентра>/parent/
```

#### Идентификатор корневого датацентра

```
{{ host }}/{{ api-ver }}/datacenters/<id датацентра>/relationships/root/
```

#### Параметры корневого датацентра

```
{{ host }}/{{ api-ver }}/datacenters/<id датацентра>/root/
```

