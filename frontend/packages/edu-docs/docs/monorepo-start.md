# Начало работы в монорепозитории

В документе описана документация по работе в монорепозитории для разработчиков образовательных сервисов. У нас есть некоторые особенности, например, отсутствует возможность пользоваться коммунальным форком.

За более подробной информацией по устройству монорепозитория и процессу работы с ним нужно обратиться к [корневому README файлу](https://github.yandex-team.ru/search-interfaces/frontend/blob/master/README.md).

## Первичная настройка

1. Сделайте форк [монорепозитория](https://github.yandex-team.ru/search-interfaces/frontend)
2. Склонируйте форк:

```bash
git clone --origin fork <имя форка> frontend
```

3. Добавьте удалённый репозиторий с монорепозиторием:

```bash
cd frontend
git remote add upstream git://github.yandex-team.ru/search-interfaces/frontend.git
```

Теперь подключено 2 удалённых репозитория:

- `fork` – форк монорепозитория
- `upstream` — сам монорепозиторий

Все ветки нужно пушить только в `fork`, а затем делать PR в `upstream` через интерфейс GitHub.

## Создание ветки

1. Получите последние изменения из `upstream`:

```bash
git fetch upstream
```

2. Отведите ветку от `upstream/master`:

```bash
git checkout -b <название ветки> upstream/master
```

3. Установите актуальную для монорепозитория версию Node.js и зависимости:

```bash
nvm install
npm install --global npm
npm ci
```

Теперь можно открыть в IDE конкретный пакет или сервис и начать работу с ним привычным вам способом.
