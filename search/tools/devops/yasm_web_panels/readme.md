Описание и помощь с синтаксисом: https://wiki.yandex-team.ru/golovan/userdocs/templatium/alerts/

Как апнуть панели:
1. Для нового шаблона (если он новый) нужно создать пустую заглушку с требуемым именем и овнерами: ```curl -d '{"key": "template_name", "owners": [""]}' 'https://yasm.yandex-team.ru/srvambry/tmpl/panels/create'```
1. Пишем код в tmpl
2. make diff_panels, проверяем, что в диффе только нащи измененения
3. make update или make update_panels. Проверяем, что панель выглядит ок
4. Если ок - коммитим
5. Если не ок - откатываемся на транк, снова зовем make update или make update_panels

Как апнуть алерты:
1. Для нового шаблона (если он новый) нужно создать пустую заглушку с требуемым именем и овнерами: ```curl -d '{"key": "template_name", "owners": [""]}' 'https://yasm.yandex-team.ru/srvambry/tmpl/alerts/create'```
1. make update или make update_alerts
2. make diff_alerts, проверяем, что в диффе только наши измененения
3. Заходим на панель алертов в головане, например https://yasm.yandex-team.ru/template/alert/mmeta_web_duty_tmpl_alerts/ - нажимаем "Применить"
4. Если ок - коммитим, не ок - откатываем, снова зовем апдейт
