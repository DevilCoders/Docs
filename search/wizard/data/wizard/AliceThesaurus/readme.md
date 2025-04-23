## How to make *synonyms.gzt.bin*
Prepare *synonyms.tsv* file
- first column is *to* word (synonym for word in query), should be lemma
- second column contains *from* words separated by ';' (for all these words will be add synonym)
- third column is *ext_type*: https://a.yandex-team.ru/arc/trunk/arcadia/search/wizard/common/thesaurus/proto/thesaurus_types.proto?rev=r8176907#L22

Download *synonyms.tsv*
```bash
YT_PROXY=hahn yt read //home/voice/deemonasd/DIALOG-7355/thesaurus/2022-01-14/result --format '<columns=[to;from;type]>schemaful_dsv' > synonyms.tsv
```

Convert *synonyms.tsv* to gzt format
```bash
search/wizard/data/wizard/AliceThesaurus/utils/make_gzt/make_gzt -i synonyms.tsv -o synonyms.gzt --format tsv_to_from
```

Compile *synonyms.gzt* to gzt.bin format
```bash
dict/gazetteer/compiler/gztcompiler synonyms.gzt synonyms.gzt.bin -A {ARCADIA_ROOT}
```

Speed of gzt.bin can be tested via dict/gazetteer/printgzt

## How to make *fixlist.gzt.bin*
This file will by automatically compiled from *fixlist.tsv*
- first column is *syn_type*
- second column contains *words* separated by ';'
More details in tool search/wizard/data/wizard/AliceThesaurus/utils/make_gzt/__main__.py (--format fixlist)
