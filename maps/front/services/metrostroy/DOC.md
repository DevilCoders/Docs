Metrostroy has two versions of the [metrostroy_testing](https://metrostroy.tst.c.maps.yandex-team.ru/) and [metrostroy_production](https://metrostroy.c.maps.yandex-team.ru/) applications. Each version of the application has testing and production environments.

Both versions are used for [metro-app](https://beta.m.soft.yandex.ru/description?app=metro&platform_shortcut=android&branch=):
1. `developer_metro-app -> metrostroy_testing=>production` - local development application
2. `testing_metro-app -> metrostroy_production=>testing`- application test build
3. `production_metro-app -> metrostroy_production=>production` - application production build
