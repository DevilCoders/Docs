## picrobot_state_decoder

Cтейт пикробота хранится в сжатом состоянии.
Тулза для декодирования стейта пикробота.

Входная таблица должна содержать следующие атрибуты:
1) `Id` - `url` картинки
2) `State` - закидрованный стейл
3) `Codec` - чем закодировали стейт

Выходная таблица содержит:
1) `url` - `url` картинки для которой раскодировали стейт
2) `state` - раскодированный стейт

Пример использования:
```
fadeevsergey@dev-idx01vd:~/arcadia/market/idx/datacamp/dev/picrobot_dump_decoded_state$ ./picrobot_dump_decoded_state --yt-proxy arnold --state-path //home/market/development/indexer/fadeevsergey/picrobot_state_decoder/state_in --output-table //home/market/development/indexer/fadeevsergey/picrobot_state_decoder/state_out_1
```

Как сгенерировать схему для использования декодированного стейта в yql запросах

```
fadeevsergey@dev-idx01vd:~$ ya yql proto_field -p ~/arcadia/market/idx/datacamp/picrobot/processor/proto/state.proto -m NMarket.NPicrobot.TPicrobotState > ~/meta.json
```

Пример получившейся схемы и ее использования в yql: https://yql.yandex-team.ru/Operations/YnJzVq5OD68Sj618lRdGve5Jl17IxCjXZ6ePbq_AI1c=
