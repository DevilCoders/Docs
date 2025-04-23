## Run
1. Get [oauth token](https://oauth.yandex-team.ru/authorize?response_type=token&client_id=18e3616ea0ba41b2affb0c7056a29ba8) or take it [from yav](https://yav.yandex-team.ru/secret/sec-01dmjfzn46m7wfs725tdmwz12w/explore/versions).
1. Export it as SOLOMON_TOKEN and ST_TOKEN.
1. Give robot access to MONITORINGREQ if needed.
1. Run `curl -XPOST -d '{"key": "MONITORINGREQ-1621"}' localhost:8080` to test program locally.


## Deploy
1. Press `Release` in Arcanum ([Projects -> Solomon -> Release Solomon Helper](https://a.yandex-team.ru/projects/solomon/ci/releases/timeline?dir=solomon%2Fscripts%2Fquotas_helper&id=release-solomon-helper)).
1. Watch deploy in https://deploy.yandex-team.ru/stages/solomon-helper-bot.
1. Go to [solomon-helper.yandex-team.ru](https://solomon-helper.yandex-team.ru) to see fresh version.

