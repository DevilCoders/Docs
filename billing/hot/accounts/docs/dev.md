## Локальная разработка

### Запуск линтеров
Помимо аркадийных линтеров, встроенных в `ya make` у нас есть дополнительные наши.
Они запускаются локально через `make lint`.

Можно настроить автоматический запуск при каждом коммите, который включает изменения из данной директории.
Для этого нужно в `~/.arcconfig` добавить следующие строчки
```
[pre-commit-hook "billing/hot/accounts"]
    hook = billing/hot/accounts/.pre-commit-hook.sh
```
Также можно пропустить проверку при коммите с помощью флага `-n`


### Тестирование
Всё построено на стандартных аркадийных инструментах - запускаем `ya make -tt` и тесты проходят:
* Большая часть тестов использует рецепт с локальным постргесом - см. [пример](../pkg/core/actions/impl/gotest/ya.make).
* Для некоторых тестов используется gomock, соответственно для них нужно запускать кодогенерацию, как-то так:
   * `ya tools mockgen -source pkg/storage/storage.go -package mock -destination mock/storage.go`
   * `ya tools mockgen -source pkg/core/actions/actions.go -package mock -destination mock/actions.go`

Для локальной отладки тестов через goland нужно:
* Сгенерировать крайне очевидной командой заглушки для используемых протобуфов `ya make --replace-result --add-result .go` (упёрто из [официального FAQ](https://wiki.yandex-team.ru/devrules/go/#faq)).
* Поднять базу локально `make start-db`.
* Прописать переменную окружения DB_DSN как она указана в Makefile'е.

Просто запустить приложение локально:
* `make start-db`
* `make runapi`

Теоретически можно аналогично с тестами дебажить целиком запущенное приложение.

Для остановки базы:
* `make stop-db`

### Линтеры
1. Есть настроенный и плюс-минус поддержанный в актуальном состоянии golangci. Запускается на данный момент только локально: `ya tool golangci run`. Для корректной работы нужно починить протобуфы, см выше.
1. Автоматическое исправление импортов по стайлгайду: `ya tool yoimport -w -local a.yandex-team.ru/billing/hot/accounts pkg/storage/db/shards.go`. Можно запускать на директории, все .go файлы отформатируются рекурсивно. Для форматирования всего есть shortcut `make yoimports`
1. Автоматическая форматирование ya.make'ов: `ya tool yo fix .`
1. Автоформатирование - можно из голанда либо `ya tool gofmt -w pkg/core/entitysettings/impl/config.go`
