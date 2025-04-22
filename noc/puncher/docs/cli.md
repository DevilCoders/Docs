# Консольный клиент Панчера
Для выполнения массовых операций над правилами мы предоставляем консольный клиент.

## Установка
### Linux
Надо установить пакет `puncher-cli` из `common/stable`
```sh
# если репозиторий ещё не подключён
sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 7FCD11186050CD1A
sudo add-apt-repository "deb http://common.dist.yandex.ru/common stable/all/"
sudo apt-get update

sudo apt-get install puncher-cli
```
### Не linux
Нужно самостоятельно собрать себе бинарь через `ya make` из [исходников](https://a.yandex-team.ru/arc/trunk/arcadia/noc/puncher/cli).

## Аутентификация
```sh
puncher auth
```
Откроется окно браузера с запросом доступа. После разрешения доступа появится код, который надо будет ввести обратно в консоль.

## Поиск правил
```sh
puncher get --destination puncher.yandex-team.ru
```

## Просмотр изменений в доступах при смене подразделения
### По логинам
```sh
puncher diff_staff_move %dmage% @dpt_yandex_mnt_noc_dev@
```
(где "dmage" – логин сотрудника).

### По подразделениям
```sh
puncher diff_staff_move @dpt_yandex_infra_tech@ @dpt_yandex_mnt_noc_dev@
```

## Создание заявки
```sh
echo '{"sources":["%dmage%"],"destinations":["puncher.yandex-team.ru"],"protocol":"tcp","ports":["443"],"comment":"Проверка"}' | puncher create

puncher create <<END
{
  "sources":["%dmage%"],
  "destinations":["puncher.yandex-team.ru"],
  "protocol":"tcp",
  "ports":["443"],
  "locations":["office","vpn","mobile"],
  "until":"2015-03-18T16:00:00Z",
  "comment":"Проверка"
}
END
```

## Создание копии правил с другим destination
```sh
puncher get --destination puncher.yandex-team.ru --json-request |
  jq -c 'del(.rule_id)' | # make a copy, not an update
  jq -c '.destinations = ["puncher-test.yandex-team.ru"]' |
  puncher create --multiple --comment="test"
```

## Добавление нового источника в правила
```sh
puncher get --json-request --exact --source @dpt_yandex_mnt@ | jq -c '.sources += ["@dpt_yandex_mnt_noc@", "@dpt_yandex_mnt_phys@", "@dpt_yandex_mnt_security@"]' | puncher create --multiple --comment="В соответствии со структурными изменениями. Подробности тут TOOLSUP-17973"
```

## Удаление устаревшего макроса из правил
```sh
puncher get --json-request --exact --destination _C_OLD_MACRO_  | jq -c '.destinations -= ["_C_OLD_MACRO_"]' | puncher create --multiple --comment "Remove obsolete macro _C_OLD_MACRO_"
```

## Удаление правила
```sh
echo '{"rule_id": "5a61bfb134df7f463036dafa"}' | puncher delete --comment "Razobrano"

# Или несколько правил одним вызовом
puncher delete --comment "Razobrano" --multiple <<END
{"rule_id": "5a61bfb134df7f463036dafa"}
{"rule_id": "6a61bfb134df7f463036dafa"}
END
```

## Если клиент перестал работать
Если вы получаете ошибку, например, `ValueError: No JSON object could be decoded`
Попробуйте аутентифицироваться заново.
