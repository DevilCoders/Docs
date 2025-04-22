# Schema library

This library is written to simplify working with YT table's schemas.

Importing `maps.analyzer.pylibs.schema` should be enough. In examples below we assume, that this module is imported, bringing anything to current scope.

1. [Creating table schema](#creating-table-schema)
1. [Create new table and write data](#create-new-table-and-write-data)
1. [Converting rows/fields, schematizing existing tables](#converting-rowsfields-schematizing-existing-tables)
1. [Deriving schema of existing tables](#deriving-schema-of-existing-tables)
1. [Merging tables](#merging-tables)
    1. [Common recipes](#common-recipes)
1. [Some helpful functions](#some-helpful-functions)

## Creating table schema

First of all, declare some columns:
```python
NAME = column('name', String, help='name of person')
AGE = column('age', Uint64, help='age of person')
COMMENTS = column('comments', Optional(List(String)), help='comments')
HEIGHT = column('height', Optional(Double), help='height of person')
```

`column` accepts name of column, type of column, help string (actually, you can set it to `None`, but this argument is not optional; this field used to describe column for other people, who will read this code later)

Types can be primitives:
    - integers: `Int8`, `Int16`, `Int32`, `Int64`
    - unsigneds: `Uint8`, `Uint16`, `Uint32`, `Uint64`
    - floating: `Double`
    - bool: `Boolean`
    - strings: `String`, `Utf8`
    - datetime: `Date`, `Datetime`, `Timestamp`, `Interval`
    - general type: `Yson`

And also complex ones:
    - `Optional`
    - `List`
    - `Tuple`
    - `Dict`
    - `Struct`
    - `Variant` - exactly one of specified types
    - `Tagged`

See [YT help](https://yt.yandex-team.ru/docs/description/storage/data_types) for details.

Then you can create table:
```python
PERSONS = table([NAME, AGE, COMMENTS, HEIGHT], help='persons')
```

Now we are ready to use it.

## Create new table and write data

To get YT schema for `column` or `table` you can use `schema` property.
Let's create new temporary table with `PERSONS` schema:
```python
persons = ytc.create_temp_table(schema=PERSONS.schema)
ytc.write_table(persons, [{'name': 'Krjemelic', 'age': 50L}])
```

## Converting rows/fields, schematizing existing tables

Quite often we get records with slightly different types. For example, we have `float` instead of `long`. In this case YT will fail to write this record to schematized table. We can `cast` rows (or fields) in order to get coverted row (or field):
```python
age = AGE.cast(10.0)  # ok, returns 10L
# AGE.cast("dsflfsh")  # raises ValueError
row, errors = PERSONS.cast({'name': "Vasiliy", 'age': "25", 'comments': None})  # ok, updates "25" to 25L, `errors` is `{}`
row, errors = PERSONS.cast({'name': 'Petr', 'age': "lala"})  # raises as long as `age` is required, but can't be converted
row, errors = PERSONS.cast({'name': 'Simon', 'age': 35.0, 'height': "haha"})  # ok, updates 35.0 to 35L and also returns errors: `{'height': <cast error message>}`
```

Another common case is having table without schema. We can apply schema to it with `schematize` function (`maps.analyzer.pylibs.schema.operations`):
```python
persons = schematize(ytc, non_schematized_persons, PERSONS)
# or inplace
schematize(ytc, non_schematized_persons, PERSONS, inplace=True)  # `non_schematized_persons` now with schema
```

## Deriving schema of existing tables

We can get `table` schema from existing YT table in order to, for example, add some columns and create new table
```python
persons_table = get_table(ytc, persons)
persons_with_address = persons_table.add_columns([column('address', String, help='persons addess')])
tmp = ytc.create_temp_table(schema=persons_with_address.schema)
# tmp contains all columns from `persons`, and additionally have 'address' column
```

The problem with code above is that it won't work as you expected if `persons` is not strong schema (i.e. such that was set by user, not by YT operations like sort). The reason is that weak (as opposite to strong) schemas can be changed by YT, but strong ones - can't (well, `sort_order` can be changed, but columns itself - names and types - can't). This can lead to surprising behaviour.
Assuming `persons` is in weak schema mode, you won't be able to sort `persons_with_address` by columns that are not present in schema, because YT is not able to change strong schema. But you can sort `persons` by these columns!
So basically you don't want to use weak schema.

In this case you should use `derive_schema` function, which will update schema only if it is strong (not to be confused with strict/nonstrict!):
```python
address = column('address', STRING, help='persons addess')
ytc.create_temp_table(schema=derive_schema(ytc, persons, alter_table=lambda t: t.add_columns([address])))
```

Code above will create table with schema only if it was strong.

## Merging tables

You can merge tables with schemas, different in various ways:
- different set of columns
- different types of same column

There're main function `merge_tables` with arguments, controlling which differencies are allowed:
* `shrink=False` — different columns will be just removed from result
* `extend_types=True` — allow extending type to `Any` if columns have incompatible types
* `optionalize_types=True` — allow making columns optional
* `narrow_any=False` — prefer using concrete type when merging complex type (struct/dict/list/etc.) and `Any`
* `narrow_opt=False` — make column required if at least one of tables have it required

You can also specify `schema` you want as output, in this case function will validate, that input table can be merged into it.

There're also functions to get merged schema instead of merging operations:
* `merge_tables_schema` — don't merge, just produce result table schema using options above
* `infer_merge_schema` — infer resulting schema; unlike above function it does not allow require some output schema
* `validate_merge_schema` — check that schemas can be merged into specified one

### Common recipes

#### Adding new required column

If you added some new required column, you may use `shrink=True`.
Merged table won't have this column, if there're mixed schemas in input tables, thus producing old schema. When all input columns get new column, merged table will get it too, switching to new schema.

#### Restricting yson columns

If you assign complex type to some yson-column, but haven't changed actual contents, use `narrow_any=True`. Merged table will have complex type-v3.

#### Making optional columns required

If data always exists, use `narrow_opt`, so that merged table will have required column as result.
If data may be absent, use `optoinalize_types`, so that merged column will stay optional until all sources tables switches to new schema.

## Some helpful functions

* `optional` — make optional column (doesn't modify column, just returns new one)
* `required` — make required column
* `strict` — make table strict (as before, it creates new table instead of modifying argument)
* `nonstrict` — make nonstrict table
