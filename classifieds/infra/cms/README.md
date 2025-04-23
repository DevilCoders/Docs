CMS
===

This service manages docker cluster.  


### Тесты
Запуск тестов:

`go test ./...`

**Для тестов необходимо:**
1. Поставить `openssl@1.1`:

   `brew install openssl@1.1`

2. Прописать путь к нему в `LIBRARY_PATH` (у меня это `/opt/homebrew/opt/openssl@1.1/lib`)

3. Прописать в `local.env` секреты из https://yav.yandex-team.ru/secret/sec-01fsa0911jgxs121gveexacdrd/explore/versions
