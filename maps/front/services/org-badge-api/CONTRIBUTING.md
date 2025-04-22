# Бейдж организации

Технологии:
* React
* Typescript

## Требования к системе

- node.js (для избежания проблем совместимости - версии 10.12)

## Разработка

### Установка

```sh
git clone git@github.yandex-team.ru:maps/org-badge-api.git ~/www/org-badge-api
cd ~/www/org-badge-api
# Настройка машины для локальной разработки.
make local
make deps
```

### Запуск

```sh
make dev
```

Открыть `http://localhost:8080/` в браузере.

### Создание тега

```sh
make arc-tag
```


### Production

```sh
make deploy-production
```