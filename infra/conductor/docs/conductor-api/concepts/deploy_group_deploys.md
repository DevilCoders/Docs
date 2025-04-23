# Выкладки по деплой-группам

Запросы позволяют получить список завершенных выкладок и подробную информацию по любой из них.

#### Список выкладок

```
{{ host }}/{{ api-ver }}/deploy_group_deploys
```

#### Параметры определенной выкладки

```
{{ host }}/{{ api-ver }}/deploy_group_deploys/<id выкладки>
```

## Связанные объекты {#section_dk2_prl_gbb}

#### Идентификатор таска, соответствующего выкладке

```
{{ host }}/{{ api-ver }}/deploy_group_deploys/<id выкладки>/relationships/task  
```

#### Параметры таска, соответствующего выкладке

```
{{ host }}/{{ api-ver }}/deploy_group_deploys/<id выкладки>/task  
```

#### Идентификатор деплой-группы выкладки

```
{{ host }}/{{ api-ver }}/deploy_group_deploys/<id выкладки>/relationships/deploy_group  
```

#### Параметры деплой-группы выкладки

```
{{ host }}/{{ api-ver }}/deploy_group_deploys/<id выкладки>/deploy_group
```

#### Идентификатор пакета, участвовавшего в выкладке

```
{{ host }}/{{ api-ver }}/deploy_group_deploys/<id выкладки>/relationships/package
```

#### Параметры пакета, участвовавшего в выкладке

```
{{ host }}/{{ api-ver }}/deploy_group_deploys/<id выкладки>/package
```

