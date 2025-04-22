## Работа экспериментов в морде

### Работа сквозных экспериментов для серверного дзена
* Мы пробрасываем эксперименты в дзен через параметр `ClientExps`
* Туда попадают эксперименты из handler "Morda"
* АB флаги, чьи имена начинаются с `zen_` и имеют значение 1/'yes' пробрасываются в дзен (к ним также добавляется суффикс `:exp`)
* Если slice_name имеет префикс `zen_`, то он также пробрасывается в дзен
* Если slice_name заканчивается на `_etalon`, то такой суффикс заменяется на `:ref`, иначе работаем как с обычным аб флагои и добавляем суффикс `:exp`
* Пример:
такой эксперимент
```json
  {
    "HANDLER": "MORDA",
    "CONTEXT": {
      "MORDA": {
        "flags": [
          "_slice_name=zen_init_etalon",
          "zen_chunked_answer=1",
          "morda_test_rtb=1",
          "zen_jft=test",
          "zen_single_column=1"
        ],
        "testid": [
          "444600"
        ]
      }
    },
    "CONDITION": "desktop",
    "RESTRICTIONS": [
      {
        "services": "morda"
      }
    ]
  }
```
будет преобразован в следующий набор клиентских экспериментов для дзена
```
zen_init:ref, zen_chunked_answer:exp, zen_single_column:exp
```

