# Translation data

This directory contains perl scripts to translate names from foreign languages to Russian.

This data is used by Garden `ymapsdf` module on `translation` stage:
https://a.yandex-team.ru/arc/trunk/arcadia/maps/garden/modules/ymapsdf/lib/translation

The module takes it from Sandbox resource: https://sandbox.yandex-team.ru/resource/888295998/view

In order to update the resource do the following:

```
tar tvf translation-data.tar.gz
ya upload translation-data.tar.gz
```

Update resource id in the following place:
https://a.yandex-team.ru/arc/trunk/arcadia/maps/garden/modules/ymapsdf/lib/ya.make?rev=6435153#L142
https://a.yandex-team.ru/arc/trunk/arcadia/maps/garden/tools/translation/tests/ya.make#L19
