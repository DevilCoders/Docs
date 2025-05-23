# tide-stats

Плагин к tide для генерации отчета о существущих тестах

## Пример отчета

```
┌────────────────────────┬──────────┬─────────────┬───────┬────────────┬─────────┐
│ Tool                   │ Features │ Experiments │ Files │ Test Cases │ Tests ▼ │
├────────────────────────┼──────────┼─────────────┼───────┼────────────┼─────────┤
│ hermione               │ 24       │ 5           │ 246   │ 697        │ 711     │
├────────────────────────┼──────────┼─────────────┼───────┼────────────┼─────────┤
│ testpalm               │ 429      │ 427         │ 2147  │ 8351       │ 9361    │
└────────────────────────┴──────────┴─────────────┴───────┴────────────┴─────────┘
```

## Использование

```
tide stat
```

- `--type [type]` — название типа тестов для подсчета тестов  (`'integration'`|`'e2e'`)
- `--group [key]` — ключ, по которому будут сгруппирован результат (`'tool'`|`testpalmDataKey`, default: `'tool'`)  
 где `testpalmdatakey` — ключ из YML-файла (`tlds`, `v-team` и другие)
- `--tool [tool]` — название инструмента для подсчета тестов для группировки не по `'tool'` (`'testpalm'`|`'hermione'`|`null`, default: `'testpalm'`)
- `--sort [column|tool.column]` — путь до столбца, по которой будут отсортированы строки (default: `'testpalm.tests'`)
- `-n, --max-count [number]` — максимальное число строк выводимых в таблице, остальные объединяются в одну строку (default: `0`)
- `-h, --help` — вывод помощи
