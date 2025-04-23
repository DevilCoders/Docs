# ugcserver-e2e

Образ ugcserver для запуска в e2e тестах.

Сам сервер и конфиги должны подкладываться из релизных sandbox-задач `BUILD_UGC_DB_BACKEND`.

- Ресурс `UGC_DB_BACKEND_EXECUTABLE` в `/ugc/ugcserver`.
- Ресурс `UGC_COMPONENT_SERVER_CONFIG_DIR` в `/ugc/config`.

## Использование

- `make build` - собрать образ,
- `make run` - запустить собранный образ,
- `make release` - собрать, поставить тэги и опубликовать образ.
