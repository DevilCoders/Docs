# Payment SDK Backend
Бекенд нативной формы оплаты

### Деплой

Проект в деплое - https://deploy.yandex-team.ru/projects/payments-sdk

#### CI/CD настроен средствами Аркадии:
В файле a.yaml хранится конфигурация ([доки](https://docs.yandex-team.ru/ci/basics)). В UI Аркадии сборка выглядит [так](https://a.yandex-team.ru/projects/paymentsdk-backend/ci/releases/timeline?dir=mail%2Fpayments-sdk-backend&id=payments-sdk-backend-release).
Текущая логика такая:
1. При вливании ветки в ``trunk`` запускается билд
2. Успешная сборка выкатывается в [тестинг](https://deploy.yandex-team.ru/stages/payments-sdk-backend-testing) автоматически
3. Выкладка в [прод](https://deploy.yandex-team.ru/stages/payments-sdk-backend-production) происходит по нажатию кнопки на flow CI.

[Пример flow](https://a.yandex-team.ru/projects/paymentsdk-backend/ci/releases/flow?dir=mail%2Fpayments-sdk-backend&id=payments-sdk-backend-release&version=8)

#### Возможен и ручной деплой (не рекомендуется):
1. Создаем релизную ветку `releases/mail/payment-sdk-backend/1.*.*`. Заменить звездочки на версию
2. В файле `package/package.json` меняем префикс версии, коммитим в ветку
3. Пушим командой `arc push -u releases/mail/payment-sdk-backend/1.*.*`
4. Создаем пакет через sandbox, копируем таску и проставляем правильную релизную ветку: https://sandbox.yandex-team.ru/task/904821330
5. Полученный tag указываем в yaml deploy-файлов
6. Выкатываем через команды из Makefile
7. Отводим от транка ветку для бампа yaml-спек, вносим туда изменения `package.json` и `yaml-файлов` (cherry-pick, rebase, руками и т.д.). Открываем pr

При необходимости можно собрать пакет следующей командой:
`ya package --docker --docker-repository payments-sdk-backend package/package.json`

**ВАЖНО**: не делайте так для прода, только для быстрой выкатки на тестинг

### Структура проекта
* `internal/app.go` – инициализация приложения
* `internal/api` – реализация HTTP API
* `internal/config` – конфиг всего приложения
* `internal/logic` – реализация бизнес-логики приложения
* `internal/logic/models` – модели бизнес-логики
* `internal/interactions` – клиенты для хождения во внешние сервисы
* `internal/utils` – общепроектные утилиты
* `cmd` – entrypoint бекенда
* `http` – примеры запросов к API в формате `IDEA`

### Как запустить?
#### Если у вас нет своего tvmtool
1. Ставим `watchdog`: ```pip install watchdog```
1. Кладеём [секрет от TVM](https://abc.yandex-team.ru/services/paymentsdk/resources/?view=consuming&layout=table&supplier=14&type=47) приложения в `./.tvm.key`: ```echo "<tvm_secret>" > ./.tvm.key```
1. Запускаем: ```make run```

Изменения во всех файлах будут отслеживаться и сервер автоматически будет пересобираться

#### Если у вас свой tvmtool
1. Добавьте новую секцию согласно `./run_local.sh`
2. Запускаем: `CONFIG_PATH=./package/etc/payments-sdk-backend/development.yaml make build_and_run`

### Как обновить mock'и
Заходим в директорию, где находиться интерфейс, мок которого хотим обновить и запускаем команду `scripts/mockgen.sh <interface>`.

Пример:

```bash
cd internal/interactions/trust
# Обновляем mock Trust Client'a
../../../scripts/mockgen.sh Client
```
