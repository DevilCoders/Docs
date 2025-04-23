yandex-market-ext-env
----------------

Общий шаблон для пакетов вида yandex-market-ext-content-preview
Установка такого пакета приведёт к включению расширенного окружения (например, content-preview) у нодных проектов, у которых есть расширенные окружения.
Смотри сюда: https://st.yandex-team.ru/MARKETVERSTKA-14635, https://st.yandex-team.ru/MARKETVERSTKA-15009

Для создния нового окружения — создаём файл по аналогии с `content-preview.py`
По умолчанию будет запущено 2 воркера. Это можно переопределить с помощью параметра workers (см. `market-cached.py`)

### Сборка пакета

К этому пакету применимы [общие инструкции по сборке][common-build-info].
Обязательно использовать параметр -C и конфиг окружения. Например, `-C market-testing.py`

### Загрузка в репозиторий

Этот пакет нужно загрузить в репозиторий [market-common][repo-link].

Информация о том [как загружать пакеты][package-upload-info].

[common-build-info]: https://github.yandex-team.ru/market/packages#%D0%A1%D0%B1%D0%BE%D1%80%D0%BA%D0%B0-%D0%BF%D0%B0%D0%BA%D0%B5%D1%82%D0%BE%D0%B2
[repo-link]: https://github.yandex-team.ru/market/packages/blob/master/README.md#market-common
[package-upload-info]: https://github.yandex-team.ru/market/packages/blob/master/README.md#%D0%97%D0%B0%D0%B3%D1%80%D1%83%D0%B7%D0%BA%D0%B0-%D0%BF%D0%B0%D0%BA%D0%B5%D1%82%D0%BE%D0%B2-%D0%B2-%D1%80%D0%B5%D0%BF%D0%BE%D0%B7%D0%B8%D1%82%D0%BE%D1%80%D0%B8%D0%B9
