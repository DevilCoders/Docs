## Общие компоненты для Я.Аренды

### Как сделать новый api ключ для elasticsearch
1. Зайти в админку kibana для нужного кластера elasticsearch (логин пароль брать из секретов elastic-rent-prod или elastic-rent-test соответственно)
например: https://yc.yandex-team.ru/folders/foo4nrk07dl14udeb4js/managed-elasticsearch/cluster/mdbvrm87vp21i5pvtbig/view
и в левом боковом меню выбрать kibana
2. В интерфейсе kibana выбрать Dev Tools
3. В консоли кибана выполнить запрос
  ```
  POST /_security/api_key
    {
    "name": "rent-api-key",
    "role_descriptors": {
      "rent_rw": {
        "cluster": [ ],
        "index": [
          {
            "names": ["flat-presets-*"],
            "privileges": ["read", "write", "create_index"]
          }
        ]
      }
    }
  }
  ```
4. В полученном ответе вида
  ```
  {"id":"xxx","name":"rent-api-key","api_key":"yyy"}
  ```
  взять значения полей id и api_key и склеить из них ключ
  ```
  echo -n "xxx:yyy" | base64
  ```
5. положить base64-encoded ключ в секрет elastic-rent-prod или elastic-rent-test соответственно с названием api_key
