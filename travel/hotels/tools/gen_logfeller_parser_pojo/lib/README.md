# gen_logfeller_parser_pojo_lib

A set of annotations to control logfeller schema.

## @LogfellerConfig

Use this annotation to redefine default behavior.

### Required field

```java
@LogfellerConfig(demand=FieldDemand.REQUIRED)
```

will make field required by adding

```json
"demand": "required"
```

to config.

### Custom name

```java
@LogfellerConfig(name="custom-name")
```

will set custom name for field.


### Custom type

```java
@LogfellerConfig(type=FieldType.VT_STRING)
```

will set string as type for field.

## @LogfellerDecompose

Adding

```java
@LogfellerDecompose
```

trigger generator to recursively decompose object.

## @LogfellerIgnore

Adding

```java
@LogfellerIgnore
```

to filed marks field as ignored and it won't be added to log schema.
