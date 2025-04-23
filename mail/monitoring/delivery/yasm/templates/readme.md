## Шаблоны панелей:

### NWSMTP:
- https://yasm.yandex-team.ru/template/panel/nwsmtp_panel/prj=mail.nwsmtp.production.mxfront
- https://yasm.yandex-team.ru/template/panel/nwsmtp_panel/prj=mail.nwsmtp.production.mxback
- https://yasm.yandex-team.ru/template/panel/nwsmtp_panel/prj=mail.nwsmtp.production.smtp

 `curl --data-binary @nwsmtp.j2 'https://yasm.yandex-team.ru/srvambry/tmpl/panels/update/content?key=nwsmtp'`

### Notsolitesrv:
- https://yasm.yandex-team.ru/template/panel/notsolitesrv/prj=mail.notsolitesrv.production.notsolitesrv
- https://yasm.yandex-team.ru/template/panel/notsolitesrv/prj=mail.notsolitesrv-corp.production.notsolitesrv

 `curl --data-binary @notsolitesrv.j2 'https://yasm.yandex-team.ru/srvambry/tmpl/panels/update/content?key=notsolitesrv'`

### Postfix:
https://yasm.yandex-team.ru/template/panel/postfix

`curl --data-binary @postfix.j2 'https://yasm.yandex-team.ru/srvambry/tmpl/panels/update/content?key=postfix'`

### RateSrv:
- https://yasm.yandex-team.ru/template/panel/ratesrv/application=ratesrv;env=production
- https://yasm.yandex-team.ru/template/panel/ratesrv/application=ratesrv-corp;env=production

`curl --data-binary @ratesrv.j2 'https://yasm.yandex-team.ru/srvambry/tmpl/panels/update/content?key=ratesrv'`

### Mbsave:
- https://yasm.yandex-team.ru/template/panel/mdbsave_panel/prj=mail.mdbsave.production.save/
- https://yasm.yandex-team.ru/template/panel/mdbsave_panel/prj=mail.mdbsave-corp.production.save/

### Шарпей для организаций:
- https://yasm.yandex-team.ru/template/panel/org-sharpei/prj=mail.sharpei.mail-production/
- https://yasm.yandex-team.ru/template/panel/org-sharpei/prj=mail.sharpei.mail-intranet-production/

`curl --data-binary @org-sharpei.j2 'https://yasm.yandex-team.ru/srvambry/tmpl/panels/update/content?key=org-sharpei'`

## Шаблоны алертов:
### Postfix:
https://yasm.yandex-team.ru/template/alert/postfix/

`curl --data-binary @postfix-alerts.j2 'https://yasm.yandex-team.ru/srvambry/tmpl/alerts/update/content?key=postfix'`

`curl -X POST https://yasm.yandex-team.ru/srvambry/tmpl/alerts/apply/postfix`

### RateSrv:
https://yasm.yandex-team.ru/template/alert/ratesrv/

`curl --data-binary @ratesrv-alerts.j2 'https://yasm.yandex-team.ru/srvambry/tmpl/alerts/update/content?key=ratesrv'`

`curl -X POST https://yasm.yandex-team.ru/srvambry/tmpl/alerts/apply/ratesrv`

### Шарпей для организаций:
https://yasm.yandex-team.ru/template/alert/org-sharpei/

`curl --data-binary @org-sharpei-alerts.j2 'https://yasm.yandex-team.ru/srvambry/tmpl/alerts/update/content?key=org-sharpei'`

`curl -X POST https://yasm.yandex-team.ru/srvambry/tmpl/alerts/apply/org-sharpei`
