## Базы поискового индекса
#### Что это?
Марти переключают базы веба, картинок, видео. Это обновление поиска.
#### Что может взорвать?
Каждый релиз - свою вертикаль, далее надо смотреть по мониторингу для определения компоненты.
#### Когда обычно приезжает в очередь
* Практически каждый день, обычно после полуночи, но обязательно до 02:00.
* Команда разработчиков могут пропускать отправку релиза в очередь, обычно это в неделю:
  * 1 раз для веба,
  * 2-3 раз для видео,
  * 4-5 для картинок.
* При сомнениях: Марти может посмотреть историю деплоя для той или иной базы, и уточнить в чате у devops вертикали.

#### Когда обычно катим?
* Переключение должно начинаться не позже 2:00 (время старта выкатки в SAS, то есть без учета preparing).
* В случае готовности релиза базы после 2:00, Марти имеет право не выкатывать базу в прод.
* Время переключения на локацию не должно превышать 120 минут.
* В случае превышения этого порога при выкатке в SAS, Марти имеет право отменить выкатку и откатить базу.
* Для каждого случая исключения из этих ограничений необходимо обязательное согласование с ответственным за вертикаль и @alexunix (и заведение инцидента SPI, который должен быть привязан к [SPPROBLEM-319](https://st.yandex-team.ru/SPPROBLEM-319))
* Выкатка базы происходит с фризом всех остальных релизов, для этого после 23:00 марти не катает релизы из очереди (исключение - begemot).
* Перед самой выкаткой надо проверить успешно ли завершились все кубики с prepare в рецептах.
* Рецепты должны содержать полокационное переключение с закрытием локации - web на L7, видео и картинки - на apphost.
* Базы переключаются только вместе (одновременно в одну локацию), т.е. если докатился веб, но не переключились картинки, не начинать переключение web в следующую локацию, пока картинки не закончат переключаться.

### Базы веба
#### Сколько катится?
preparing - 0.5ч, 1ч переключения каждый локации, до 30 минут открытие каждой локации. Итого ~4ч.

#### Как катать?
* Найти в searchmon очереди тикет вида `web db index`.
* Провалиться в него, в ссылку вида `SANDBOX_RELEASE`.
* Выделить все тикеты через Select All.
* Далее `commit`.
* В описании есть ссылка на рецепт - проваливаемся в нее.
* Ждем немного прогрузку и выбираем `Apply through Nanny`.
* Далее будет ссылка на деплой - идем туда.
* В depoy можно сразу выбрать summary view.
* В 2:00 выбираем в summary view `Close SAS`. Рецепт сам выставит downtime и уведет трафик из ДЦ.
* Ждем на икностасе по графикам Веб Поиска в Сасово серых no data и когда уйдет полностью трафик на графиках.
* Как трафик ушел - жмем `Start Switch SAS`.
* Как базы допереключаться, будет heat up локации, далее появится `pre open`. Это дает 5% трафика, сразу нажимать не надо, а подождать пока [sas_age и sas_nocache_age](https://yasm.yandex-team.ru/panel/web_quality) станут меньше 30 а лучше меньше 20, также смотрим на sinsig - МКБР график и в целом чтобы ничего не критовало.
* После `pre open` ждем минут 15.
* Обычно критует [кеш](https://yasm.yandex-team.ru/alert/web_mmeta_tmpl_alerts.ASEARCH.mmeta_prestable_web-main_sas_yandsearch.cache-found) - это нормально.
* Если проблем нет - переходим к `open SAS`.
* Ждем минут 5-7 и убираем Confirm'ом все downtime на локацию.
* Если все ок - идем дальше и конфирмим `Close MAN for switch`.
* Повторить для MAN.
* Повторить для VLA.

#### Кого призывать при проблемах?
Дежурных веба в чате [DevOps Reactions (websearch)](https://t.me/joinchat/Qu9gEjzH9TfDPHH6) в зависимости от компоненты.

#### Как откатывать?
При необходимости отката, Марти должен призвать ответственного за релиз девопса и дежурного девопса для отката базы, т.к. необходим новый рецепт отката.

### Базы картинок
#### Сколько катится?
1,5ч на локацию, preparing быстрый.
#### Как катать?
* В searchmon находим тикет вида `images db index`.
* Проваливаемся в один из сервисов, и далее в dashboard `Основной контур Картинок` [images_all](https://nanny.yandex-team.ru/ui/#/services/dashboards/catalog/images_all).
* Накомичиваем тикеты с базой, номер базы скопировать (запомнить) из тикета в searchmon пред.пункта.
* Выбираем рецепт выкатки из описания, обычно это `switch_images_database_with_tier1_with_locks_queue`.
* Выктываем полокационно вместе с другими базами.
#### Кого призывать при проблемах?
[Дежурных от картинок](https://warden.z.yandex-team.ru/components/images).
#### Как откатывать?
При необходимости отката, Марти должен призвать ответственного за релиз девопса и дежурного девопса для отката базы, но при необходимости может начать откат через [revert view](https://nanny.yandex-team.ru/ui/#/services/group_revert?serviceIds=hamster_imgsint_vla%2Cproduction_imgmmeta_man%2Cproduction_imgmmeta_vla%2Chamster_app_host_vla_imgs%2Cvla_imgs_mmeta_beta%2Cproduction_imgsint_man%2Chamster_report_vla_imgs_all%2Cimgrq-production-man-yp%2Cproduction_images_report_renderer_vla_rkub%2Cproduction_imgs_embedding_storage_vla%2Cvla_imgs_int_beta%2Cproduction_images_commercial_daemon_man%2Cheater_imgmmeta_sas%2Cproduction_imgs_embedding_storage_sas%2Chamster_app_host_man_imgs%2Cprestable_report_sas_imgs_rkub%2Cproduction_app_host_man_imgs%2Chamster_report_sas_imgs_all%2Cpip_images_int%2Chamster_imgsint_man%2Chamster_noapache_man_imgs%2Cproduction_src_setup_sas_imgs%2Cproduction_noapache_man_imgs_rkub%2Cproduction_report_data_vla_imgs%2Chamster_src_setup_man_imgs%2Chamster_images_commercial_daemon_sas%2Cproduction_imgsint_sas%2Cvla_imgs_beta2_int%2Cproduction_imgscbrint_tier1_man%2Cproduction_report_vla_imgs_rkub%2Cproduction_src_setup_vla_imgs%2Cproduction_imgscbrint_tier1_vla%2Chamster_noapache_sas_imgs%2Chamster_images_commercial_daemon_man%2Chamster_src_setup_sas_imgs%2Cvla_imgs_beta2_mmeta%2Chamster_imgmmeta_sas%2Chamster_imgmmeta_man%2Cproduction_noapache_vla_imgs_rkub%2Cimgrq-production-sas-yp%2Cproduction_imgsint_tier1_vla%2Cproduction_imgmmeta_sas%2Cproduction_imgscbrint_sas%2Cproduction_report_man_imgs_rkub%2Cvla_imgs_multimeta_mmeta%2Cproduction_src_setup_man_imgs%2Csaas_refresh_production_images_quick_imgmmeta%2Chamster_imgsint_sas%2Cheater_imgmmeta_vla%2Cproduction_images_commercial_daemon_vla%2Csas-images-base-resources%2Cproduction_report_data_sas_imgs%2Cpip_cbir_int%2Cproduction_imgscbrint_tier1_sas%2Cvla_imgs_multibeta_cbr_int%2Cheater_imgmmeta_man%2Cproduction_noapache_sas_imgs_rkub%2Cvla_imgs_multibeta_int%2Cman-images-base-resources%2Cproduction_imgsint_vla%2Cproduction_images_commercial_daemon_sas%2Chamster_report_man_imgs_all%2Chamster_src_setup_vla_imgs%2Cproduction_app_host_sas_imgs%2Chamster_imgscbrint_man%2Chamster_imgmmeta_vla%2Cproduction_images_report_renderer_man_rkub%2Cvla-images-base-resources%2Cproduction_imgsint_tier1_man%2Chamster_imgscbrint_sas%2Cproduction_report_data_man_imgs%2Chamster_app_host_sas_imgs%2Cimgrq-production-vla-yp%2Cvla_imgs_multibeta_mmeta%2Cproduction_imgscbrint_man%2Cproduction_imgscbrint_vla%2Cproduction_imgs_remote_storage_sas%2Cproduction_imgs_embedding_storage_man%2Cproduction_imgsint_tier1_sas%2Cvla_images_mmeta_pip%2Chamster_noapache_vla_imgs%2Cproduction_app_host_vla_imgs%2Cproduction_imgs_inverted_index_vla%2Cproduction_images_report_renderer_sas_rkub%2Cproduction_imgs_inverted_index_sas&recentSnapshotsCount=5).

### Базы видео
#### Сколько катится?
1 час на локацию, preparing 30 мин. Итого 3,5ч.
####  Как катать?
* В searchmon находим тикет вида `video db index`.
* Проваливаемся в один из сервисов, и далее в dashboard `Video_base_searches` [video_base](https://nanny.yandex-team.ru/ui/#/services/dashboards/catalog/video_base).
* Накомичиваем тикеты с базой, номер базы скопировать (запомнить) из тикета в searchmon пред.пункта.
* Выбираем рецепт выкатки из описания, обычно это `deploy_video_database_with_locks_queue`.
* Выктываем полокационно вместе с другими базами.
* В последнее время участились случая, при открытии локации возрастает график деградации (красные горбики) на графике базовых, необходимо перед переходом к другой локации на переключение дождаться пока он спадет.
#### Кого призывать при проблемах?
Дежурных от видео [warden](https://warden.z.yandex-team.ru/components/video)
#### Как откатывать?
При необходимости отката, Марти должен призвать ответственного за релиз девопса и дежурного девопса для отката базы, но при необходимости может начать откат через [revert view](https://nanny.yandex-team.ru/ui/#/services/group_revert?serviceIds=vla-video-base-resources%2Cvideo_int_pip%2Cvla_video_int_hamster%2Cman_video_remote_storage%2Csas_video_remote_storage%2Cproduction_hamster_prs_vidmmeta_sas%2Cproduction_hamster_vidmmeta_sas%2Csaas_refresh_hamster_vhs_base_yp%2Cvla_video_int%2Cvla_video_multibeta_mmeta%2Csas-video-base-resources%2Cvideo_base_pip%2Csas_video_int%2Cproduction_hamster_vidmmeta_man%2Csaas_refresh_production_vhs_base_vla_yp%2Csaas_refresh_production_video_base_man%2Cproduction_vidmmeta_sas%2Cvla_video_multibeta_int%2Cman-video-embedding-resources%2Cproduction_hamster_prs_vidmmeta_vla%2Csas_video_int_hamster%2Csas-video-embedding-resources%2Cproduction_hamster_prs_vidmmeta_man%2Cman-video-invindex-resources%2Csaas_refresh_production_vhs_base_man_yp%2Csaas_refresh_production_vhs_base_sas_yp%2Cvla-video-embedding-resources%2Csas-video-invindex-resources%2Csaas_refresh_production_video_base_sas%2Cman_video_int%2Cman_video_int_hamster%2Cproduction_vidmmeta_vla%2Cvideo_base_pip_platinum%2Csaas_refresh_production_video_base_vla%2Cvideo_mmeta_pip%2Cvla_video_remote_storage%2Cman-video-base-resources%2Cvla_video_inverted_index_pip%2Csaas_refresh_hamster_video_base_sas%2Cvla_video_multimeta_mmeta%2Csaas_refresh_hamster_video_base_man%2Cproduction_vidmmeta_man%2Cvla_video_multibeta_united_rtyserver%2Cvla_video_multibeta_united_deploy%2Csaas_refresh_hamster_video_base_vla%2Cvla_video_embedding_pip%2Cvla-video-invindex-resources%2Cproduction_hamster_vidmmeta_vla&recentSnapshotsCount=5).

## Upper (noapache)
#### Что это?
Верхний метапоиск development (upper, noapache). Исторически был получен методом отпиливания от apache report bundle метапоисковой части, и назвали его noapacheupper. С переходом на apphost было решено вернуться к имени upper. Работает в двухголовом режиме
* UPPER_INT (блок, опрашивающий источники под верхним метапоиском)
* BLENDER (переранжирования, в т.ч. блендер)
#### Что может взорвать?
Верхний метапоиск, следвательно сам поиск.
#### Когда обычно приезжает в очередь?
По будням, раз в день/раз в два дня.
#### Когда обычно катим?
В рабочее время по будням.
#### Сколько катится?
2-2,5ч
#### Как катать?
* В searchmon очереди находим три релиза
    * upper (noapacheupper_executable_red_id): upple/stable-*-*
    * upper (rearrange_data_res_id): upple/stable-*-*/arcadia/search/web/rearrs_upper
    * upper (noapache_rtcc_bundle_res_id): upple/stable-*-*
Кликаем на любой и проваливаемся в сервис каждого вида web/img/video, следовательно в 3 дашборда.
* [noapache_web](https://nanny.yandex-team.ru/ui/#/services/dashboards/catalog/noapache_web)
* [noapache_imgs](https://nanny.yandex-team.ru/ui/#/services/dashboards/catalog/noapache_imgs)
* [noapache_video](https://nanny.yandex-team.ru/ui/#/services/dashboards/catalog/noapache_video)

В каждом накомитить указанные выше релизы из searchmon, для удобства можно выбрать сортировку itype. Как всегда смотрим diff и подтверждаем deploy.
Рецепты:
* Для video `manualconfirm_deploy_prestable_with_locks_queue`
* Для img `parallel_prepare_manual_deploy_with_locks_queue`
* Для web `a1_with_locks_queue`
#### Кого призывать при проблемах?
Дежурных [upper](https://warden.z.yandex-team.ru/components/web/s/upper) в чате [DevOps Reactions (websearch)](https://t.me/joinchat/Qu9gEjzH9TfDPHH6) или в чате [Релизы и саппорт noapacheupper](https://t.me/joinchat/CaUODkNMIpwWNzLu4pngow). 
#### Как откатывать?
В каждом дашборде надо через revert view.

## Rearrange_dynamic
#### Что это?
Быстрые релизы формул и конфигурационных файлов верхнего метапоиска через rearrange.dynamic.
#### Что может взорвать?
Верхний метапоиск
#### Когда обычно приезжает в очередь?
По нескольку раз в сутки.
#### Когда обычно катим?
В рабочие часы по будням.
#### Сколько катится?
1,5
#### Как катать?
Так как катается теми же рецептами что и Upper (noapache), можно катать совместно с Upper (noapache). Но тогда труднее опредить что взорвалось.
#### Кого призывать при проблемах?
Аналогично Upper (noapache).
#### Как откатывать?
Аналогично Upper (noapache).

## Web graph mapping
#### Что это?
Внесение изменений в графы аппхоста.
#### Что может взорвать?
Источники аппхоста, следовательно взрывает только web
#### Когда обычно приезжает в очередь?
По будням в рабочее время. 2-3 раза в неделю.
#### Когда обычно катим?
По будням в рабочее время.
#### Сколько катится?
1,5ч
#### Как катать?
Выбираем в searchmon очереди релиз вида `web_graph_mapping (app_host_stable_branch)`. Далее проваливаемся в один из сервисов и оттуда в дашборд [app_host_web](https://nanny.yandex-team.ru/ui/#/services/dashboards/catalog/app_host/)m накомичиваем тикеты, запускаем deploy с рецептом `app_host_ppsa_with_locks_queue`.
#### Кого призывать при проблемах?
Автора релиза (из описания релизного тикета) в чате [WEB Report, Graphs & RequestInit Releases](https://t.me/joinchat/CaUODkYSN2MyE5jE9xgJzg). Так как в warden компонента не занесена, можно найти дежурного [тут](https://rm.z.yandex-team.ru/component/web_graph_mapping) в графе `Responsible`. Обычно это @alex-ersh, @avitella, @feldsherov, @elshiko.
#### Как откатывать?
Через [revert view](https://nanny.yandex-team.ru/ui/#/services/group_revert?serviceIds=hamster_app_host_man_web_yp,production_src_setup_man_web_yp,prestable_app_host_sas_web_yp,hamster_app_host_man_pre_web_yp,production_app_host_man_web_yp,hamster_app_host_sas_web_yp,prestable_exp_app_host_sas_web_yp,hamster_src_setup_man_web_yp,production_src_setup_sas_web_yp,hamster_src_setup_vla_web_yp,production_app_host_sas_web_yp,production_app_host_vla_web_yp,hamster_src_setup_sas_web_yp,prestable_src_setup_sas_web_yp,production_src_setup_vla_web_yp,hamster_app_host_vla_web_yp&recentSnapshotsCount=5).

## Src_setup
#### Что это?
Сервант аппхоста, через конфиг которого, можно завести прокси для источников, которые тяжело переводить на протокол аппхоста (либо если просто нужно быстро перевести сервис под аппхост, но часть источников не готова).
SRC_SETUP - платформа для написания аппхостовых сервантов.
#### Что может взорвать?
Web.
#### Когда обычно приезжает в очередь?
По будням в рабочие часы.
#### Когда обычно катим?
По будням в рабочие часы.
#### Сколько катится?
1,5ч
#### Как катать?
В searchmon очереди тикеты вида `src_setup`. проваливаемся в сервис, затем в дашборд [app_host](https://nanny.yandex-team.ru/ui/#/services/dashboards/catalog/app_host). Комитим тикеты, далее deploy, рецепт `src_setup_ppsa_with_locks_queue`.
#### Кого призывать при проблемах?
@elshiko в чате [SrcSetup Releases](https://t.me/joinchat/BwkfgA6-Mif5lJ7PnNCkpA)
#### Как откатывать?
Через [revert view](https://nanny.yandex-team.ru/ui/#/services/group_revert?serviceIds=hamster_app_host_man_pre_web_yp%2Chamster_app_host_man_web_yp%2Chamster_app_host_sas_web_yp%2Chamster_app_host_vla_web_yp%2Cprestable_app_host_sas_web_yp%2Cprestable_exp_app_host_sas_web_yp%2Cproduction_app_host_man_web_yp%2Cproduction_app_host_sas_web_yp%2Cproduction_app_host_vla_web_yp&recentSnapshotsCount=5).


## Эксперименты
#### Что это?
Эксперимент - это возможность протестировать любое новшество (или изменение существующей функциональности) на контролируемой (небольшой) по размеру аудитории пользователей Яндекса. Это обязательный этап для запуска новой функциональности на Поиске.
#### Что может взорвать?
Главная опасность выкатки экспериментов в том, что взорваться может что угодно, из-за этого не рекомендуется выкатка экспериментов совместно с релизами затрудняяющими установить причину проблемы (балансер, антиробот, голован)
#### Когда обычно приезжает в очередь?
По будням два раза в день - утренняя и вечерняя выкладка, в выходной как правило один раз в день.
#### Когда обычно катим?
По будням желательно успеть прокатить утреннюю и вечернюю выкатку экспериментов, из-за этого если в rviewer будет очередь - экспериментам будет одна приоритет, сразу переместятся вверх очреди. В выходные марти выкатывает релиз экспериментов в дневное время.
#### Сколько катится?
30 минут. Это 5 минут на prestable sas, 20 минут пауза, далее 5 минут на все локации сразу.
#### Как катать?
Эксперемнты катаются рецептом няни через таскгруппу а не дашборд. Выбрать в searchmon очереди `Update experements to config #`, провалиться в сам сервис production_experements_nginx, в последнем снепшоте выбрать в `taskgroup` ссылку на `deploy-XXXXXXX`.
#### Кого призывать при проблемах?
При проблемах, эксперементы можно сразу откатить - это быстро. Далее нужны дежурные от [сервиса ab](https://warden.yandex-team.ru/components/ab).
#### Как откатывать?
Если выкатка еще идет - то reject на странице деплоя, далее на странице сервиса в няне rollback на последнем снепшоте. Далее проверить какой сейчас current снепшот.
Помимо инцидентного чата указанного в warden, следует писать при проблемах и в [этот](https://t.me/joinchat/CyCSrknStrKg0dT24S2GXA).

## Флаги
#### Что это?
Прошедшие проверку эксперименты, теперь уже на всех пользователей
#### Что может взорвать?
Взорвать могут также все, но катятся полокационно.
#### Когда обычно приезжает в очередь?
по будням в рабочее время
#### Когда обычно катим?
по будням в рабочее время
#### Сколько катится?
1,5ч
#### Как катать?
В searchmon выбираем релиз вида `SEAREL-*: Update flags.json to the version * [web]`. Проваливаемся в любой сервис, затем в дашборд [report_data_all](https://nanny.yandex-team.ru/ui/#/services/dashboards/catalog/report_data_all), накомичиваем тикеты нужного релиза, далее deploy, рецепт new_shiny_flags_deploy_with_locks.
#### Кого призывать при проблемах?
Чат [выкатка на 100%](https://t.me/joinchat/Tqp1-86s8c9_Bz7f). @buryakov + @assenova + дежурный от [ab/uaas](https://warden.z.yandex-team.ru/components/ab/s/uaas).
#### Как откатывать?
Через [revert view](https://nanny.yandex-team.ru/ui/#/services/group_revert?serviceIds=hamster_flags_provider_man_web_yp%2Chamster_flags_provider_sas_web_yp%2Chamster_flags_provider_vla_web_yp%2Cprestable_flags_provider_sas_web_yp%2Cproduction_flags_provider_man_web_yp%2Cproduction_flags_provider_sas_web_yp%2Cproduction_flags_provider_vla_web_yp&recentSnapshotsCount=5).

## Словари
#### Что это?
Словари SDCH для графов в аппхосте  
#### Что может взорвать?
WEB-поиск  
#### Когда обычно приезжает в очередь?
В выходные
#### Когда обычно катим?
Выходные, днем, при наличии события в желтом календаре плановых работ([ПРИМЕР](https://calendar.yandex-team.ru/event/52116743?applyToFuture=1&event_date=2022-01-16T09%3A00%3A00&layerId=63324))  
#### Сколько катится?
Каждая  фаза 20-30 минут  
#### Как катать?
1. Развернуть 1-ую фазу в очереди [SEARCHMON](https://nanny.yandex-team.ru/ui/#/queues/meta/SEARCHMON/releases)

   {% cut "Разворот фазы" %}

     ![1](_imgs/SDCH1.png)

   {% endcut %}

1. Выбрать любой сервис в 1-ой фазе

   {% cut "Выбор сервиса" %}

     ![2](_imgs/SDCH2.png)

   {% endcut %}

1. Выбрать Dashboards Refs на странице сервиса

   {% cut "Dashboard Refs" %}

     ![3](_imgs/SDCH3.png)

   {% endcut %}

1. Выбрать sdch encoders dashboard

   {% cut "sdch encoders dashboard" %}

     ![4](_imgs/SDCH4.png)

   {% endcut %}

1. **ТОЛЬКО ДЛЯ ОДНОЙ ФАЗЫ В ПОРЯДКЕ ОЧЕРЕДИ** Select & Commit 

   {% cut "Select&Commit" %}

     ![5](_imgs/SDCH5.png)

   {% endcut %}

1. Только убедившись в коммитах **ОДНОЙ ИЗ ФАЗ В ПОРЯДКЕ ОЧЕРЕДИ** в [SEARCHMON](https://nanny.yandex-team.ru/ui/#/queues/meta/SEARCHMON/releases) - нажать Deploy

   {% cut "Deploy" %}

     ![6](_imgs/SDCH6.png)

   {% endcut %}

1. Выбрать рецепт из выпадающего списка: default

   {% cut "Рецепт default" %}

     ![7](_imgs/SDCH7.png)

   {% endcut %}

1. Проверить, что изменения коснулись только номеров id

   {% cut "Проверка diff'ов" %}

     ![8](_imgs/SDCH8.png)

   {% endcut %}

Только при полном окончании 1-ой фазы, переходим к следующей, по порядковому номеру фазы. 
#### Кого призывать при проблемах?
@feldsherov
#### Как откатывать?
При необходимости воспользоваться [revert view](https://nanny.yandex-team.ru/ui/#/services/group_revert?serviceIds=man_sdch_encoder_yp%2Csas_sdch_encoder_yp%2Cvla_sdch_encoder_yp&recentSnapshotsCount=5).

## Report
####  Что это?
Исторически report-ом называлась часть Поиска, написанная на perl и работающая в связке с Apache. Она принимала входящий запрос пользователя, проводила его минимальную предобработку, затем перенаправляла запрос в ReqWizard (Колдунщик запросов, ныне Begemot), а обогащённый колдунщиком запрос - в метапоиски. Ответ метапоиска передавался затем в шаблонизатор (templates) и отправлялся пользователю.
В настоящее время вся эта нетривиальная логика переехала в граф под apphost, часть логики предобработки - в http_adapter.
#### Что может взорвать?
Верхний метапоиск (upper, noapache).
#### Когда обычно приезжает в очередь?
В дневное время по будням, с примерной периодичностью 1 раз в месяц.
#### Когда обычно катим?
В дневное время по будням
#### Сколько катится?
1,5ч
#### Как катать?
В searchmon будет релиз с маской в названии: `report*report_core_package`.
Далее через дашборд [report](https://nanny.yandex-team.ru/ui/#/services/dashboards/catalog/report) сделать commit тикетов, для deploy использовать рецепт `manual_confirmed_prepare_and_deploy_optimized_with_locks_queue`.
#### Кого призывать при проблемах?
Дежурных от [report](https://warden.yandex-team.ru/components/web/s/report).
#### Как откатывать?
Через [revert view](https://nanny.yandex-team.ru/ui/#/services/group_revert?serviceIds=production_report_man_web_yp%2Chamster_report_sas_web_yp%2Cproduction_report_vla_web_yp%2Chamster_report_vla_web_yp%2Cproduction_report_sas_web_yp%2Chamster_report_man_web_yp%2Cprestable_report_sas_web_yp&recentSnapshotsCount=5).

## Begemot
#### Что это?
Сервис, который преобразует исходный запрос пользователя в формат, понятный поисковому рантайму (разбор запроса, обогащение синонимами, представление в виде qtree/reqbundle), считает запросные факторы, классифицирует запрос.
#### Что может взорвать?
Используется в вебе, видео, картинках, Алисе, геопоиске, а также поиске музыки, маркета, этушки и всяких других.
Катить в прайм-тайм нельзя, т.к. размывает кеш на средних.
#### Когда обычно приезжает в очередь?
Вечером, после 22:00 по будням
####  Когда обычно катим?
После 23:00 по будням перед выкаткой баз поискового индекса.
#### Сколько катится?
3ч.
#### Как катать?
Обычно дежурные оставляют подготовку деплоя выполненой, необходимо подтвердить деплой в дашборде, выбрать рецепт `deploy_day_fast`.
#### Кого призывать при проблемах?
[gluk47@](https://staff.yandex-team.ru/gluk47), если не удается связаться то дежурные от [begemot](https://warden.yandex-team.ru/components/begemot). Чат [begemoting](https://t.me/joinchat/B5EDfEDnX06iR6GTsfKrEw). При проблемах необходимо сделать SPI и прилинковать к [SPPROBLEM-421](https://st.yandex-team.ru/SPPROBLEM-421#601d30b5375d271c3d9a84ae)
#### Как откатывать?
Через дежурных от [begemot](https://warden.yandex-team.ru/components/begemot).
