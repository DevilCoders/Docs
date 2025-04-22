# Hotes suggest builder

See [HOTELS-4898](https://st.yandex-team.ru/HOTELS-4898)


## Dictionary building

Stages:

### 1. Build .txt dictionary with this tool

```shell script
ya make bin && bin/hotels_suggest_builder  --yql-token $(cat ~/.yql/token) --yt-token $(cat ~/.yt/token)  --days 4 --cleanup-strategy KeepLastN:3
```

### 2. Build binary dictionary with Suggest data builder

[Suggest data builder](https://a.yandex-team.ru/arc/trunk/arcadia/quality/trailer/suggest/data_builder)
is a tool developed by suggest command.

```shell script
ya make . && for dict in region_suggest search_suggest top_hotels_suggest ; do ./suggest-data-builder -A -r ${ARCADIA_ROOT}/travel/hotels/tools/hotels_suggest_builder/build/$dict/ready.txt -g ${ARCADIA_ROOT}/travel/hotels/tools/hotels_suggest_builder/build/$dict/groups.txt -s ${ARCADIA_ROOT}/travel/hotels/tools/hotels_suggest_builder/build/$dict/streams.txt -d ${ARCADIA_ROOT}/travel/hotels/tools/hotels_suggest_builder/build/$dict/data.txt -o /home/sulim/arc/idea-projects/suggest/hotels/$dict ; done
```

### 3. Upload binary dictionaries to sandbox

```shell script
SUGGEST_TYPE=hotels && SANDBOX_TYPE=SUGGEST_DICT && ya upload -d "Upload ${SUGGEST_TYPE} from $(hostname) by $(whoami)" --token $(cat ~/.sandbox/token) --owner sulim -Aname="${SUGGEST_TYPE}" -Aautodeploy=yes --ttl inf -T "${SANDBOX_TYPE}" hotels
```


## Documentation

[Suggest documentation [RUS]](https://wiki.yandex-team.ru/suggest/)
