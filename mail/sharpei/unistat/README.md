Для обновления всех панелей надо выполнить в текущей директории следующие команды:
```(bash)
curl --data-binary @panel_common.j2 'https://yasm.yandex-team.ru/srvambry/tmpl/panels/update/content?key=mail_sharpei_panel_common'
curl --data-binary @panel_brief.j2 'https://yasm.yandex-team.ru/srvambry/tmpl/panels/update/content?key=Mail_Sharpei_Brief'
curl --data-binary @panel.j2 'https://yasm.yandex-team.ru/srvambry/tmpl/panels/update/content?key=Mail_Sharpei'
```
