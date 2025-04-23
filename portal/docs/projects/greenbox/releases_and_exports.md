# Как релизить
Рекомендуется [релизить через новый CI](../releases.md).
Если по каким-либо причинам не получается, еще есть [дашборд](https://nanny.yandex-team.ru/ui/#/services/dashboards/catalog/portal_greenbox/). На момент написания страницы ресурс собирать нужно только один, [BUILD_PORTAL_GREENBOX](https://sandbox.yandex-team.ru/task/1019335936/view), но [это может поменяться](https://a.yandex-team.ru/review/1894196/details).
Настоятельно рекомендуется прочитать про [мониторинг гринбокса](./monitoring.md) перед выкаткой. Краткий список ссылок:
* [Еrror booster](https://error.yandex-team.ru/projects/avocado/projectDashboard?filter=service%20%3D%3D%20greenbox) - склад логов (ошибки)
* [Внутренняя панель](https://yasm.yandex-team.ru/menu/Portal/Avocado/greenbox/greenbox_own/) - графики о целостности кэша и не только
* [Внешняя панель](https://yasm.yandex-team.ru/menu/Portal/Avocado/greenbox/greenbox/) - аппхостовые и железные графики вершин

Также имеет смысл поглядывать на графики графов, в которых участвует гринбокс, например, сейчас он используется в графе новостей ([панель](https://yasm.yandex-team.ru/panel/yanykin.avocado_top_news_graph)).

# Как добавлять экспорты
Для добавления экспорта достаточно сказать экспорт пуллеру, чтобы он его начал загружать в гринбокс. Делается это через экспорт options в мадме, [но это может поменяться](https://st.yandex-team.ru/HOME-71537). Опция называется `export_puller_http_post_push_export_params`, сейчас в ней 
```json
{
  "topnews.json": {
    "precheck": true,
    "mode": "overwrite",
    "urls": [
      "http://greenbox-testing.yandex.net/set",
      "http://greenbox.yandex.net/set"
    ]
  },
  "topnews_new.json": {
    "precheck": true,
    "mode": "overwrite",
    "urls": [
      "http://greenbox-testing.yandex.net/set"
    ]
  }
}
```
но в одну строку. На верхнем уровне указывается имя файла экспорта, далее:
- `precheck` ставится в true
- `mode` должен соответствовать значению поля `rm_old` в `scripts/cacheup_daemon.pl` в перле
- `urls` ссылки, куда загружать данные.

Через минуту-две после выкатки экспорта с обновленным конфигом экспорт должен добраться до гринбокса.
**Также нужно добавить алерты для экспорта**, делается это через изменение шаблона алертов, описано подробнее в [секции о мониторинге](./monitoring.md#alerts).
Обновление алертов также обновит [внутреннюю панель мониторинга](https://yasm.yandex-team.ru/menu/Portal/Avocado/greenbox/greenbox_own/).
