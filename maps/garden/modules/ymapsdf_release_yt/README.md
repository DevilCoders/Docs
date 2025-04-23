# ymapsdf_release_yt module

Creates a resource in Sandbox [MAPS_GARDEN_YMAPSDF_EXPORT_YT](https://sandbox.yandex-team.ru/resources?type=MAPS_GARDEN_YMAPSDF_EXPORT_YT) that contains a path to the latest ymapsdf dataset in YT.

Example path: `//home/maps/core/garden/prod/ymapsdf/20190226_303119_1015_124326679`

Resource is a file with the path. And it also has an attribute `yt_path` with the same path.

The module also creates a soft link in YT to the latest ymapsdf dataset [//home/maps/core/garden/prod/ymapsdf/latest](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/core/garden/prod/ymapsdf/latest).

## Disclaimer

There is a possibility that the latest ymapsdf dataset has errors. In that case is is necessary to remove the module build and manually reset the link in YT to the previous ymapsdf release.
