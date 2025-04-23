# **Либа распространненных в парсинге фукций.**

Желательно если сюда что-то доваляете - пишите вики к функциям чтобы можно было как то в этом ориентироваться


# Гайд по либам и функциям

## index.sql

Либа в которой собраны фукции для работы с белым(/синим) индексом маркета

### is_valid_region
### get_price
### fix_url

## normalize_url.sql
Либа функций с нормализацией урлов. Основная цель поддерживать $normalize_url функцию. которая на вход принимает url и максимально его чистит.
### normalize_url
Если добавляете кастомную чистку урлов для какого-то домена, закиньте сюда через case when ...

## parse_ozon.sql
Правила парсинга озона для [kwyt_traversal](https://a.yandex-team.ru/arc_vcs/market/dynamic_pricing_parsing/kwyt_traversal/executables/yql/ParseHtmls.yql) и [regional_parsing](https://a.yandex-team.ru/arc_vcs/market/dynamic_pricing_parsing/regional_parsing/vh/operation_parse_htmls.yql)
