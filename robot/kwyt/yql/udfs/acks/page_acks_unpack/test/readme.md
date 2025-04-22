Для генерации тестовых данных использовался следующий YQL запрос:

```
USE hahn;
pragma yt.MaxRowWeight='134217728';
pragma yt.DefaultMemoryLimit='4G';
pragma yt.pool = 'kwyt-test';

select
    Host, Path, LastAccess, TextCRC, Acknowledgements
from
    [//home/kwyt/pages/000/data]
where
    Acknowledgements is not null
    and IsLast
order by Host, Path, LastAccess, TextCRC
limit 20
UNION ALL
select
    Host, Path, LastAccess, TextCRC, Acknowledgements
from
    [//home/kwyt/pages/000/data]
where
    Acknowledgements is null
    and IsLast
order by Host, Path, LastAccess, TextCRC
limit 20
```
