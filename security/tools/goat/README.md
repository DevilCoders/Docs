# Golang Arcadia Toolkit

Простенький утиля для облегчения жизни с Golang в Аркадии.

На текущий момент поддерживает следующие команды:

  - `goat fix` - поправит ya-мейки (сгенерит не достающие и т.д.) с помощью `yo fix`
  - `goat bench` - запустить бенчи с переданными флажками
  - `goat fmt` - бьютифаит код (включая сортировку импортов с помощью `goimports`)
  - `goat lint` - запустит линтер с минимально принятым Аркадийным конфигом
  - `goat install` - аналог `go install`. Собирает текущий `GO_PROGRAM` таргет и складывает получившийся бинарь в `$GOPATH/bin`
  - `goat self-update` - обновляет goat до последней доступной версии. **Внимание:** директория с исполняемый файлом должна быть доступна на запись


## Где взять

  - можно собранный бинарь из sectools: https://tools.sec.yandex-team.ru/goat
  - можно собранный бинарь из SB: https://sandbox.yandex-team.ru/tasks?author=buglloc&type=BUILD_SECURITY_TOOL_ARC&desc_re=Goat&limit=20
  - или собрать самому :)

## Project config

Проект может иметь собственный конфиг.

Проектный конфиг должен иметь имя `.goat.toml` и ищется от текущей директории вверх до первого попавшегося.

Пример конфига (всегда добавлять этих оунеров в `ya.make`):
```toml
[fix]
# add "buglloc" and "g:security" as owners
owners = ["buglloc", "g:security"]

[fmt]
# use "lax" imports format (allowed custom groups and so on, default: false)
lax-imports = true
```

## Changelog

  - **0.13**: Added `goat fmt --changed`
  - **0.12**: deprecate `goat lint`
  - **0.11**: `goat bench` uses "TEST_COMMAND_WRAPPER"
  - **0.10**: `goat bench` uses "native" yatool bench :)
  - **0.9**: Removed `goat arcignore` :)
  - **0.8**: Added `goat bench`
  - **0.7**: Added `goat arcignore` command & auto `.arcignore` generation in `goat fix` command
  - **0.6**: Added `goat self-update`
  - **0.5**: Allowed to specify target for suitable commands
  - **0.4**: Added strict/lax imports format mode
  - **0.3**: Added project configs
  - **0.2**: Added `goat install`
  - **0.1**: Initial
