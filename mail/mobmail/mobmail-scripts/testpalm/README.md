## Клонирование версий

### Установка окружения
1. Установить jq: brew install jq 
2. Получить токен для работы с testpalm api: https://oauth.yandex-team.ru/authorize?response_type=token&client_id=6d967b191847496a8a7077e2e636142f

### Запуск скриптов
Для запуска скрипта нужно указать:
1. Oauth токен, 
2. Проект, откуда будут склонированы кейсы, 
3. Проект, куда будут склонированы кейсы,
4. ID кейсов, разделенные пробелом, если скрипт запущен без ключа `--range`, или id первого и последнего кейса

**Важно!** Поля должны быть указаны именно в таком порядке:
Ключ `--range` (может не быть), `oauth-token`, исходный проект, проект назначения, айди кейсов.

### Разница между скриптами
`clone_tc.sh` - клонирует кейсы при помощи ручки `testcases/clone` со всеми полями - более надежный способ, но нельзя конфигурировать
`copy_tc.sh` - получает кейс из одного проекта, удаляет поля (прилинкованные баги, таски, все фичи, теги и тд) и создает из этих данных новый кейс в другом проекте

### Примеры
1.Скопировать кейсы с id `5553, 5554, 5555, 5556` из проекта `mobmail_android` в проект `mobmail_ios`:

`sh copy_tc.sh --range AQAD-oauth-token mobmail_android mobmail_ios 5553 5556`

2.Скопировать кейсы с id `5553, 5556` из проекта `mobmail_android` в проект `mobmail_ios`:

`sh copy_tc.sh AQAD-oauth-token mobmail_android mobmail_ios 5553 5556`

3.Склонировать кейсы с id `5553, 5554, 5555, 5556` из проекта `mobmail_android` в проект `mobmail_ios`:

`sh clone_tc.sh --range AQAD-oauth-token mobmail_android mobmail_ios 5553 5556`

4.Склонировать кейсы с id `5553, 5556` из проекта `mobmail_android` в проект `mobmail_ios`:

`sh clone_tc.sh AQAD-oauth-token mobmail_android mobmail_ios '5553, 5556'`


## Получение yaml-файла из кейса

Скрипт `get_tc.py` позволяет получить yaml-файл из тест кейса 

## Установка окружение

`pip3 install -i https://pypi.yandex-team.ru/simple yandex_tp_api_client`

### Параметры запуска
- `--range` - позволяет получить все промежуточные кейсы, указав id первого кейса последовательности в параметре `--from` и последнего в параметре `--to`
- `--project`- название проекта в TestPalm, из которого будут браться кейсы
- `--from` - id кейса, начиная с которого нужно выгрузить. Используется только если передан `--range`. 
- `--to` - id последнего кейса, который нужно выгрузить. Используется только если передан `--range`. 
- `--list` - список id кейсов, разделенных запятой. Используется только если НЕ передан `--range`. 
- `--filter` - фильтр кейсов в формате `{"type":"EQ","key":"attributes.54193b6ae4b0b658a756b7b3","value":"Account switcher animation"}`
- `--path` - путь до папки, в которую нужно сохранить кейсы. По умолчанию кейсы будут сохранены в текущую директорию.

### Примеры

* Выгрузить из проекта `mobmail_ios` кейсы c `5763` до `5766` в папку `deeplink` в текущей директории

    `python3 get_tc.py --project mobmail_ios --range --from 5763 --to 5766 --path './deeplink/'`

* Выгрузить из проекта `mobmail_ios` кейсы `1`, `2`, `777` в текущую директорию

    `python3 get_tc.py --project mobmail_ios --list '1, 2,777'`
 
* Выгрузить из проекта `mobmail_ios` все кейсы по фильтру `Feature 1 = Account switcher animation` в папку `account switcher` в текущей директории

    `python3 get_tc.py --project mobmail_ios --filter '{"type":"EQ","key":"attributes.54193b6ae4b0b658a756b7b3","value":"Account switcher animation"}' --path './account switcher/'`

## Создание кейса из yaml-файла

Скрипт `create_tc.py` позволяет создать кейс из yaml-файла

## Установка окружение

`pip3 install -i https://pypi.yandex-team.ru/simple yandex_tp_api_client`

### Параметры запуска

- `--recursive` - позволяет создать кейсы из всех файлов из указанной в параметре `--path` папки и ее подпапок
- `--project` - название проекта TestPalm, в котором будут созданы кейсы
- `--path` - путь до директории, в которой лежат кейсы

### Примеры

* Создать тесткейсы из yaml-файлов в папке `./deeplink` и во всех ее подпапках в проекте `mobmail_ios`

    `python3 create_tc.py --project mobmail_ios --recursive --path './deeplink/'`

* Создать тест кейс из yaml-файлов текущей папки в проекте `mobmail_ios`

    `python3 create_tc.py --project mobmail_ios`

## Удаление связей кейсов с тикетами из Трекера

Скрипт `delete_link.py` позволяет удалить связи тесткейса в тикетами из Трекера

## Установка окружение

`pip3 install -i https://pypi.yandex-team.ru/simple yandex_tp_api_client`

Перед запуском нужно указать свой oauth-токен в константу `TESTPALM_TOKEN`

Токен  можно получить здесь: https://oauth.yandex-team.ru/authorize?response_type=token&client_id=6d967b191847496a8a7077e2e636142f

### Параметры запуска
- `-p` - название проекта в TestPalm
- `-q` - очереди, тикеты из которых нужно отвязать. Строка с очередями, разделенными запятой

### Примеры
Удалить связь тесткейсов из проекта mobmail_android с тикетами из очередей `MOBMAILEXPIOS` и `MOBILEMAILEXP`

`python3 delete_link.py -p mobmail_android -q 'MOBMAILEXPIOS,MOBILEMAILEXP'`
