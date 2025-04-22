### О скрипте
Скрипт проходится по кейсам выбранного проекта и переразмечает их Feature Priority и Case Priority,
в зависимости от аудитории и продуктового веса.
Продуктовый вес фичи определяется в дополнительных конфигурационных файлах (`features_iOS.json`, `features_Android.json`)
Аудитория фичи определяется исходя из аудитории событий, связанных с этой фичой, также указанных в дополнительных конфигурационных файлах (`features_iOS.json`, `features_Android.json`)

### Используемые зависимости
Для использования скриптов необходимо через пип установить следующие зависимости:
* Питоновский клиент для ST `pip3 install -i https://pypi.yandex-team.ru/simple/ startrek_client`
* Библиотеку yandex-yt  `pip3 install -i https://pypi.yandex-team.ru/simple/ yandex-yt`
* Библиотки для работы со статистикой `pip3 install -i https://pypi.yandex-team.ru/simple/ python-statface-client`
* Библиотеку для работы с TestPalm `pip3 install -i https://pypi.yandex-team.ru/simple yandex_tp_api_client`

Для работы скрипта необходимы следующие токены:
* токен для TP - можно получить по [этой ссылке](https://oauth.yandex-team.ru/authorize?response_type=token&client_id=6d967b191847496a8a7077e2e636142f)
* токен для работы со Stat-ой  - можно получить по [этой ссылке](https://oauth.yandex-team.ru/authorize?response_type=token&client_id=801af94c94e040848ebe206086a7a4e2)

### Запуск скрипта
`python3 Run_assessors.py -p iOS` - запускает разметку кейсов для проекта iOS по заданному конфигу

Параметры запуска:
`-p: iOS` или `-p: Android`
