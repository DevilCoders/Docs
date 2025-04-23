# norm_words_type.trie.tsv

See https://st.yandex-team.ru/SEARCHSPAM-10869

Trie [1] with dirty language markers', (works with single words only!)

Expected format:

    <UTF-8 lowercase word> \t <word_type>

Where `word_type` is a number that corresponds to [`TDirtyLangProto::EDirtyLangType`][2].

[1]: https://a.yandex-team.ru/arc/trunk/arcadia/tools/triecompiler?rev=2559265
[2]: https://a.yandex-team.ru/arc/trunk/arcadia/search/wizard/rules/proto/dirty_lang.gztproto?rev=2559143#L6


# dirty_lang_fixlist.txt

Has following format:

    <UTF-8 space-separated ngram> \t <word_type>

This file is transformed into dirty_lang_fixlist.gzt during build phase with the script `prepare_gzt.py`.
