Configuration File Format
=========================
This file describes only a part of the configuration file format. Additional
information can be found on [wiki][wiki].

The file must be called `json2ymapsdf.xml` and contain sections described
below. All sections must be enclosed by the `<json2ymapsdf>` tag.


Split Rules
-----------
The splitting rules are used to split a ymapsdf schema on several by
[regions](#regions).

The rules description is located under the path `/json2ymapsdf/split-rules`.

The splitting process is based on joining tables of the initial schema with
tables that contain information about regions (their isocodes). Therefore, each
rule describes a way to join tables. A rule is described by one or several
`<join>` tags.

The tag `<join>` has two **required** attributes:
* `table` - the table to be splitted.
* `with-table` - the table used for splitting (usually this is a table with name
  `..._isocode`). This table is joined to the table `table`.

The tag `<join>` **must** contain one attribute `using` or a pair of attributes
`table-key` and `with-table-key`. These attributes describe the key or keys the
tables must be joined by.

If a table has to be joined with several tables then several `<join>` tags with
the same attribute `table` are used. The attribute `as` is used if a table must
be joined several times with the same table. It creates an alias for the joined
table.

The default join type is `INNER`, however if several joins take place `LEFT
JOIN` is used. The attribute `join-type` is used to enforce this fact. It can
take two values: `left` or `inner` [default].

By default, each joined table is used in filtration by regions. However,
sometimes this behaviour is undesirable. So, it can be disabled by setting the
attribute `use-for-isocode-filtration` to the `false` value.


Regions
-------
The regions are used to [split](#split-rules) a ymapsdf schema on several.

The regions description is located under the path `/json2ymapsdf/regions`.

Each region is described by a tag `<region>`. The tag has the following
**required** attributes:
* `id` - an internal name of the region. The name (or several names) can be
  passed to the `json2ymapsdf` tool as an argument of the parameter `--regions`.
* `name` - a formal name of the region.
* `suffix` - the splitted region is saved into the schema with the name
  `<initial schema name>_<suffix>`.
* `isocodes` - a string with the list of iso-codes (TODO: Add cross reference to
  the standard) that forms the region. The values in the list **must** be
  separated by any number of space or/and punctuation symbols.


[wiki]: https://wiki.yandex-team.ru/maps/dev/core/wikimap/mapspro/tasks/export
