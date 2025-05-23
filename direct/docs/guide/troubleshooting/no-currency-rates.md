# Нет свежих курсов валют

## Как проявляется

- тесты падают с `не найден курс валюты КОД на ДАТА`
- иногда это может выглядеть в логе так: `"\\x{43d}\\x{435} \\x{43d}\\x{430}\\x{439}\\x{434}\\x{435}\\x{43d} \\x{43a}\\x{443}\\x{440}\\x{441} \\x{432}\\x{430}\\x{43b}\\x{44e}\\x{442}\\x{44b} UAH \\x{43d}\\x{430} 20210118 at /var/www/ppc.yandex.ru/protected/Currency/Rate.pm line 235.\n\"`

## Диагностика

Нужно посмотреть, что там на самом деле отвечает баланс.
На ppcdev с беты можно выполнить такой однострочник (дату и валюту подставить свои):
```sh
perl -Mmy_inc=for,protected -MYandex::Balance -MSettings -MDDP -le ' p Yandex::Balance::balance_call("Balance.GetCurrencyRate", ["EUR", "20210118"]);'
```
Выведет:
```text
\ [
    [0] 0,
    [1] "SUCCESS",
    [2] {
        currency   "EUR",
        date       "20210116T00:00:00",
        rate       89.2546
    }
]
```
Здесь видно, что на запрос курса за 18 января пришел курс от 16го числа — мы такое себе не сохраняем, считая что свежего курса нет.

## Решение 1
Написать в чатик баланса [{#T}](../../reference/chats.md#balance-test) о проблеме с курсами, приложить запрос/ответ, попросить починить курсы.
Дождаться починки. Скрипты с небольшой задержкой сами подтянут свежие данные.

## Решение 2
Если нет времени ждать и курсы подойдут "хоть какие", есть скриптик `protected/maintenance/fill_currency_rates.pl`.
Его запуском с беты в нужной конфигурации можно заполнить курсы последними значениями.
У скрипта есть опция `--help`, там подробности.
