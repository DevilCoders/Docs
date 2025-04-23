# Мониторинг для Fast-Data
## Панельки {#panels}
* **WEB** [yasm.yandex-team.ru/panel/fast-data/](https://yasm.yandex-team.ru/panel/fast-data/)
* **VIDEO** [yasm.yandex-team.ru/panel/fast-data-video/](https://yasm.yandex-team.ru/panel/fast-data-video/)

## Графики {#graphs}
* Графики **процента выкладки web** на которых видно какая версия была активирована в последний деплой: [активация](https://nda.ya.ru/3Vp5Qc), [активация + prepare](https://nda.ya.ru/3Vp5Qy)
* Графики **процента выкладки video** на которых видно какая версия была активирована в последний деплой: [активация](https://nda.ya.ru/t/tFekxkeh5DJPbw), [активация + prepare](https://nda.ya.ru/t/Tqb5Qlqr5DJRax)
* [unistat-load_fast_data_success_dmmm](https://yasm.yandex-team.ru/chart/signals=unistat-load_fast_data_success_dmmm;hosts=ASEARCH;itype=noapache;prj=web-main) – количество успешных reload-ов
* [unistat-load_fast_data_error_dmmm](https://yasm.yandex-team.ru/chart/signals=unistat-load_fast_data_error_dmmm;hosts=ASEARCH;itype=noapache;prj=web-main) – количество неупешых reload-ов
* [unistat-load_fast_data_time_axxt](https://yasm.yandex-team.ru/chart/signals=unistat-load_fast_data_time_axxt;hosts=ASEARCH;itype=noapache;prj=web-main/) – максимальное время перезагрузки данных, текущее число на графике – это максимальное время перезагрузки данных с последнего релиза в мс
* [YT request load](https://solomon.yandex-team.ru/?project=yt&cluster=locke&dashboard=yt-ui-user-request-load-new&service=yt_master&user=robot-upper-fastdata&b=1d)

## Светофоры и алерты {#alerts}
* [noapache-fast-data-age-web-all_dc](https://juggler.yandex-team.ru/project/report-infra-alerts/aggregate?host=web_sandwich.NOAPACHE_fast_data_age_chart_for_all_dc&service=for_all_dc) – juggler для WEB (all_dc)
* [noapache-fast-data-age-web](https://juggler.yandex-team.ru/project/search.noapache.fast_data/aggregate?host=noapache-web&service=fast-data-age&project=search.noapache.fast_data) – juggler для WEB
* [noapache-fast-data-age-video](https://juggler.yandex-team.ru/project/search.noapache.fast_data/aggregate?host=noapache-video&service=fast-data-age) – juggler для VIDEO
* [noapache-fast-data-age-betas](https://juggler.yandex-team.ru/project/report-infra-alerts/aggregate?host=web_sandwich.NOAPACHE_fast_data_age_betas_chart_for_all_dc&service=for_all_dc) – juggler для беток
* [noapache-fast-data-version](https://yasm.yandex-team.ru/chart-alert/alerts=noapache-fast-data-version;hosts=ASEARCH;itype=noapache;ctype=hamster,prestable,prod;prj=web-main/) – версия данных в продакшене
* [noapache-fast-data-version-diff](https://yasm.yandex-team.ru/chart-alert/alerts=noapache-fast-data-version-diff;hosts=ASEARCH;itype=noapache;ctype=hamster,prestable,prod;prj=web-main/) – разница между самой свежой версией и самой старой версией данных, используемых в данный момент в продакшене
* [noapache-fast-data-age](https://yasm.yandex-team.ru/chart-alert/alerts=noapache-fast-data-age;hosts=ASEARCH;itype=noapache;prj=web-main/) – разница между текущим временем и временем последнего коммита в данные в минутах
* Для **VIDEO** вертикали графики и светофоры аналогичные, их можно найти на [соответствующей панели](https://yasm.yandex-team.ru/panel/fast-data-video/)
