# CodeSearch

Клиент для [CodeSearch](https://cs.yandex-team.ru).

## Usage

```py
lm_set_id = 1
cs = CodeSearch(single=True, regexp=': {},'.format(lm_set_id), file_regexp=r"linear_set\.json", wsvn=True, json=True)
response = cs.search()
if response.results:
    url = response.results[0]['url']        # arcanum url
    file = response.results[0]['file']      # yabs/utils/experiment-switcher/linear_set.json
    source = response.results[0]['source']  # "ID": 1
```
