# DCSaaP Nirvana Operations Warehouse (powered by Valhalla 3)

## Что это?

Хранилище Nirvana-операций, которые используются в сверках.
Позволяет хранить операции в коде, проводить над ними ревью, тестировать и выкладывать в Nirvana через CI.

## Основная документация по Valhalla

Документацию можно найти по следующей ссылке: https://docs.yandex-team.ru/vh3/.

## Структура проекта

```
├── bin/
├── graphs/
├── operations/
├── tests/
├── a.yaml
├── local-deploy.py
├── Makefile
├── README.md
├── requirements.txt
├── requirements.unittest.txt
├── setup.cfg
├── setup.py
└── ya.make
```

{% list tabs %}

- bin

  Входная точка в хранилище, собирается и используется Valhalla для запуска в Nirvana.

- graphs

  Хранилище графов (`workflow`).
  Может содержать как наши, так внешние графы (графы, кода которых нет в Arcadia).
  Такие графы можно использовать, если предварительно описать их сигнатуру с помощью `make import` или `vh3 import`.

- operations

  Хранилище операций. Может содержать как наши, так и внешние операции (операции, кода которых нет в Arcadia).
  Такие операции можно использовать, если предварительно описать их сигнатуру с помощью `make import` или `vh3 import`.
  Дополнительно хранит исходный код всех наших операций.

- tests

  Тесты на код операций и графов.

- a.yaml

  Дополнительный `a.yaml` файл,
  который привносит возможность обновлять операции по коммиту и создавать релизы Nirvana-графов.

- local-deploy.py

  Скрипт, который помогает развернуть локальное окружение.
  Получает токены и настраивает окружение Valhalla (`~/.vh3/profile.yaml`).

- Makefile

  Основная входная точка для управления локальным окружением и работой с хранилищем.
  Например, развернуть окружение можно одной командой: `make`.

{% endlist %}

## Разворачивание окружения

### Автоматическое разворачивание окружения

Для автоматического разворачивания окружения потребуется `GNU make` и `Python v3.8+` (минимальная версия для использования Valhalla).

1. Из директории хранилища запускам `make`, выбираем тип виртуального окружения, которое создаст скрипт (по-умолчанию используется стандартный `python -m venv`:
```bash
> make
Do you want to deploy "ya ide venv" (y) or native "python -m venv" (N)?
```
2. После этого окружение будет установлено в директорию `.env`, установятся зависимости:
```bash
/usr/bin/env python3 -m venv .env
...
./.env/bin/python3 -m pip install -i https://pypi.yandex-team.ru/simple/ -e /Users/srg91/dev/projects/dcsaap/nirvana/vh3
...
Successfully installed Jinja2-3.0.3 MarkupSafe-2.1.1 XlsxWriter-3.0.3 dcsaap-vh3-0.0.1.dev0 et-xmlfile-1.1.0 ijson-3.1.4 openpyxl-3.0.10 startrek_client-2.5 yandex_tracker_client-2.3
```

3. Далее скрипт попросит ввести OAuth-токен Nirvana и YT, если они отсутствуют на компьютере.
```bash
[Nirvana OAuth token] Token not found at "/Users/srg91/.nirvana/token". You can find one at next url: https://oauth.yandex-team.ru/authorize?response_type=token&client_id=637ca17604cb4dfa90b262952c00b1e9.
[Nirvana OAuth token] Please, enter your token:
[Nirvana OAuth token] Token was written to "/Users/srg91/.nirvana/token".

[YT OAuth token] Token not found at "/Users/srg91/.yt/token". You can find one at next url: https://oauth.yt.yandex.net.
[YT OAuth token] Please, enter your token:
[YT OAuth token] Token was written to "/Users/srg91/.yt/token".
Everything is configured. You can find additional information at https://docs.yandex-team.ru/vh3/usage/cli.
```

4. После получения токен потребуется указать Valhalla, что мы хотим использовать локальную Аркадию для запуска:
```bash
[vh3 profile.yaml] Profile not found at "/Users/srg91/.vh3/profile.yaml", new one will be created.
[vh3 profile.yaml] Please, provide arcadia root path: [default: /Users/srg91/dev/projects/dcsaap]
---
quota: default
arcadia: !object:vh3.arcadia.Local
    root: /Users/srg91/dev/projects/dcsaap
Everything is configured. You can find additional information at https://docs.yandex-team.ru/vh3/usage/cli.
```

Подробнее про `~/.vh3/profile.yaml` можно прочитать [в документации](https://docs.yandex-team.ru/vh3/usage/cli#podgotovka).

## Ручное разворачивание окружения

В целом про установку так же написано [в документации](https://docs.yandex-team.ru/vh3/quickstart#ustanovka).

1. Устанавливаем `virtualenv` или используем свой:
```bash
python3 -m venv .env
source .env/bin/activate
```

2. Устанавливаем `vh3` из исходного кода:
```bash
pip3 install -i https://pypi.yandex-team.ru/simple/ -e ${ARCADIA_ROOT_DIR}/nirvana/vh3
```

3. Устанавливаем хранилище и зависимости:
```bash
pip3 install -e . -r requirements.txt -r requirements.unittest.txt
```

Основное, что стоит учесть, структура проекта шаблонная для `vh3`, поэтому верхнеуровнево мы получаем два пакета: `graphs` и `operations`.

4. Получаем токены

- Nirvana:
  - URL: https://oauth.yandex-team.ru/authorize?response_type=token&client_id=637ca17604cb4dfa90b262952c00b1e9
  - Кладём в: `~/.nirvana/token`
  - Обязательно правим права: `chmod 0600 ~/.nirvana/token`

- YT:
  - URL: https://oauth.yt.yandex.net
  - Кладём в: `~/.yt/token`
  - Обязательно правим права: `chmod 0600 ~/.yt/token`

5. Указываем `vh3` расположение локальной аркадии:
```bash
mkdir -p ~/.vh3 && ~/.echo "
---
quota: default
arcadia: !object:vh3.arcadia.Local
    root: ${ЗДЕСЬ УКАЗЫВАЕМ ПУТЬ ДО АРКАДИИ}
"
```

6. Можно пользоваться.

## Релизы

Релизы выполняются через Arcadia CI. Операции обновляются каждый коммит, если в них произошли изменения.
Графы выкладываются через полноценные релизы.
Возможно, в будущем, стоит объединить эти два процесса и выполнять выкладку только через релизы, а возможно и с подтверждением.

## Основные команды

- `make`
  - Команда аналогична запуску `make deploy-local`, выполняет разворачивание локального окружения и обновляет токены (если это требуется);
  - Фактически команда состоит из двух подкоманд: `make env` и `make deploy-vh3-config`;
- `make env`
  - Команда выполняет разворачивание локального окружения;
  - На выбор можно установить окружение от `ya ide venv`, либо самое обычное `python -m venv`;
- `make deploy-vh3-config`
  - Проверяет, что все токены и конфиги на местах, если что - просит или пробует изменить;
- `tests`
  - Выполняет запуск тестов (для обычного окружения - запуск pytest, для Аркадийного - `ya make -t`);
- `clean`
  - Полностью очищает рабочее окружение. Состоит из команд: `clean-env`, `clean-vh3`, `clean-tests`, `clean-build`;
- `make draft-block OPERATION=python_cat`:
  - Позволяет создать черновик графа из операции из кода, который можно запустить в Nirvana;
  - Не создаёт реальную операцию;
- `make run-block OPERATION=python_cat`:
  - Позволяет создать граф из операции и сразу же его запустить в Nirvana;
- `make draft GRAPH=concatenate_files`:
  - Позволяет создать черновик графа из кода;
- `make run GRAPH=concatenate_files`:
  - Позволяет создать граф из кода и сразу же его запустить в Nirvana;
- `make import-block OPERATION=2fdd4bb4-4303-11e7-89a6-0025909427cc`:
  - Позволяет увидеть и использовать сигнатуру внешней операции из Nirvana;
- `make import-graph GRAPH=a2f54b83-f6fc-4a0b-a79c-fbc30a587e1d`:
  - Позволяет увидеть и использовать сигнатуру внешнего графа из Nirvana;
- `make import OPERATION=https://nirvana.yandex-team.ru/operation/b59a3f36-a467-4951-b596-efe2055188b8`:
  - Позволяет получить сигнатуру графа или операции по ссылке.
