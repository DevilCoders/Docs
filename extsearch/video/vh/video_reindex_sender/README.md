Service sends documents to reindex.

For vh documents it simply updates field `update_time` in db. Service updates 3000 docs each 60 seconds and doesn't check lb queue size, so be carefull, don't send too much uuids.

For ugc documents service sends uuids to sqs meta_notify.fifo. It checks queue size itself and doesn't overflow it so you can send ugc docs as much as you want.

## yandex-deploy
https://yd.yandex-team.ru/stages/vh-video-reindex-sender

## yasm
https://yasm.yandex-team.ru/panel/antonfn._dmXzb0

## upstream
https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/frontend.vh.yandex.ru/upstreams/list/internal_video_reindex_sender/show/

## pgpass secret
https://yav.yandex-team.ru/secret/sec-01eyrd0yhh31q2abre79exje61

## handlers

# /upload post
uploads video to service and then sends it to reindex queues

curl 'internal.vh.yandex-team.ru/reindex/upload' -X POST -d '{
    "uuids": [
        "v-0CWa6OgfAU", "4e5dc39571f338cd9ea318c65405df2c", "13152780619761459671", 13152780619761459671
    ],
    "urls": [
        "frontend.vh.yandex.ru/player/1241369629866379822",
        "GroupingUrl=frontend.vh.yandex.ru/player/v-0CWa6OgfAU"
    ]
}'

`uuids` - array of string/int, can be ugc uuid, vh uuid, vh content_group_id
`urls` - array of strings, uuid will be retrieved from string with regex like "player/<uuid/conten_group>"

# /clear post
clear currents queues with docs

curl 'internal.vh.yandex-team.ru/reindex/clear' -X POST -d '{
    "clear_vh": true,
    "clear_ugc": true
}'

# /unistat get
return current queues size

curl 'internal.vh.yandex-team.ru/reindex/unistat'

## run locally
setup SQS_MODERATION_TOKEN
https://yav.yandex-team.ru/secret/sec-01dfb7vvfwgfwe3sw3zhdeexgj - sqs_token

see ./start.sh
