## Тесты на основные метрики Веб-карт

В UI [логируется](https://wiki.yandex-team.ru/maps/analytics/web/bebr/) каждый значимый блок, а аналитики по этим логам считают [статистику посещений и кликов](https://stat.yandex-team.ru/Maps/Adhoc/CTRBlocks). Некоторые из этих метрик являются для Веб-карт основными — например, сколько людей бронирует столик в ресторане или кликает в плашку геопродукта.

Если во время разработки поменять имена аналитических нод, мы перестанем правильно считать статистику, но узнаем об этом примерно через месяц, когда аналитики заметят просадку основных метрик Веб-карт.

Тесты в этой директории гарантируют, что основные метрики не ломаются.

### Что делать, если упал тест?

1. Любые _случайные_ изменения, которые ломают текущие тесты, нужно откатить.
2. Если изменения _неслучайны_, нужно договориться с аналитиками, что назрела необходимость поменять имена нод и, соответственно, регулярные выражения в тестах.

### Почему упал тест?

1. Разработчик случайно изменил имя аналитической ноды.
2. Разработчик перенёс UI-блок в другой компонент.

### Почему в тестах регулярные выражения?

Например, кнопка "Забронировать столик" есть и в широкой карточке, и в узкой и ещё в poi-панели. При кликах в неё будут логироваться разные аналитические ноды:

-   в широкой карточке — [`maps_www.orgpage.content.business_link`](https://stat.yandex-team.ru/Maps/Adhoc/CTRBlocks?scale=d&path=%09R%09orgpage%09content%09business_link%09&geo_path=%0910000%09&max_distance=1&path__mode=subtree&date_min=2021-01-26+00%3A00%3A00&date_max=2021-01-26+23%3A59%3A59&_incl_fields=visitors&_incl_fields=clicked_visitors&_incl_fields=visitors_ctr&_incl_fields=sessions&_incl_fields=clicked_sessions&_incl_fields=sessions_ctr&_incl_fields=shows&_incl_fields=clicks&_incl_fields=ctr)
-   в узкой карточке — [`maps_www.serp_panel.preview_card.business_link`](https://stat.yandex-team.ru/Maps/Adhoc/CTRBlocks?scale=d&path=%09R%09serp_panel%09preview_card%09business_link%09&geo_path=%0910000%09&max_distance=1&path__mode=subtree&date_min=2021-01-26+00%3A00%3A00&date_max=2021-01-26+23%3A59%3A59&_incl_fields=visitors&_incl_fields=clicked_visitors&_incl_fields=visitors_ctr&_incl_fields=sessions&_incl_fields=clicked_sessions&_incl_fields=sessions_ctr&_incl_fields=shows&_incl_fields=clicks&_incl_fields=ctr)
-   в карточке poi — [`maps_www.poi_panel.preview_card.business_link`](https://stat.yandex-team.ru/Maps/Adhoc/CTRBlocks?scale=d&path=%09R%09poi_panel%09preview_card%09business_link%09&geo_path=%0910000%09&max_distance=1&path__mode=subtree&_incl_fields=visitors&_incl_fields=clicked_visitors&_incl_fields=visitors_ctr&_incl_fields=sessions&_incl_fields=clicked_sessions&_incl_fields=sessions_ctr&_incl_fields=shows&_incl_fields=clicks&_incl_fields=ctr&date_min=2021-01-26+00%3A00%3A00&date_max=2021-01-26+23%3A59%3A59)

Чтобы в тестах не харкодить имена каждой аналитической ноды, мы проверяем не полное имя, а сверяем, что оно удовлетворяет регекспу `.*\.(preview_card|orgpage)\..*(business_link)$`

### ВАЖНО

Все регулярные выражения собраны в файле `tests/sets/counters/main-metrics/analytic-names.ts`.

Аналитики используют эти же регекспы, чтобы считать статистику.

**Менять регулярные выражения можно только после апрува аналитиков!**
