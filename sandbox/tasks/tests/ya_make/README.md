This test ensures that [sandbox/projects/ya.make](https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/projects/ya.make)
contains only first-level PEERDIRs (e.g. sandbox/projects/foobar), except for the ones that existed before.

The legacy yet-acceptable nested PEERDIRs are taken from `whitelist.json`. Please update it regularly with an enclosed utility:

```bash
arcadia/sandbox/tasks/tests/ya_make$ ya make updater
arcadia/sandbox/tasks/tests/ya_make$ updater/updater -i ../../../projects/ya.make -o whitelist.json

Found 1490 offenders for the whitelist...
Updated!
```
