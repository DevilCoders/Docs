* [История выкатки релизов](https://wiki.yandex-team.ru/pochta/testirovanie/release/#25.10.2018-relizgruppirovkapisem)
* [Тестирование почтового фронтенда в qloud](https://wiki.yandex-team.ru/users/sanyatihy/Testirovanie-pochtovogo-frontenda-v-qloud/)


## Мониторинги

https://wiki.yandex-team.ru/users/avanes/Dashbordy/

* Touch: [grafana (nginx, duffman, backends)](https://grafana.yandex-team.ru/d/mail-touch-server/mail-touch-server-http) | [golovan](https://yasm.yandex-team.ru/template/panel/webmail/prj=mail.webmail.production;component=quinn/) | [golovan-http](https://yasm.yandex-team.ru/template/panel/webmail-http/prj=mail.webmail.production;component=quinn/) | [клиентские метрики](https://grafana.yandex-team.ru/d/mail-touch/touch-mail-client)

* Touch-corp: [graphite](https://gr-mg.yandex-team.ru/dashboard#mail_quinn_corp) | [golovan](https://yasm.yandex-team.ru/template/panel/webmail/prj=mail.webmail.intranet-production;component=quinn/) | [golovan-http](https://yasm.yandex-team.ru/template/panel/webmail-http/prj=mail.webmail.intranet-production;component=quinn/)
* [s3-mds](https://yasm.yandex-team.ru/template/panel/s3_mds_nginx/bucket=quinn/) | [yastatic-S3](https://yasm.yandex-team.ru/template/panel/yastatic_projects_s3/yastatic_project_name=quinn/)
* [mail-web-backends golovan](https://yasm.yandex-team.ru/panel/sanyatihy.mail_web_backends/)

## Логи

* [duffman-access](https://yt.yandex-team.ru/hahn/navigation?path=//home/logfeller/logs/mail-duffman-access-log)
* [duffman-http](https://yt.yandex-team.ru/hahn/navigation?path=//home/logfeller/logs/mail-duffman-http-log)
* [nginx-access](https://yt.yandex-team.ru/hahn/navigation?path=//home/logfeller/logs/mail-access-log)
* [monitoring](https://yt.yandex-team.ru/hahn/navigation?path=//home/mailfront&filter=monitoring)
* [errors](https://yt.yandex-team.ru/hahn/navigation?path=//home/mailfront&filter=errors)

## Стрельбы

* https://jenkins-load.yandex-team.ru/view/MAIL/job/quinn_qloud/
