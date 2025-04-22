# Panels

**Dashboard МЯК**: https://yasm.yandex-team.ru/template/panel/mobile-maps/ <br />
**Dashboard Навигатора**: https://yasm.yandex-team.ru/template/panel/mobile-navigator/ <br />

Подробная документация по Головану https://wiki.yandex-team.ru/golovan/

---

## Готовые запросы для Maps
* **update** - `curl --data-binary @./mobile-maps.jinja2 'https://yasm.yandex-team.ru/srvambry/tmpl/panels/update/content?key=mobile-maps'`

## Готовые запросы для Maps
* **update** - `curl --data-binary @./mobile-navigator.jinja2 'https://yasm.yandex-team.ru/srvambry/tmpl/panels/update/content?key=mobile-navigator'`

---

Значения сигналов можно помотреть в интерфейсе Голована,  составив руками запрос. <br />
https://yasm.yandex-team.ru/chart/itype=maps-mobile;deploy_unit=app;stage=maps-mobile-infra_production;hosts=ASEARCH;signals=unistat-maps_ios_crash_sessions_percentage_10m_axxx/

ios_crash_sessions_percentage_10m

```
itype=maps-mobile;
deploy_unit=app;
stage=maps-mobile-infra_production;
hosts=ASEARCH;
signals=unistat-<signal_name>
```

---

Все сигналы можно посмотреть через поиск <br />
https://yasm.yandex-team.ru/search/-tags/?term=maps-mobile-infra<br />
* Тег - `itype=maps-mobile; deploy_unit=app; stage=maps-mobile-infra_production` <br />
* Метагруппа - `ASEARCH` <br />
* Наши сигналы начинаются с префикса - `unistat-maps` <br />

