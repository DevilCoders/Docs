# Запуск бекенда

## Подготовка

Переходим в корень репозитория:

```(bash)
cd ~/arcadia/
```

В начале необходимо собрать бекенд:

```bash
ya make --build=debug drive/backend/server
```

Далее собираем консольную утилиту:

```bash
ya make --build=release drive/devops/cli
```

## Запуск

Для запуска пользуемся командой:

```bash
./drive/devops/cli/cli start-backend
```

Бекенд берет свой бинарь из `~/arcadia/drive/backend/server/server`.

Конфигурация будет взята из `~/arcadia/drive/backend/configs/`.

По умолчанию бекенд будет запущен в `testing` окружении (меняется через опцию `--environ ENV`) на `10000` порту (меняется через опцию `--port PORT`).

Конфигурация и логи будут находиться в `~/.drive-backend/testing/`.

В качестве `CType` будет установлен `${USER}_cli` (можно поменять через опцию `--ctype CTYPE`).

При запуске Prestable будет дополнительно настроен биллинг:

  * Хост `trust-payments.paysys.yandex.net` будет заменен на `trust-payments-test.paysys.yandex.net`.
  * В `ActiveQueue` будет указано значение `tests`.

## Остановка

Для остановки пользуемся командой:

```bash
./drive/devops/cli/cli stop-backend
```

## Quick version

Используем скрипт
```
./drive/backend/scripts/start.sh [--env ENV]
```

## Поддержанные окружения
- testing – Carsharing Testing
- prestable – Carsharing Prestable
- drivematics_testing – Drivematics Testing
- drivematics_prestable – Drivematics Prestable
