For speed `--nonet` option of the `xmllint` tool is used. To achieve this all `schemaLocation`
attributes in xml schemas are replaced to local paths.

Speed improvement for the one `xmllint --timing` run:
* Before: ~1400 ms
* After: ~47 ms
