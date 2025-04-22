# gh-payload-by-uuid

Тулза для поиска Delivery Payload в известных репозиториях по UUID-доставки.

![image](https://media.github.yandex-team.ru/user/3220/files/c2ff0700-45d7-11ea-9dd4-43f0afcf8899)

:warn: Требует user-сессии из куки браузера. При первом запуске и протухании попросит ввести её из куки и сохранит в конфиг.

## Requirements

- `node 8.6+`
- `npm 6.2+`

## Usage

`npx @yandex-int/gh-payload-by-uuid 00112233-4455-6677-8899-aabbccddeeff`

```bash
# Скопировать в буфер payload и ответ от обработчика в формате gfm (aka md)
$ npx @yandex-int/gh-payload-by-uuid 00112233-4455-6677-8899-aabbccddeeff | pbcopy

# Загрузить на paste тело payload
$ npx @yandex-int/gh-payload-by-uuid 00112233-4455-6677-8899-aabbccddeeff --payload-body | ya paste

# Вывести в терминал тело ответа
$ npx @yandex-int/gh-payload-by-uuid 00112233-4455-6677-8899-aabbccddeeff --response-body
```

### Specificity

По-умолчанию ищет в доставках trendbox-ci хуков в значимых репозиториях (при наличии доступа):
```
    7315, // search-interfaces/trendbox-ci,
    13643, // serp/trendbox-ci,
    10008, // search-interfaces/frontend,
```

Досыпать ID своих хуков можно через переменную окружения HOOK_IDS:
```bash
$ env HOOK_IDS=12345,67890 npx @yandex-int/gh-payload-by-uuid 00112233-4455-6677-8899-aabbccddeeff
```

Ошибки съедаются, но можно включить, чтобы они выводились в `stderr`.
Для этого нужно выставить переменную окружения `DEBUG=gh-payload-by-uuid` (модуль debug).
