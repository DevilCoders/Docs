# CLI

Для работы с Огородом из консоли потребуется программа `garden`.

## Установка

{% list tabs %}

- Ubuntu Linux

  Шаг 0. Убедиться, что запущен ssh-агент и ssh-ключ прописан на Staff.

  Шаг 1. Установить клиент
  ```bash
  sudo apt-get install yandex-maps-garden-cli-launcher
  ```

  {% note info "Если на хосте отсутствуют deb-репозитории yandex-musl" %}

    Шаг 1. Прописать в /etc/apt/sources.list.d/yandex-musl.list следующее:
    ```bash
    deb http://yandex-musl.dist.yandex.ru/yandex-musl unstable/all/
    deb http://yandex-musl.dist.yandex.ru/yandex-musl unstable/$(ARCH)/
    deb http://yandex-musl.dist.yandex.ru/yandex-musl testing/all/
    deb http://yandex-musl.dist.yandex.ru/yandex-musl testing/$(ARCH)/
    deb http://yandex-musl.dist.yandex.ru/yandex-musl prestable/all/
    deb http://yandex-musl.dist.yandex.ru/yandex-musl prestable/$(ARCH)/
    deb http://yandex-musl.dist.yandex.ru/yandex-musl stable/all/
    deb http://yandex-musl.dist.yandex.ru/yandex-musl stable/$(ARCH)/
    ```
    Шаг 2. Установить пакет с ключами
    ```bash
    sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 7FCD11186050CD1A
    sudo apt-get update && sudo apt-get install yandex-archive-keyring
    ```

  {% endnote %}

- Other

  Собрать и использовать `garden` тул из репозитория
  ```bash
  ya make -r maps/garden/tools/garden_cli/bin
  ```

{% endlist %}

## Использование

Актуальное описание команд приложения `garden` доступно через опцию помощи:
```bash
garden --help
```

Сценарии использования тулы для работы над эксперименами описаны на [отдельной странице](experiments.md).

## Обновление

Тул `garden` обновляется автоматически, если
* тул запущен в первый раз
* тул запущен с опцией `--update`
* последняя проверка на наличие изменений была сделана более суток назад.

Для запуска тулы в режиме обновления потребуется правильная настройка `ssh-agent`
(ssh-подпись будет использоваться для получения секретов из Секретницы и обмена ключа
на OAuth-token для скачки обновления из Sandbox).
