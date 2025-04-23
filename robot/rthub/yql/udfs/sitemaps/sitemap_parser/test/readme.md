#Для генерации тестовых данных использовались следующие YQL запросы (нужна robot/rthub/yql/udfs/common/libcommon_udf.so):

##Basic:

```
pragma yt.DefaultMemoryLimit='4G';

PRAGMA udf("libcommon_udf.so");

$splitter = Common::SplitResponse();

select
    Url
    , MimeType
    , ResponseBody
from (
    select
        row_number() over w as row_num
        , Url
        , MimeType
        , ResponseBody
    from (
        select
            Url
            , MimeType
            , LastAccess
            , ResponseBody
        from (
            select
                Host || Path as Url
                , MimeType
                , LastAccess
                , $splitter(HttpResponse).Body as ResponseBody
            from hahn.[home/kwyt/sitemaps/data]
            where HttpResponse is not null and MimeType <> 2)
        where
           ResponseBody like '%xmlns="http://www.sitemaps.org/schemas/sitemap/0.9"%'
           and ResponseBody not like '%<sitemap%'
           and ResponseBody not like '%<ovs:video%'
           and ResponseBody not like '%<image:image'
           and ResponseBody regexp '<loc>\\s+'
        limit 1000)
    WINDOW w AS (PARTITION BY Url ORDER BY LastAccess DESC))
WHERE
    row_num = 1
limit 30;
```

##Index:

```
PRAGMA udf("libcommon_udf.so");

$splitter = Common::SplitResponse();

select
    *
from (
    select
        Host || Path as Url,
        MimeType,
        $splitter(HttpResponse).Body as Sitemap
    from hahn.[home/kwyt/sitemaps/data]
    where HttpResponse is not null and MimeType <> 2)
where
    Sitemap like '%<sitemapindex>%'
limit 20;
```

##Ovs

```
pragma yt.DefaultMemoryLimit='4G';

PRAGMA udf("libcommon_udf.so");

$splitter = Common::SplitResponse();

select
    Url
    , MimeType
    , ResponseBody
from (
    select
        row_number() over w as row_num
        , Url
        , MimeType
        , ResponseBody
    from (
        select
            Url
            , MimeType
            , LastAccess
            , ResponseBody
        from (
            select
                Host || Path as Url
                , MimeType
                , LastAccess
                , $splitter(HttpResponse).Body as ResponseBody
            from hahn.[home/kwyt/sitemaps/data]
            where HttpResponse is not null and MimeType <> 2)
        where
            ResponseBody like '%http://video.yandex.ru/schemas/video_import%'
            and ResponseBody like '%xmlns="http://www.sitemaps.org/schemas/sitemap/%'
            and ResponseBody regexp '<ovs:video>\\s+'
            and ResponseBody not like '%<image:image>%'
            and ResponseBody not like '%<video:video>%'
        limit 200)
    WINDOW w AS (PARTITION BY Url ORDER BY LastAccess DESC))
WHERE
    row_num = 1
limit 20;
```

##Ovs2

```
pragma yt.DefaultMemoryLimit='4G';

PRAGMA udf("libcommon_udf.so");

$splitter = Common::SplitResponse();

select
    Url
    , MimeType
    , ResponseBody
from (
    select
        row_number() over w as row_num
        , Url
        , MimeType
        , ResponseBody
    from (
        select
            Url
            , MimeType
            , LastAccess
            , ResponseBody
        from (
            select
                Host || Path as Url
                , MimeType
                , LastAccess
                , $splitter(HttpResponse).Body as ResponseBody
            from hahn.[home/kwyt/sitemaps/data]
            where HttpResponse is not null and MimeType <> 2)
        where
            ResponseBody like '%https://yandex.ru/support/video/partners/markup.html%'
            and ResponseBody like '%xmlns="http://www.sitemaps.org/schemas/sitemap/%'
            and ResponseBody like '%<ovs:video>%'
        limit 200)
    WINDOW w AS (PARTITION BY Url ORDER BY LastAccess DESC))
WHERE
    row_num = 1
limit 20;
```

##Images:

```
pragma yt.DefaultMemoryLimit='4G';

PRAGMA udf("libcommon_udf.so");

$splitter = Common::SplitResponse();

select
    Url
    , MimeType
    , ResponseBody
from (
    select
        row_number() over w as row_num
        , Url
        , MimeType
        , ResponseBody
    from (
        select
            Url
            , MimeType
            , LastAccess
            , ResponseBody
        from (
            select
                Host || Path as Url
                , MimeType
                , LastAccess
                , $splitter(HttpResponse).Body as ResponseBody
            from hahn.[home/kwyt/sitemaps/data]
            where HttpResponse is not null and MimeType <> 2)
        where
            ResponseBody like '%http://www.google.com/schemas/sitemap-image/1.1%'
            and ResponseBody regexp '<image:image>\\s+'
            and ResponseBody like '%xmlns="http://www.sitemaps.org/schemas/sitemap/0.9"%'
            and ResponseBody not like '%<ovs:video>%'
            and ResponseBody not like '%<video:video>%'
        limit 200)
    WINDOW w AS (PARTITION BY Url ORDER BY LastAccess DESC))
WHERE
    row_num = 1
limit 20;
```

##Deprecated:

```
pragma yt.DefaultMemoryLimit='4G';

PRAGMA udf("libcommon_udf.so");

$splitter = Common::SplitResponse();

select
    Url
    , MimeType
    , ResponseBody
from (
    select
        row_number() over w as row_num
        , Url
        , MimeType
        , ResponseBody
    from (
        select
            Url
            , MimeType
            , LastAccess
            , ResponseBody
        from (
            select
                Host || Path as Url
                , MimeType
                , LastAccess
                , $splitter(HttpResponse).Body as ResponseBody
            from hahn.[home/kwyt/sitemaps/data]
            where HttpResponse is not null and MimeType <> 2)
        where
            ResponseBody regexp '<urlset\\s+xmlns="http://www.google.com/schemas/sitemap/0\\.\\d+"'
            and ResponseBody not like '%<ovs:video>%'
            and ResponseBody not like '%<image:image>%'
            and ResponseBody not like '%<video:video>%'
        limit 200)
    WINDOW w AS (PARTITION BY Url ORDER BY LastAccess DESC))
WHERE
    row_num = 1
limit 20;
```

##AltLang:

```
pragma yt.DefaultMemoryLimit='4G';
pragma yt.MaxRowWeight='134217728';

PRAGMA udf("libcommon_udf.so");

$splitter = Common::SplitResponse();

select
    Url
    , MimeType
    , ResponseBody
from (
    select
        row_number() over w as row_num
        , Url
        , MimeType
        , ResponseBody
    from (
        select
            Url
            , MimeType
            , LastAccess
            , ResponseBody
        from (
            select
                Host || Path as Url
                , MimeType
                , LastAccess
                , $splitter(HttpResponse).Body as ResponseBody
            from hahn.[home/kwyt/sitemaps/data]
            where HttpResponse is not null and MimeType <> 2)
        where
           ResponseBody like '%xmlns="http://www.sitemaps.org/schemas/sitemap/0.9"%'
           and ResponseBody not like '%<sitemap%'
           and ResponseBody not like '%<ovs:video%'
           and ResponseBody not like '%<image:image'
           and ResponseBody regexp '<loc>\\s+'
           and ResponseBody regexp '<xhtml:link'
        limit 200)
    WINDOW w AS (PARTITION BY Url ORDER BY LastAccess DESC))
WHERE
    row_num = 1
limit 20;
```

##AltLang2:

```
pragma yt.DefaultMemoryLimit='4G';
pragma yt.MaxRowWeight='134217728';

PRAGMA udf("libcommon_udf.so");

$splitter = Common::SplitResponse();

select
    Url
    , MimeType
    , ResponseBody
from (
    select
        row_number() over w as row_num
        , Url
        , MimeType
        , ResponseBody
    from (
        select
            Url
            , MimeType
            , LastAccess
            , ResponseBody
        from (
            select
                Host || Path as Url
                , MimeType
                , LastAccess
                , $splitter(HttpResponse).Body as ResponseBody
            from hahn.[home/kwyt/sitemaps/data]
            where HttpResponse is not null and MimeType <> 2)
        where
           ResponseBody like '%xmlns="http://www.sitemaps.org/schemas/sitemap/0.9"%'
           and ResponseBody not like '%<sitemap%'
           and ResponseBody like '%<loc>%'
           and ResponseBody regexp '<xhtml:link\\s+rel="alternate"\\s+hreflang=[^>]+/></url>'
        limit 200)
    WINDOW w AS (PARTITION BY Url ORDER BY LastAccess DESC))
WHERE
    row_num = 1
limit 20;
```

##News:

```
pragma yt.DefaultMemoryLimit='4G';

PRAGMA udf("libcommon_udf.so");

$splitter = Common::SplitResponse();

select
    Url
    , MimeType
    , ResponseBody
from (
    select
        row_number() over w as row_num
        , Url
        , MimeType
        , ResponseBody
    from (
        select
            Url
            , MimeType
            , LastAccess
            , ResponseBody
        from (
            select
                Host || Path as Url
                , MimeType
                , LastAccess
                , $splitter(HttpResponse).Body as ResponseBody
            from hahn.[home/kwyt/sitemaps/data]
            where HttpResponse is not null and MimeType <> 2)
        where
            ResponseBody like '%http://www.google.com/schemas/sitemap-news/0.9%'
            and ResponseBody regexp '<news:news>\\s+'
            and ResponseBody like '%xmlns="http://www.sitemaps.org/schemas/sitemap/0.9"%'
            and ResponseBody like '%<news:language>en%'
            and ResponseBody not like '%<ovs:video>%'
            and ResponseBody not like '%<video:video>%'
            and ResponseBody not like '%<image:image>%'
        limit 200)
    WINDOW w AS (PARTITION BY Url ORDER BY LastAccess DESC))
WHERE
    row_num = 1
limit 20;
```

##Videos

```
pragma yt.DefaultMemoryLimit='4G';

PRAGMA udf("libcommon_udf.so");

$splitter = Common::SplitResponse();

select
    Url
    , MimeType
    , ResponseBody
from (
    select
        row_number() over w as row_num
        , Url
        , MimeType
        , ResponseBody
    from (
        select
            Url
            , MimeType
            , LastAccess
            , ResponseBody
        from (
            select
                Host || Path as Url
                , MimeType
                , LastAccess
                , $splitter(HttpResponse).Body as ResponseBody
            from hahn.[home/kwyt/sitemaps/data]
            where HttpResponse is not null and MimeType <> 2)
        where
            ResponseBody like '%http://www.google.com/schemas/sitemap-video/1.1%'
            and ResponseBody regexp '<video:video>\\s+'
            and ResponseBody like '%xmlns="http://www.sitemaps.org/schemas/sitemap/0.9"%'
            and ResponseBody not like '%<ovs:video>%'
            and ResponseBody not like '%<news:news>%'
            and ResponseBody not like '%<image:image>%'
        limit 200)
    WINDOW w AS (PARTITION BY Url ORDER BY LastAccess DESC))
WHERE
    row_num = 1
limit 20;
```
