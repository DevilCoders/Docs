# ML User Features

Скрипт позволяет просто набрать нужные вам признаки пользователей, и удобно подготовить табличку для запуска на ней катбуста.

## Признаки
Существущие признаки в основном поделены на группы:
* socdem: категориальные признаки из Крипты - gender, age, income
* interests: разные сегменты интересов из Крипты - shortterm_interests, longterm_interests, interests_composite, heuristic_segments, marketing_segments, probabilistic_segments, lal_common, heuristic_common
* vectors: ежемесячные векторы, построенные по сайтам Бразуера и Метрики - monthly_yandexuid_vectors_b, monthly_yandexuid_vectors_m (TODO: добавить ежедневные векторы и векторы, построенные по приложениям)
* geo: категориальные признаки - main_region, main_region_country, main_region_obl, main_region_city
* sessions: построенные по активности пользователя в браузере - webview, ip_activity_type, browser
* device: категориальные фичи с информацией о девайсе пользователя - is_mobile, device_type, vendor, os
* sites: категориальные фичи c часто посещаемыми сайтами: affinitive_sites, top_common_sites (TODO: сейчас слишком много сайтов, чтобы можно было пользоваться, нужно обрезать мало посещаемые)

Также есть отдельная фича
* yandex_loyalty - доля визитов на ресурсы Яндекса относительно посещений конкурирующих сервисов

## Таск
Примеры тасков можно посмотреть в example_collect_features_task и detect_user_cost_task. Таск состоит из следующих разделов:

* глобальные опции yt_proxy, tmp_prefix, test, test_tmp_prefix, key
* features - опции для выбора нужных признаков
* subtasks - подтаски, для которых будут собираться эти признаки. В табличку dst_features будт сохранены сами признаки всех юзеров, dst_cd - это column description табличка с описанием принаков, нужная для запуска catboost на ней. В разделе new_features можно описать все дополнительные фичи, которые вам нужны, с опциями table - откуда брать эту фичу, name - название колонки из этой таблицы, feature_type - тип, is_target - является ли фича таргетом, inner_join - нужно ли при джойне выкидывать юзеров, у которых нет этой фичи.

## Как запустить на получившихся табличках Catboost
Воспользоваться скриптом [ads/ml_user_catboost](https://a.yandex-team.ru/arc/trunk/arcadia/ads/ml_user_features)
