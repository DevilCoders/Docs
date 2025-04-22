## Yandex Maps Data Format (ymapsdf)

Official documentation: https://doc.yandex-team.ru/ymaps/ymapsdf/ymapsdf-ref

### How to add a new table

* Consult @tail first
* Add the table to `garden/create` dir
* Add primary keys, indexes and constraints for the table to `garden/finalize` if necessary
* Add foreign keys for the table to `garden/integrity` if necessary
* Add a query to `garden/extensions/region_view_format` (ask @uht)
* Add new sql file names to the corresponding ya.make files (including `package/ya.make`)
* Add the table to `tables_with_object_ids.sql` if it contains new object ids
* Add the name of the table to the [list](https://a.yandex-team.ru/arc/trunk/arcadia/maps/libs/ymapsdf/impl/tables.cpp)
* Run script to regenerate json schema (see below)

### How to add a new column to a table

* Add the column to `garden/create/table_name.sql`
* Add a constraint (if needed) to `garden/finalize/table_name.sql`
* Run script to regenerate json schema (see below)

### How to regenerate json schema

```
cd <path to package dir>
ya make
cd <path to tools/bin dir>
ya make
./schema_converter convert_and_generate --sql-schema-path ../../package/ymapsdf.sql --ymapsdf-dir ../../
```

### How to test changes

Run manually LARGE unit tests in CI and wait until they finish.

If you made a significant change ask a member of NMAPS team to run export manually in production before commit.

### How to test changes in Garden

Create an archive with the new schema:
```bash
tar --directory maps/doc/schemas/ymapsdf/garden --create --file ymapsdf2.schema.tar .
ya upload ymapsdf2.schema.tar
```

Open [Garden](https://garden.maps.yandex-team.ru/) and create a new contour.
More information about contours is in the [documentation](https://docs.yandex-team.ru/garden/experiments).

Create a file `data.json` with the request body:
```json
{
  "contour": "<contour_name>",
  "foreign_key": {
      "nmaps_export_task_id": "<task_id>",
      "region": "<region>"
  },
  "resources": [
    {
      "name": "src_url_<region>_yandex",
      "version": {
        "properties": {
          "file_list": [
            {
              "url": "<data url>",
              "name": "ymapsdf2.dump.gz.tar"
            },
            {
              "url": "<schema url>",
              "name": "ymapsdf2.schema.tar"
            }
          ],
          "vendor": "yandex",
          "region": "<region>",
          "shipping_date": "<shipping_date>"
        }
      }
    }
  ]
}
```

Fill in the placeholders: `<contour_name>`, `<task_id>`, `<region>`, `<shipping_date>`, `<data url>`, `<schema url>`.

Make a request:
```bash
curl -X POST -H "Content-Type: application/json" http://core-garden-server.maps.yandex.net/modules/ymapsdf_src/builds/ --data @data.json
```

Open `ymapsdf` page in Garden and switch to the earlier created contour.
Run `ymapsdf` build with your source.

### How to deploy the package

* Up the version in [changelog](package/debian/changelog)
* Run script to regenerate json schema (see above)
* Create a review
* Commit to Arcadia
* Wait until NMAPS docker images `core-nmaps-tasks-export` and `core-nmaps-tasks-sprav` are built in Sandbox
* Ask a member of NMAPS team (https://abc.yandex-team.ru/services/maps-core-nmaps) to deploy the docker images to testing
* Remind the member of NAMPS team to deploy the images to production
* If you added a new table then deploy modules `ymapsdf`/`ymapsdf_archive`/`ymapsdf_release_yt` to testing and to stable

Note that garden testing environment uses nmaps production export data.
Consider making hotfix if changes are out of nmaps release schedule.

Anyway consult @tail or Garden team members if you don't feel confident enough.

### If you want to remove a column or a table

Use YQL script to find ymapsdf consumers in order to notify them.
Edit `$table_name` variable to find consumers of a particular table.

```
USE hahn;

$table_name = "node";

$format = DateTime::Format("%Y-%m-%d");
$today = CurrentUtcDate();
$start_date = $today - DateTime::IntervalFromDays(7);
$end_date = $today;

SELECT DISTINCT user
FROM RANGE(`//home/logfeller/logs/yt-access-master-log/1d`, $format($start_date), $format($end_date))
WHERE cluster="hahn"
    AND method="GetBasicAttributes"
    AND (
        path LIKE "//home/maps/core/garden/stable/ymapsdf/latest%" OR
        original_path LIKE "//home/maps/core/garden/stable/ymapsdf/latest%" OR
        path LIKE "//home/maps/core/garden/stable/ymapsdf_release/%" OR
        original_path LIKE "//home/maps/core/garden/stable/ymapsdf_release/%"
    )
    AND (
        path LIKE "%/" || $table_name || "%" OR
        original_path LIKE "%/" || $table_name || "%"
    );
```
