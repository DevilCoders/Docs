json-schema-diff-validator
==========================

This package allows comparision of two versions of schema file and detect any breaking change. The new version is considered as non-backward compatible when

* a new node with minimum requirement is added.
* when a node is removed.
* when a node is replaced.

Usage
-----

```
npm install json-schema-diff-validator -g
json-schema-diff-validator oldschema.json newschema.json
```

This will return with exit code 0 if there is no breaking change.
Throws an exception if there is a breaking change

```
Error: The schema is not backward compatible. Difference include breaking change =
[{"op":"remove","path":"/definitions/code_inline_node/allOf/1/properties"},{"op":"replace","path":"/definitions/code_inline_node/allOf/1/type","value":"string"}]
```

### To use it in code

```
 const difftool = require('json-schema-diff-validator')
 #to validate files
 difftool.validateSchemaFiles(file1,file2);
 #to validate json objects
 difftool.validateSchemaCompatibility(oldjson , newjson)
```

Supported options:

 * allowNewOneOf - new oneOf/anyOf items are considered a backwards compatible change (`false` by default)
 * allowNewEnumValues - new enum values are considered a backwards compatible change (`false` by default)
 * allowReorder - reordering of `anyOf` items are considered a backwards compatible change (`false` by default)
 