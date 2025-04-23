# Как исследовать логи nginx

Со всех продакшен хостов в Картах логи nginx отправляются в YT в папку [//home/logfeller/logs/maps-log](https://yt.yandex-team.ru/hahn/navigation?path=//home/logfeller/logs/maps-log). Каждый день набирается несколько терабайт логов.

Для исследования логов Огорода их стоит сначала перенести в отдельную таблицу.

```sql
USE hahn;

$start_date = "2020-11-01";
$end_date = "2020-11-10";

INSERT INTO `//home/maps/core/garden-exp/alexbobkov/garden_logs`
SELECT *
FROM RANGE(`//home/logfeller/logs/maps-log/1d`, $start_date, $end_date)
WHERE tskv_format="garden-server";
```

Получившаяся таблица имеет небольшой размер, и по ней можно запускать сравнительно быстрые YQL-запросы.

Пример YQL-запроса, который считает HTTP-запросы к Огороду с группировкой по ручкам:
```sql
USE hahn;

$replace_contours = Re2::Replace("/contours/[0-9a-z-_]+$");
$replace_contours2 = Re2::Replace("/contours/[0-9a-z-_]+/");
$replace_pages = Re2::Replace("/pages/[a-z_]+/");
$replace_modules = Re2::Replace("/modules/[a-z_]+/");
$replace_builds = Re2::Replace("/builds/[0-9]+/");
$replace_versions = Re2::Replace("/versions/[0-9]+/");
$replace_dir = Re2::Replace("/dir/[a-z0-9]+");
$replace_storage = Re2::Replace("/storage/[a-z0-9]+");
$replace_static = Re2::Replace("/static/.*");

$prepare = ($str) -> {
    $str = $replace_contours($str, "/contours/{contour_name}");
    $str = $replace_contours2($str, "/contours/{contour_name}/");
    $str = $replace_pages($str, "/pages/{module_name}/");
    $str = $replace_modules($str, "/modules/{module_name}/");
    $str = $replace_builds($str, "/builds/{build_id}/");
    $str = $replace_versions($str, "/versions/{version_id}/");
    $str = $replace_dir($str, "/dir/{key}");
    $str = $replace_storage($str, "/storage/{key}");
    $str = $replace_static($str, "/static/*");
    RETURN $str;
};

$prepared_data = (
    SELECT method, $prepare(Url::GetPath(request)) as request
    FROM `//home/maps/core/garden-exp/alexbobkov/garden_logs`
    WHERE vhost = "core-garden-server.maps.yandex.net"
);

SELECT method, request, count(*) AS count
FROM $prepared_data
GROUP BY method, request
ORDER BY count DESC;
```
