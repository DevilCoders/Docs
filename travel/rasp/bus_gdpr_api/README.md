# Bus gdpr api
Это сервис для выгрузки персональных данных пользователей из сервиса Яндекс.Автобусы

# End points
GET /api/gdpr?uid=PASSPORT_UID&unixtime=SOME_TIME
Выгрузить все персональные данные пользователя
Ручка защищена TVM

POST /api/gdpr
Выгрузить все персональные данные пользователя
uid=PASSPORT_UID&unixtime=SOME_TIME
Ручка защищена TVM

GET /api/ping
Ручка для определения живости сервиса

# Qloud
https://qloud-ext.yandex-team.ru/projects/rasp/yandex-bus-gdpr-api/

# cli-режим
1. cd bin/cli && ya make --checkout
2. ./bus_gdpr_cli --uid USER_PASSPORT_UID

# server-режим
1. Вам нужно зайти в qloud и узнать значение секрета: BUS_GDPR_CONNECTION_STRING
2. cd bin/server && ya make --checkout
3. DISABLE_TVM=true BUS_GDPR_CONNECTION_STRING="CONNECTION_STRING_TO_BUS_PGAAS" ./bus_gdpr_api -b [::]:5000

# !!!! Важно
Результаты ответа ручек /api/gdpr не должны быть нигде сохранениы и опубликованы, эта ручка отдает настоящие данные пользователей
