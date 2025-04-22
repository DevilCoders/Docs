# Самые популярные урлы страницы Цены КМ

Топ-1000 популярных запросов на странице сервиса. Полезны для анализа дата-граббером.

Теги: `тестирование`, `км`.

Ссылка: https://yql.yandex-team.ru/Operations/YVbOBJfFtzcrh77H7aRzLYbCudziwgYUQyUzAIEdrpA=

```sql
use marketclickhouse;

select
    url as qs
from market.nginx2
where
    date = today()
    and page_id = 'market:product-offers'
    and environment = 'PRODUCTION'
    and (position(url, '&how=') > 1 or position(url, '?how=') > 1)
group by url
order by count(url) desc
limit 1000;
```
