## Style Guide для БД

### TABLE

#### Имя таблицы

```${table_name}```

```sql
CREATE TABLE info_model ();
```

#### Имя таблицы связей

```${table_name_1}_${table_name_2}```

```sql
CREATE TABLE info_model ();
CREATE TABLE attribute ();

CREATE TABLE info_model_attribute ();
```

### CONSTRAINT

#### Первичный ключ

```pk__${table_name}```

```sql
CREATE TABLE info_model (
    CONSTRAINT pk__info_model PRIMARY KEY (id)
);
```

#### Внешний ключ

```fk__${table_name_1}__${foreign_key}__${table_name_2}```

```sql
CREATE TABLE country ();
CREATE TABLE lang (
    country_id BIGINT NOT NULL,

    CONSTRAINT fk__lang__country_id__country FOREIGN KEY (country_id) REFERENCES country (id)
);
```

#### Уникальность

```uq__${table_name}__${field_1}__${field_2}```

```sql
CREATE TABLE info_model (
    region_id BIGINT NOT NULL,
    code TEXT NOT NULL,

    CONSTRAINT fk__info_model__region_id__code UNIQUE (region_id, code)
);
```

#### Проверки

```check__${table_name}__${check_name}```

```sql
CREATE TABLE lang (
    CONSTRAINT check__lang__lang_is_ok CHECK (lang IS TRUE)
);
```

### FUNCTION

```${table_name}__${action_name}```

```sql
CREATE OR REPLACE FUNCTION lang__check_lang_is_ok()
```

### TRIGGER

```trigger__${table_name}__${action_name}```

```sql
CREATE TRIGGER trigger__lang__check_lang_is_ok
```
