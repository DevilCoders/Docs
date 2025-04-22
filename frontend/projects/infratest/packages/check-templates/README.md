# Check-templates

Маленький пакет, который извлекает содержимое страницы по адресу и ищет там переданное значение.
Есть возможность сузить поиск с помощью регулярного выражения, переданного в `--pattern`.
Если регулярное выражение содержит скобочную группу, что сравниваться будет значение из группы.

## Установка

```
npm i @yandex-int/check-templates
```

## Использование

```bash
check-templates <url> <expected>

Check templates by some service url.

Positionals:
  url       service url for check templates                             [string]
  expected  string to be found on the page                              [string]

Options:
  --help, -h     Show help                                             [boolean]
  --version, -v  Show version number                                   [boolean]
  --pattern      RegExp pattern to find the string to be compared       [string]
```

## Примеры

```bash
# ищем на странице любое упоминание данной версии
check-templates "www.yandex.ru/search?text=cat" "v0.176.0"

# ищем на странице версию по паттерну
check-templates "www.yandex.ru/search?text=cat" "v0.176.0" --pattern "v\d*\.\d*\.\d*"

# ищем на странице версию подключенного скрипта butterfly. Сначала найдем по pattern значение, после сравним его с переданным.
check-templates "www.yandex.ru/search?text=cat" "v0.176.0" --pattern "butterfly/(v\d*\.\d*\.\d)/butterfly.js"
```
