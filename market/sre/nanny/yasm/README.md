#YASM templates

[Documentation](https://wiki.yandex-team.ru/users/yoschi/templates-api/)

A Step-by-Step guide for updating a template:
1. Check you have the latest version
  ```> template=market-nginx; diff -Nu ${template}.template <(curl -s "https://yasm.yandex-team.ru/srvambry/tmpl/panels/get/content?key=${template}")```
2. Choose which version you like more
3. Upload the template file
  ```> template=market-nginx; curl --data-binary @${template}.template "https://yasm.yandex-team.ru/srvambry/tmpl/panels/update/content?key=${template}"```
4. Check it renders as you expect
  ```> template=market-nginx; curl "https://yasm.yandex-team.ru/srvambry/tmpl/panels/render_json/${template}?itype=ugcdaemon&ctype=production&prj=market"```
5. Go to the panel
  [https://yasm.yandex-team.ru/template/panel/market-nginx/itype=ugcdaemon;ctype=production;prj=market/](https://yasm.yandex-team.ru/template/panel/market-nginx/itype=ugcdaemon;ctype=production;prj=market/)