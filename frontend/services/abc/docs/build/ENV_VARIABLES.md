# Environment variables

## `ENVIRONMENT`
Используется только при `NODE_ENV !== 'development' && NODE_ENV !== 'hermione'` и определяет окружение в CI. 
По аналогии с использованием в [tools-deploy-scripts](https://github.yandex-team.ru/dima117a/tools-deploy-scripts/blob/master/README.md#конфигурационные-файлы-используемых-инструментов)
принимает значения `beta / testing / production`.
Используется для определения окружения, в котором нужно обновить статику текущей версии на s3.
Default: `testing`

## `YENV`
Принимает значения `testing / production`

## `NODE_ENV`
Принимает значения `testing / production / development / hermione`
