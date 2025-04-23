Template Alerts
===============

* `common-yasm-alerts.jinja` - template for common alerts of market logistics
* `database-alerts.jinja` - template for database alerts of market logistics

Links
--------
* [market-logistics-database](https://yasm.yandex-team.ru/template/alert/market-logistics-database) template

Cookbook
--------

1. [Wiki article](https://wiki.yandex-team.ru/golovan/userdocs/templatium/alerts/api/)

1. **Create**

        curl -d '{"key": "market_logistics", "owners": ["login", ...]}' 'https://yasm.yandex-team.ru/srvambry/tmpl/alerts/create'

1. **Render and check**

        curl 'https://yasm.yandex-team.ru/srvambry/tmpl/alerts/render_json/market-logistics-database'

1. **Update template**

        curl -s --data-binary @database-alerts.jinja 'https://yasm.yandex-team.ru/srvambry/tmpl/alerts/update/content?key=market-logistics-database'

1. **Apply & generate juggler checks**

        curl -X POST 'https://yasm.yandex-team.ru/srvambry/tmpl/alerts/apply/market-logistics-database'
