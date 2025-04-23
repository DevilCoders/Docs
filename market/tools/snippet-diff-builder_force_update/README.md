# Snippet diff builder fix state

Утилита, которая принимает на вход ferryman-state и state нашего snippet-diff-builder и чинит:
1. Отправляет на удаление документы, которые есть только в ferryman-state;
2. Документы, которые есть в нашем state, но нет в ferryman-state удаляются из нашего state, чтобы они были вновь загружены в след. итерации snippet-diff-builder.

## Запуск
./snippet-diff-builder
  --yt-proxy <ex.:hahn.yt.yandex.net>
  --yt-token-path <path to token, ex.:~/.yt/token>
  --input-ferryman-state-table ex.:"//home/saas/ferryman-stable-kv/market_snippet/final/2019-04-12T10:55:46.623844Z/state_prev/main"
  --input-ferryman-state-table ex.:"//home/saas/ferryman-stable-kv/market_snippet/final/2019-04-12T10:55:46.623844Z/input_json/0-1555062780000000"
  (--input-ferryman-state-table может быть сколько угодно)

  --input-state-table <path to current snippet state table, ex.:"//home/market/production/indexer/gibson/saas_snippet/state"
  --output-diff-table <path to output ferryman table, ex.: "//home/market/development/indexer/ferryman/target.prod.bin">
  --output-state-table <path to new state ex."//tmp/zhnick/new_state">
