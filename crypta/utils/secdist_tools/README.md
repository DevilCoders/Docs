# Назначение

Скрипт для перевоза секретов из secdist в Yandex Vault. Так как скрипт написан в Крипта и для Крипты, то
все характерные для проектов переменные захардкожены для Крипты, например PROJECTS_BASEPATH =
'/repo/projects/crypta'. Из Секдиста секреты раскладываются в Волт в плоскую структуру, при этом в имени
секрета учитывается старая иерархия директорий проекта на Секдисте. Также скрипт наивно пытается угадать
тип секрета и записывает его в ключ и в теги. По договоренности в команде, все небуквенные и нечисловые
символы в имени секрета заменяются на символ подчеркивания. Иерархия директорий в Секдисте сохраняется
через точку. 

# Использование

Основную работу делает secdist_client.py. Чтобы бегло посмотреть возможности скрипта, можно запустить его
с ключом -h:

    $ ./secdist_client.py -h
    usage: secdist_client.py [-h] [-d SECRETS_DIR] [--dry-run [DRY_RUN]]
                             [--production [IS_PRODUCTION]] [-e EXPRESSION]
                             [-x EXCLUDE_DIRS]
    
    Script to migrate from secdist to Yandex Vault
    
    optional arguments:
      -h, --help            show this help message and exit
      -d SECRETS_DIR, --secrets_dir SECRETS_DIR
                            Relative path with desired secrets directory
      --dry-run [DRY_RUN]   Dry run mode, secrets won't be added to Vault
      --production [IS_PRODUCTION]
                            Upload secrets to production Vault, yav-test is used
                            by default
      -e EXPRESSION, --expression EXPRESSION
                            Search Regex to match particular keys
      -x EXCLUDE_DIRS, --exclude-dirs EXCLUDE_DIRS
                            Exclude directories from transferring to Yandex Vault,
                            use comma to separate


Скрипт использует ssh-ключ из запущенного на компьютере агента, поэтому позаботьтесь о том, чтобы ваш ключ
был добавлен в агент на машине, на которой вы его используете, а открыая его часть была залита на стафф.

## Опции

### Пробный запуск

    --dry-run [DRY_RUN]   Dry run mode, secrets won't be added to Vault
Позволяет посмотреть, как работает скрипт, не заливая секреты в Волт.

### Выбор директории secdist

    -d SECRETS_DIR, --secrets_dir SECRETS_DIR
    
Этим ключом можно задать путь к директории с секретами относительно проекта, из которой нужно читать
секреты. Из этой директории секреты будут читаться рекурсивно, если директория содержит поддиректории.
Если этот ключ опустить, то рекурсивно считаются все секреты из проекта.

### Выбор ключей по регулярному выражению

    -e EXPRESSION         Search Regex to match particular keys
Задает регулярное выражение, по вхождению которого в имя секрета можно указать, какие именно секреты
вы хотите залить.

### Выбор сервера Yandex Vault

     --production [IS_PRODUCTION]

Сейчас поддерживается только два сервера: тестовый и продакшон. По умолчанию ключи зальются
в тестинг https://yav-test.yandex-team.ru/
При использовании опции секреты будут заливаться в продакшон https://yav.yandex-team.ru/

### Исключение директории из чтения

    -x EXCLUDE_DIRS, --exclude-dirs EXCLUDE_DIRS
                                Exclude directories from transferring to Yandex Vault,
                                use comma to separate
Можно указать через запятую (без пробелов) точные имена директорий, которые вы не хотите заливать в Волт
