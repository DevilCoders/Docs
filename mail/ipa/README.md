# ipa

### TVM
Чтобы добавить запуск tvmtool нужно:
1. Положить в `.tvm.key` секрет.
2. В `run_local.sh` прописать `self_tvm_id`.
Между перезапусками нужно самостоятельно удалять `.tvm.json`, если была ошибка запуска tvmtool.


### Локальный запуск
1. `make build_bin` - каждый раз, когда меняются `ya.make` файлы.
2. `make wl_runserver` - запускает tvm и api под watchmedo. Каждое изменение .py файла перезапустит приложение, не
   пересобирая его. Т.к. конфиги .conf кладутся в бинарь, при их изменении придется его пересобирать.
3. `make dev-unit`, `make dev-functional` - запускает тесты, без пересборки. В отличие от `ya make -A` и `make test`
   запускает `pytest` напрямую, поэтому принимает на вход другие параметры и в теории может работать немного иначе.
   Примеры запуска: `make dev-unit ipa/tests/unit/mappers`, `make dev-functional -- -x ipa/tests/functional`.
   P.S. не стоит одной командой для unit-тестов запускать функциональные, потому что у них могут быть разные
   зависимости.
