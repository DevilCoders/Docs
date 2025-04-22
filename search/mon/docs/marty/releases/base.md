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
1. Найти тикет вида `web db index` в очереди [SEARCHMON](https://nanny.yandex-team.ru/ui/#/queues/meta/SEARCHMON/releases)

   {% cut "Тикет" %}

     ![1](_imgs/web_base1.png)

   {% endcut %}

1. Провалиться в него, в ссылку вида `SANDBOX_RELEASE`

   {% cut "Переход в тикет" %}

     ![2](_imgs/web_base2.png)

   {% endcut %}

1. Выделить все тикеты через Select All.

1.  Далее `commit`.

1. В описании есть ссылка на рецепт - провалиться в нее

   {% cut "Ссылка на рецепт" %}

     ![3](_imgs/web_base3.png)

   {% endcut %}

1. Подождать прогрузку и выбрать `Apply through Nanny`.
1. Глазами проверить, что в рецепте выкладки новые ревизии снапшотов (может быть баг, и ревизия останется старой, тогда вся база никуда не поедет)
1. Далее будет ссылка на деплой - идти туда

   {% cut "Ссылка на deploy" %}

     ![4](_imgs/web_base4.png)

   {% endcut %}

1. В depoy можно сразу выбрать summary view.
1. В 2:00 выбираем в summary view `Close SAS`. Рецепт сам выставит downtime и уведет трафик из ДЦ.
1. Ждем на икностасе по графикам Веб Поиска в Сасово серых no data и когда уйдет полностью трафик на графиках.
1. Как трафик ушел - жмем `Start Switch SAS`.
1. Как базы допереключаться, будет heat up локации, далее появится `pre open`. Это дает 5% трафика, сразу нажимать не надо, а подождать пока [sas_age и sas_nocache_age](https://yasm.yandex-team.ru/panel/web_quality) станут меньше 30 а лучше меньше 20, также смотрим на sinsig - МКБР график и в целом чтобы ничего не критовало.
1. После `pre open` ждем минут 15.
1. Обычно критует [кеш](https://yasm.yandex-team.ru/alert/web_mmeta_tmpl_alerts.ASEARCH.mmeta_prestable_web-main_sas_yandsearch.cache-found) - это нормально.
1. Если проблем нет - переходим к `open SAS`.
1. Ждем минут 5-7 и убираем Confirm'ом все downtime на локацию.
1. Если все ок - идем дальше и конфирмим `Close MAN for switch`.
1. Повторить для MAN.
1. Повторить для VLA.

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
1. Найти тикет вида `video db index` в очереди [SEARCHMON](https://nanny.yandex-team.ru/ui/#/queues/meta/SEARCHMON/releases)

   {% cut "Тикет" %}

     ![1](_imgs/video_base1.png)

   {% endcut %}

1. Провалиться в один из сервисов

   {% cut "Переход в сервис" %}

     ![2](_imgs/video_base2.png)

   {% endcut %}

1. Перейти в dashboard [Video_base_searches](https://nanny.yandex-team.ru/ui/#/services/dashboards/catalog/video_base).

   {% cut "Dashboard" %}

     ![3](_imgs/video_base3.png)

   {% endcut %}

1. Выбрать сортировку по itype

   {% cut "Сортировка по itype" %}

     ![4](_imgs/video_base4.png)

   {% endcut %}

1. Cкопировать версию из названия релиза в очереди [SEARCHMON](https://nanny.yandex-team.ru/ui/#/queues/meta/SEARCHMON/releases)

   {% cut "Версия релиза" %}

     ![5](_imgs/video_base5.png)

   {% endcut %}

1. Сделать на дашборде поиск по странице с этим номером и накоммичивать снизу вверх

   {% cut "Commit снизу вверх по фильтру" %}

     ![6](_imgs/video_base6.png)

   {% endcut %}

1. Проверить, что все вкомиичено в очереди [SEARCHMON](https://nanny.yandex-team.ru/ui/#/queues/meta/SEARCHMON/releases)

   {% cut "Commit с проверкой" %}

     ![7](_imgs/video_base7.png)

   {% endcut %}

1. Выбрать рецепт выкатки из описания, обычно это `deploy_video_database_with_locks_queue`.
1. Выкатить полокационно вместе с другими базами.
1. В последнее время участились случая, при открытии локации возрастает график деградации (красные горбики) на графике базовых, необходимо перед переходом к другой локации на переключение дождаться пока он спадет.
#### Кого призывать при проблемах?
Дежурных от видео [warden](https://warden.z.yandex-team.ru/components/video)
#### Как откатывать?
При необходимости отката, Марти должен призвать ответственного за релиз девопса и дежурного девопса для отката базы, но при необходимости может начать откат через [revert view](https://nanny.yandex-team.ru/ui/#/services/group_revert?serviceIds=vla-video-base-resources%2Cvideo_int_pip%2Cvla_video_int_hamster%2Cman_video_remote_storage%2Csas_video_remote_storage%2Cproduction_hamster_prs_vidmmeta_sas%2Cproduction_hamster_vidmmeta_sas%2Csaas_refresh_hamster_vhs_base_yp%2Cvla_video_int%2Cvla_video_multibeta_mmeta%2Csas-video-base-resources%2Cvideo_base_pip%2Csas_video_int%2Cproduction_hamster_vidmmeta_man%2Csaas_refresh_production_vhs_base_vla_yp%2Csaas_refresh_production_video_base_man%2Cproduction_vidmmeta_sas%2Cvla_video_multibeta_int%2Cman-video-embedding-resources%2Cproduction_hamster_prs_vidmmeta_vla%2Csas_video_int_hamster%2Csas-video-embedding-resources%2Cproduction_hamster_prs_vidmmeta_man%2Cman-video-invindex-resources%2Csaas_refresh_production_vhs_base_man_yp%2Csaas_refresh_production_vhs_base_sas_yp%2Cvla-video-embedding-resources%2Csas-video-invindex-resources%2Csaas_refresh_production_video_base_sas%2Cman_video_int%2Cman_video_int_hamster%2Cproduction_vidmmeta_vla%2Cvideo_base_pip_platinum%2Csaas_refresh_production_video_base_vla%2Cvideo_mmeta_pip%2Cvla_video_remote_storage%2Cman-video-base-resources%2Cvla_video_inverted_index_pip%2Csaas_refresh_hamster_video_base_sas%2Cvla_video_multimeta_mmeta%2Csaas_refresh_hamster_video_base_man%2Cproduction_vidmmeta_man%2Cvla_video_multibeta_united_rtyserver%2Cvla_video_multibeta_united_deploy%2Csaas_refresh_hamster_video_base_vla%2Cvla_video_embedding_pip%2Cvla-video-invindex-resources%2Cproduction_hamster_vidmmeta_vla&recentSnapshotsCount=5).
