# Файловая структура

`src/common` - инфраструктурные компоненты 

`src/common/acl` - работа с правами

`src/common/api` - работа с api

`src/common/config` - конфиг приложения

`src/common/events` - работа с событиями

`src/common/experiments` - эксперименты 3.0, в том числе конфиги

`src/common/http` - функции для работы с http слоем

`src/common/invariant` - проверка инвариантов

`src/common/loggers` - логгирование действий, в том числе метрик и security events

`src/common/passport` - работа с паспортной инфраструктурой 

`src/common/tvm` - работа с TVM

`src/api` - ручки сервисов

`src/modules/api` - api

`src/modules/catalogs` - справочники

`src/modules/checkouter` - работа с данными чекаутера

`src/types` - Общие типы. Реэкспорты и собственные.

`bootstrap.ts` - первичная инициализация окружения. 

`events.ts` - реакции на события (писать события в логи)

`localTvm.ts` - tvmtool для локальной разработки

`middlewares.ts` - общие мидлвары

`router.ts` - корневые роуты