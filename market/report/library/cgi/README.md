# Документация компонента ```Market Report```

## Оглавление:
1. [Раздел 1. Параметры ```place```](#section-1-place)
2. [Раздел 2. Параметры ```cgi```](#section-2-cgi)


## Определение place
Основной интерфейс компонента market report

## Определение cgi
Различного рода входные параметры

<br>

## Section 1 Place
<br>

#### Place: <b>[REST_SERVICE_METHOD](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.cpp?rev=20450873c10bb360c6907a893e6bd65badbdb721#L578)</b>
Описание:
 Дутый плейс для экспериментального рестового интерфейса репорта<br/>
Пример использования:
```example: &place=REST_SERVICE_METHOD...```<br/>

---

#### Place: <b>[accessories](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.cpp?rev=20450873c10bb360c6907a893e6bd65badbdb721#L533)</b>
Описание:
 Выдает список сопутствующих товаров<br/>
Пример использования:
```example: &place=accessories...```<br/><b>[..."&place=accessories"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_accessories.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L135)</b><br/><b>[..."&place=accessories"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_accessories_facets.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L64)</b><br/><b>[..."&place=accessories"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_accessories_facets.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L115)</b><br/>

---

#### Place: <b>[actual_delivery](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.cpp?rev=20450873c10bb360c6907a893e6bd65badbdb721#L565)</b>
Описание:
 Выдает актуальные условия доставки для группы синих офферов<br/>
Пример использования:
```example: &place=actual_delivery...```<br/><b>[..."&place=actual_delivery"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_actual_delivery_saashub.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L242)</b><br/><b>[..."&place=actual_delivery"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_actual_delivery_saashub.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L269)</b><br/><b>[..."&place=actual_delivery"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_actual_delivery_saashub.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L301)</b><br/>

---

#### Place: <b>[advertising_carousel](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.cpp?rev=20450873c10bb360c6907a893e6bd65badbdb721#L631)</b>
Описание:
 https://st.yandex-team.ru/MARKETOUT-38182 https://st.yandex-team.ru/MARKETOUT-42180 Рекламная карусель "Товары с высоким рейтингом"<br/>
Пример использования:
```example: &place=advertising_carousel...```<br/><b>[..."&place=advertising_carousel"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_advertising_carousel.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L150)</b><br/><b>[..."&place=advertising_carousel"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_advertising_carousel.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L189)</b><br/><b>[..."&place=advertising_carousel"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_advertising_carousel.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L276)</b><br/>

---

#### Place: <b>[also_viewed](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.cpp?rev=20450873c10bb360c6907a893e6bd65badbdb721#L569)</b>
Описание:
 https://st.yandex-team.ru/MARKETOUT-16817 Модели-рекомендации "видевшие также смотрели"<br/>
Пример использования:
```example: &place=also_viewed...```<br/><b>[..."&place=also_viewe"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_also_viewed_cpa_boosted.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L13)</b><br/><b>[..."&place=also_viewe"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_also_viewed_cpa_boosted.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L19)</b><br/><b>[..."&place=also_viewed"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_also_viewed_cpa_boosted.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L58)</b><br/>

---

#### Place: <b>[alt_same_shop](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.cpp?rev=20450873c10bb360c6907a893e6bd65badbdb721#L537)</b>
Описание:
 Выдает те же товары, только в одном магазине<br/>
Пример использования:
```example: &place=alt_same_shop...```<br/><b>[..."&place=alt_same_shop"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_alt_same_shop.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L970)</b><br/><b>[..."&place=alt_same_shop"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_alt_same_shop.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1003)</b><br/><b>[..."&place=alt_same_shop"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_alt_same_shop.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1070)</b><br/>

---

#### Place: <b>[api_offerauction](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.cpp?rev=20450873c10bb360c6907a893e6bd65badbdb721#L503)</b>
Описание:
 Для внутреннего использования репортом<br/>
Пример использования:
```example: &place=api_offerauction...```<br/><b>[..."&place=api_offerauction"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_apiofferauction.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L24)</b><br/><b>[..."&place=api_offerauction"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_apiofferauction.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L42)</b><br/><b>[..."&place=api_offerauction"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_show_log.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1273)</b><br/>

---

#### Place: <b>[api_offerinfo](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.cpp?rev=20450873c10bb360c6907a893e6bd65badbdb721#L502)</b>
Описание:
 Для внутреннего использования репортом<br/>
Пример использования:
```example: &place=api_offerinfo...```<br/><b>[..."&place=api_offerinfo"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_offerinfo.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L679)</b><br/><b>[..."&place=api_offerinfo"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_offerinfo.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L706)</b><br/>

---

#### Place: <b>[articles](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.cpp?rev=20450873c10bb360c6907a893e6bd65badbdb721#L524)</b>
Описание:
 Поиск персональных статей и подборок в репорте https://st.yandex-team.ru/MARKETOUT-9231<br/>
Пример использования:
```example: &place=articles...```<br/><b>[..."&place=articles"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_articles.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L120)</b><br/><b>[..."&place=articles"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_articles.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L139)</b><br/><b>[..."&place=articles"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_articles.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L157)</b><br/>

---

#### Place: <b>[attractive_models](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.cpp?rev=20450873c10bb360c6907a893e6bd65badbdb721#L571)</b>
Описание:
 https://st.yandex-team.ru/MARKETOUT-17626 Отдает модели, рекомендуемые OMM на морде маркета<br/>
Пример использования:
```example: &place=attractive_models...```<br/><b>[..."&place=attractive_models"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_recom_banned_categories.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L454)</b><br/><b>[..."&place=attractive_models"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_golovan_metrics.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L73)</b><br/><b>[..."&place=attractive_models"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_dj.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2114)</b><br/>

---

#### Place: <b>[attractive_offers](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.cpp?rev=20450873c10bb360c6907a893e6bd65badbdb721#L561)</b>
Описание:
 https://st.yandex-team.ru/MARKETOUT-15888 Плейс для получение потенциально интересных офферов<br/>
Пример использования:
```example: &place=attractive_offers...```<br/>

---

#### Place: <b>[beru_bonuses](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.cpp?rev=20450873c10bb360c6907a893e6bd65badbdb721#L597)</b>
Описание:
 https://st.yandex-team.ru/MARKETOUT-24305 Реклама Беру на белом<br/>
Пример использования:
```example: &place=beru_bonuses...```<br/><b>[..."&place=beru_bonuses"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_beru_bonuses.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L450)</b><br/>

---

#### Place: <b>[best_model_reviews](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.cpp?rev=20450873c10bb360c6907a893e6bd65badbdb721#L558)</b>
Описание:
 https://st.yandex-team.ru/MARKETOUT-14620 Сделать плейс для получения лучших отзывов<br/>
Пример использования:
```example: &place=best_model_reviews...```<br/><b>[..."&place=best_model_reviews"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_best_model_grades.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L36)</b><br/><b>[..."&place=best_model_reviews"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_best_model_grades.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L73)</b><br/>

---

#### Place: <b>[bestdeals](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.cpp?rev=20450873c10bb360c6907a893e6bd65badbdb721#L498)</b>
Описание:
 Выдает 30 лучших кластеров со скидками<br/>
Пример использования:
```example: &place=bestdeals...```<br/><b>[..."&place=bestdeals"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_bestdeals_personal.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L95)</b><br/><b>[..."&place=bestdeals"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_bestdeals_personal.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L103)</b><br/><b>[..."&place=bestdeals"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_bestdeals_personal.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L111)</b><br/>

---

#### Place: <b>[better_price](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.cpp?rev=20450873c10bb360c6907a893e6bd65badbdb721#L548)</b>
Описание:
 https://st.yandex-team.ru/MARKETOUT-12488 У нас дешевле<br/>
Пример использования:
```example: &place=better_price...```<br/><b>[..."&place=better_pric"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_models_with_offers.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L185)</b><br/><b>[..."&place=better_price"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_models_with_offers.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L220)</b><br/><b>[..."&place=better_price"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_recom_banned_categories.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L500)</b><br/>

---

#### Place: <b>[bids_recommender](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.cpp?rev=20450873c10bb360c6907a893e6bd65badbdb721#L506)</b>
Описание:
 Показывает CPA рекомендации<br/>
Пример использования:
```example: &place=bids_recommender...```<br/><b>[..."&place=bids_recommender"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_bids_recommender_formulas.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L38)</b><br/><b>[..."&place=bids_recommender"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_bids_recommender_cpa_uncollapse.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L293)</b><br/><b>[..."&place=bids_recommender"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_bids_recommender_cpa_uncollapse.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L363)</b><br/>

---

#### Place: <b>[blender](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.cpp?rev=20450873c10bb360c6907a893e6bd65badbdb721#L612)</b>
Описание:
 Блендер https://st.yandex-team.ru/MARKETSEARCH-335<br/>
Пример использования:
```example: &place=blender...```<br/><b>[..."&place=blender"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_rerequests.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L406)</b><br/><b>[..."&place=blender"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_blender_bundles_catalog_quiz.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L134)</b><br/><b>[..."&place=blender"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_blender_bundles_catalog_quiz.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L196)</b><br/>

---

#### Place: <b>[blue_ads](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.cpp?rev=20450873c10bb360c6907a893e6bd65badbdb721#L596)</b>
Описание:
 https://st.yandex-team.ru/MARKETOUT-24305 Реклама Беру на белом<br/>
Пример использования:
```example: &place=blue_ads...```<br/>

---

#### Place: <b>[blue_attractive_models](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.cpp?rev=20450873c10bb360c6907a893e6bd65badbdb721#L577)</b>
Описание:
 https://st.yandex-team.ru/MARKETOUT-18867 Отдает модели, рекомендуемые OMM на синем маркете<br/>
Пример использования:
```example: &place=blue_attractive_models...```<br/><b>[..."&place=blue_attractive_models"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_omm.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L131)</b><br/><b>[..."&place=blue_attractive_models"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_omm.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L135)</b><br/><b>[..."&place=blue_attractive_models"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_omm.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L370)</b><br/>

---

#### Place: <b>[blue_omm_findings](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.cpp?rev=20450873c10bb360c6907a893e6bd65badbdb721#L590)</b>
Описание:
 https://st.yandex-team.ru/MARKETOUT-21580 Отдает модели, рекомендуемые OMM в ленте на морде Беру<br/>
Пример использования:
```example: &place=blue_omm_findings...```<br/><b>[..."&place=blue_omm_findings"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_omm.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L541)</b><br/><b>[..."&place=blue_omm_findings"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_omm.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L557)</b><br/><b>[..."&place=blue_omm_findings"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_omm.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L576)</b><br/>

---

#### Place: <b>[blue_tariffs](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.cpp?rev=20450873c10bb360c6907a893e6bd65badbdb721#L617)</b>
Описание:
 https://st.yandex-team.ru/MARKETOUT-34200 Ручка для выдачи информации о доставке на синем маркете. Тарифы и сроки.<br/>
Пример использования:
```example: &place=blue_tariffs...```<br/><b>[..."&place=blue_tariffs"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_place_blue_tariffs.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L698)</b><br/><b>[..."&place=blue_tariffs"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_place_blue_tariffs.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L716)</b><br/><b>[..."&place=blue_tariffs"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_place_blue_tariffs.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L770)</b><br/>

---

#### Place: <b>[book_now_incut](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.cpp?rev=20450873c10bb360c6907a893e6bd65badbdb721#L512)</b>
Описание:
 Запрос за врезкой для магазинов подключенных в систему бронирования<br/>
Пример использования:
```example: &place=book_now_incut...```<br/><b>[..."&place=book_now_incut"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_book_now_ctr.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L32)</b><br/><b>[..."&place=book_now_incut"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_book_now_ctr.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L59)</b><br/><b>[..."&place=book_now_incut"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_error_format.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L70)</b><br/>

---

#### Place: <b>[brand_products](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.cpp?rev=20450873c10bb360c6907a893e6bd65badbdb721#L541)</b>
Описание:
 Плейс для страницы товаров бренда в кабинете вендора<br/>
Пример использования:
```example: &place=brand_products...```<br/><b>[..."&place=brand_products"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_reqwizard.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L312)</b><br/><b>[..."&place=brand_products"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_lingboost.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L43)</b><br/><b>[..."&place=brand_products"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_brand_products.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L444)</b><br/>

---

#### Place: <b>[brandbestdeals](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.cpp?rev=20450873c10bb360c6907a893e6bd65badbdb721#L499)</b>
Описание:
 Выдает лучшие кластеры из 120 популярных категорий бренда (bestdeals от результатов top_categories)<br/>
Пример использования:
```example: &place=brandbestdeals...```<br/><b>[..."&place=brandbestdeals"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_brandbestdeals.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L69)</b><br/><b>[..."&place=brandbestdeals"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_brandbestdeals.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L119)</b><br/><b>[..."&place=brandbestdeals"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_brandbestdeals.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L134)</b><br/>

---

#### Place: <b>[business_info](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.cpp?rev=20450873c10bb360c6907a893e6bd65badbdb721#L544)</b>
Описание:
 https://st.yandex-team.ru/MARKETOUT-36107 Информация о бизнесе<br/>
Пример использования:
```example: &place=business_info...```<br/><b>[..."&place=business_info"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_business_info.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L94)</b><br/><b>[..."&place=business_info"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_business_info.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L117)</b><br/><b>[..."&place=business_info"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_express_delivery.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L731)</b><br/>

---

#### Place: <b>[cart_models](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.cpp?rev=20450873c10bb360c6907a893e6bd65badbdb721#L553)</b>
Описание:
 Плейс для поиска товаров, которые есть одновременно в одном магазине<br/>
Пример использования:
```example: &place=cart_models...```<br/><b>[..."&place=cart_models"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_cart_models.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L36)</b><br/>

---

#### Place: <b>[categories_and_models_by_history](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.cpp?rev=20450873c10bb360c6907a893e6bd65badbdb721#L568)</b>
Описание:
 https://st.yandex-team.ru/MARKETOUT-17265: Оптимизировать запросы отзывов на морде<br/>
Пример использования:
```example: &place=categories_and_models_by_history...```<br/><b>[..."&place=categories_and_models_by_history"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_recom_banned_categories.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L338)</b><br/><b>[..."&place=categories_and_models_by_histor"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_categories_and_models_by_history.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L31)</b><br/><b>[..."&place=categories_and_models_by_history"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_categories_and_models_by_history.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L172)</b><br/>

---

#### Place: <b>[categories_by_history](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.cpp?rev=20450873c10bb360c6907a893e6bd65badbdb721#L567)</b>
Описание:
 https://st.yandex-team.ru/MARKETOUT-16851 Персональные категории из истории просмотров<br/>
Пример использования:
```example: &place=categories_by_history...```<br/><b>[..."&place=categories_by_histor"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_categories_by_history.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L14)</b><br/><b>[..."&place=categories_by_history"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_categories_by_history.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L91)</b><br/><b>[..."&place=categories_by_history"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_categories_by_history.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L102)</b><br/>

---

#### Place: <b>[check_delivery_available](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.cpp?rev=20450873c10bb360c6907a893e6bd65badbdb721#L585)</b>
Описание:
 https://st.yandex-team.ru/MARKETOUT-20187 проверка возможности доставки в регион<br/>
Пример использования:
```example: &place=check_delivery_available...```<br/><b>[..."&place=check_delivery_available"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_prohibited_blue_offers.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L909)</b><br/><b>[..."&place=check_delivery_available"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_prohibited_blue_offers.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L913)</b><br/><b>[..."&place=check_delivery_available"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_check_delivery_available.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L269)</b><br/>

---

#### Place: <b>[check_filters](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.cpp?rev=20450873c10bb360c6907a893e6bd65badbdb721#L603)</b>
Описание:
 https://st.yandex-team.ru/MARKETOUT-27616 Ручка для валидации фильров в конкретной категории на Беру (сквозные фильтры)<br/>
Пример использования:
```example: &place=check_filters...```<br/><b>[..."&place=check_filters"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_check_filters.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L34)</b><br/><b>[..."&place=check_filters"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_check_filters.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L50)</b><br/><b>[..."&place=check_filters"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_check_filters.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L67)</b><br/>

---

#### Place: <b>[check_models_in_marketplace](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.cpp?rev=20450873c10bb360c6907a893e6bd65badbdb721#L615)</b>
Описание:
 https://st.yandex-team.ru/MARKETOUT-34038?<br/>
Пример использования:
```example: &place=check_models_in_marketplace...```<br/><b>[..."&place=check_models_in_marketplace"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_check_models_in_marketplace.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L113)</b><br/>

---

#### Place: <b>[check_offers](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.cpp?rev=20450873c10bb360c6907a893e6bd65badbdb721#L593)</b>
Описание:
 https://st.yandex-team.ru/MARKETOUT-24283 Ручка для ПАПИ для проверки наличия офферов и их модельности<br/>
Пример использования:
```example: &place=check_offers...```<br/><b>[..."&place=check_offers"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_check_offers.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L97)</b><br/><b>[..."&place=check_offers"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_check_offers.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L99)</b><br/><b>[..."&place=check_offers"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_check_offers.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L121)</b><br/>

---

#### Place: <b>[check_prices](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.cpp?rev=20450873c10bb360c6907a893e6bd65badbdb721#L595)</b>
Описание:
 https://st.yandex-team.ru/MARKETOUT-24379 Ручка для ДЦО для получения акутальных цен по списку офферов или магазинов+msku<br/>
Пример использования:
```example: &place=check_prices...```<br/><b>[..."&place=check_prices"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_blue_promo_direct_discount.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2928)</b><br/><b>[..."&place=check_prices"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_check_prices.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L211)</b><br/><b>[..."&place=check_prices"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_check_prices.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L240)</b><br/>

---

#### Place: <b>[collect_promo_secondary_items](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.cpp?rev=20450873c10bb360c6907a893e6bd65badbdb721#L607)</b>
Описание:
 https://st.yandex-team.ru/MARKETOUT-30806: Плейс для получения доступных подарочных офферов<br/>
Пример использования:
```example: &place=collect_promo_secondary_items...```<br/><b>[..."&place=collect_promo_secondary_items"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_collect_promo_secondary_items.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L135)</b><br/><b>[..."&place=collect_promo_secondary_items"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_fast_promos.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1164)</b><br/>

---

#### Place: <b>[collections](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.cpp?rev=20450873c10bb360c6907a893e6bd65badbdb721#L525)</b>
Описание:
 Поиск коллекций https://st.yandex-team.ru/MARKETOUT-9231<br/>
Пример использования:
```example: &place=collections...```<br/><b>[..."&place=collections"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_collections.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L142)</b><br/><b>[..."&place=collections"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_collections.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L161)</b><br/><b>[..."&place=collections"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_collections.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L179)</b><br/>

---

#### Place: <b>[combine](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.cpp?rev=20450873c10bb360c6907a893e6bd65badbdb721#L605)</b>
Описание:
 https://st.yandex-team.ru/MARKETOUT-30205: Пользовательские стратегии для консолидации и подмен<br/>
Пример использования:
```example: &place=combine...```<br/><b>[..."&place=combine"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_on_demand_delivery.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L312)</b><br/><b>[..."&place=combine"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_on_demand_delivery.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L957)</b><br/><b>[..."&place=combine"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_combine_warehouses.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L126)</b><br/>

---

#### Place: <b>[commonly_purchased](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.cpp?rev=20450873c10bb360c6907a893e6bd65badbdb721#L575)</b>
Описание:
 https://st.yandex-team.ru/MARKETOUT-17629 Отдает модели из списков универсальных и персональных категорий<br/>
Пример использования:
```example: &place=commonly_purchased...```<br/><b>[..."&place=commonly_purchased"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_recom_big_exp.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L953)</b><br/><b>[..."&place=commonly_purchased"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_recom_big_exp.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L973)</b><br/><b>[..."&place=commonly_purchased"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_default_offer_in_models.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1387)</b><br/>

---

#### Place: <b>[compare_products](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.cpp?rev=20450873c10bb360c6907a893e6bd65badbdb721#L538)</b>
Описание:
 Сравнивает параметры моделей и кластеров<br/>
Пример использования:
```example: &place=compare_products...```<br/><b>[..."&place=compare_products"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_compare_products.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L530)</b><br/><b>[..."&place=compare_products"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_compare_products.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L570)</b><br/><b>[..."&place=compare_products"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_compare_products.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L587)</b><br/>

---

#### Place: <b>[competitive_model_card](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.cpp?rev=20450873c10bb360c6907a893e6bd65badbdb721#L621)</b>
Описание:
 https://st.yandex-team.ru/MARKETOUT-34771 Ручка для получения конкурентной карточки модели по model_id<br/>
Пример использования:
```example: &place=competitive_model_card...```<br/><b>[..."&place=competitive_model_card"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_competitive_model_card.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L57)</b><br/><b>[..."&place=competitive_model_card"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_competitive_model_card.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L92)</b><br/><b>[..."&place=competitive_model_card"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_competitive_model_card.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L101)</b><br/>

---

#### Place: <b>[complementary_product_groups](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.cpp?rev=20450873c10bb360c6907a893e6bd65badbdb721#L618)</b>
Описание:
 Дополнительные продукты<br/>
Пример использования:
```example: &place=complementary_product_groups...```<br/><b>[..."&place=complementary_product_groups"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_complementary_product_groups_blue.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L155)</b><br/><b>[..."&place=complementary_product_groups"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_complementary_product_groups_blue.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L197)</b><br/><b>[..."&place=complementary_product_groups"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_complementary_product_groups_blue.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L229)</b><br/>

---

#### Place: <b>[consistency_check](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.cpp?rev=20450873c10bb360c6907a893e6bd65badbdb721#L507)</b>
Описание:
 Проверка консистентности<br/>
Пример использования:
```example: &place=consistency_check...```<br/><b>[..."&place=consistency_check"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_consistency_check.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L25)</b><br/><b>[..."&place=consistency_check"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_consistency_check.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L27)</b><br/><b>[..."&place=consistency_check"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_consistency_check.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L32)</b><br/>

---

#### Place: <b>[cpa_shop_incut](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.cpp?rev=20450873c10bb360c6907a893e6bd65badbdb721#L623)</b>
Описание:
 https://st.yandex-team.ru/MARKETOUT-36989 CPA-врезка, топ-1 офера по моделям<br/>
Пример использования:
```example: &place=cpa_shop_incut...```<br/><b>[..."&place=cpa_shop_incut"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_advertising_carousel.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L237)</b><br/><b>[..."&place=cpa_shop_incut"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_advertising_carousel.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L258)</b><br/><b>[..."&place=cpa_shop_incu"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_blender_bundles.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1373)</b><br/>

---

#### Place: <b>[credit_info](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.cpp?rev=20450873c10bb360c6907a893e6bd65badbdb721#L598)</b>
Описание:
 https://st.yandex-team.ru/MARKETOUT-24598 Выдача кредитной информации для Checkouter'а (Кредиты на Беру)<br/>
Пример использования:
```example: &place=credit_info...```<br/><b>[..."&place=credit_info"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_place_credit_info.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L208)</b><br/><b>[..."&place=credit_info"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_place_credit_info.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L234)</b><br/><b>[..."&place=credit_info"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_place_credit_info.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L309)</b><br/>

---

#### Place: <b>[currency_convert](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.cpp?rev=20450873c10bb360c6907a893e6bd65badbdb721#L542)</b>
Описание:
 https://st.yandex-team.ru/MARKETOUT-11520 Конвертация валюты<br/>
Пример использования:
```example: &place=currency_convert...```<br/><b>[..."&place=currency_convert"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_currencies_complete.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L77)</b><br/><b>[..."&place=currency_convert"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_currency_convert.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L36)</b><br/><b>[..."&place=currency_convert"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_currency_convert.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L40)</b><br/>

---

#### Place: <b>[deals](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.cpp?rev=20450873c10bb360c6907a893e6bd65badbdb721#L573)</b>
Описание:
 https://st.yandex-team.ru/MARKETOUT-17704 Отдает персональные и неперсональные скидки (если передан параметр show-personal=0 в паре с параметром hid https://st.yandex-team.ru/MARKETOUT-20870)<br/>
Пример использования:
```example: &place=deals...```<br/><b>[..."&place=deals"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_recom_banned_categories.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L418)</b><br/><b>[..."&place=deals"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_recom_big_exp.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L618)</b><br/><b>[..."&place=deals"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_recom_big_exp.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L632)</b><br/>

---

#### Place: <b>[defaultoffer](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.cpp?rev=20450873c10bb360c6907a893e6bd65badbdb721#L505)</b>
Описание:
 Показывает наиболе подходящий (с точки зрения монетизации) оффер<br/>
Пример использования:
```example: &place=defaultoffer...```<br/><b>[..."&place=defaultoffer"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_alice.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L33)</b><br/><b>[..."&place=defaultoffer"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_credit.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1121)</b><br/><b>[..."&place=defaultoffer"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_default_offer_combinator.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L311)</b><br/>

---

#### Place: <b>[delivery_route](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.cpp?rev=20450873c10bb360c6907a893e6bd65badbdb721#L611)</b>
Описание:
 https://st.yandex-team.ru/COMBINATOR-127 Получение маршрута доставки посылки от комбинатора<br/>
Пример использования:
```example: &place=delivery_route...```<br/><b>[..."&place=delivery_route"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_combinator_string_delivery_dates.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L227)</b><br/><b>[..."&place=delivery_route"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_combinator_string_delivery_dates.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L355)</b><br/><b>[..."&place=delivery_route"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_deferred_courier_delivery.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L163)</b><br/>

---

#### Place: <b>[delivery_status](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.cpp?rev=20450873c10bb360c6907a893e6bd65badbdb721#L547)</b>
Описание:
 https://st.yandex-team.ru/MARKETOUT-13021 Информация о статусе доставки по ID<br/>
Пример использования:
```example: &place=delivery_status...```<br/><b>[..."&place=delivery_status"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_delivery_status.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L29)</b><br/><b>[..."&place=delivery_status"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_delivery_status.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L38)</b><br/><b>[..."&place=delivery_status"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_delivery_status.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L45)</b><br/>

---

#### Place: <b>[dj](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.cpp?rev=20450873c10bb360c6907a893e6bd65badbdb721#L608)</b>
Описание:
 https://st.yandex-team.ru/MARKETRECOM-2205 универсальный плейс dj<br/>
Пример использования:
```example: &place=dj...```<br/><b>[..."&place=dj"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_recom_soft_ban.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L130)</b><br/><b>[..."&place=dj_links"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_dj_thematic_nid_response.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L70)</b><br/><b>[..."&place=dj_links"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_dj_thematic_nid_response.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L77)</b><br/>

---

#### Place: <b>[dj_links](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.cpp?rev=20450873c10bb360c6907a893e6bd65badbdb721#L620)</b>
Описание:
 https://st.yandex-team.ru/MARKETRECOM-2839 Ручка для dj-блоков со ссылками<br/>
Пример использования:
```example: &place=dj_links...```<br/><b>[..."&place=dj_links"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_dj_thematic_nid_response.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L70)</b><br/><b>[..."&place=dj_links"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_dj_thematic_nid_response.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L77)</b><br/><b>[..."&place=dj_links"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_dj_thematic_nid_response.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L105)</b><br/>

---

#### Place: <b>[dsp_models](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.cpp?rev=20450873c10bb360c6907a893e6bd65badbdb721#L629)</b>
Описание:
 https://st.yandex-team.ru/MARKETOUT-38182MARKETYA-86 модели для ДСП согласован https://st.yandex-team.ru/MSI-288<br/>
Пример использования:
```example: &place=dsp_models...```<br/><b>[..."&place=dsp_models"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_dsp_models.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L136)</b><br/><b>[..."&place=dsp_models"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_dsp_models.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L157)</b><br/><b>[..."&place=dsp_models"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_dsp_models.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L188)</b><br/>

---

#### Place: <b>[filter_models](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.cpp?rev=20450873c10bb360c6907a893e6bd65badbdb721#L599)</b>
Описание:
 https://st.yandex-team.ru/MARKETOUT-25338 Фильтрует переданные модели и выдает id и title отфильтрованных моделей<br/>
Пример использования:
```example: &place=filter_models...```<br/><b>[..."&place=filter_models"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_filter_models.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L43)</b><br/><b>[..."&place=filter_models"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_filter_models.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L49)</b><br/><b>[..."&place=filter_models"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_filter_models.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L53)</b><br/>

---

#### Place: <b>[formalize_gl](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.cpp?rev=20450873c10bb360c6907a893e6bd65badbdb721#L582)</b>
Описание:
 https://st.yandex-team.ru/MARKETOUT-19224 Отдаёт фильтры, которые смог формализовать по текстовому запросу и hid'у<br/>
Пример использования:
```example: &place=formalize_gl...```<br/><b>[..."&place=formalize_gl"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_place_formalize_gl.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L83)</b><br/><b>[..."&place=formalize_gl"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_place_formalize_gl.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L95)</b><br/><b>[..."&place=formalize_gl"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_place_formalize_gl.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L96)</b><br/>

---

#### Place: <b>[geo](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.cpp?rev=20450873c10bb360c6907a893e6bd65badbdb721#L521)</b>
Описание:
 Информация об аутлетах и офферах на карте<br/>
Пример использования:
```example: &place=geo...```<br/><b>[..."&place=geo"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_multi_service_pickup.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L162)</b><br/><b>[..."&place=geo"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_multi_service_pickup.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L235)</b><br/><b>[..."&place=geo"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_multi_service_pickup.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L264)</b><br/>

---

#### Place: <b>[get_eats_warehouses](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.cpp?rev=20450873c10bb360c6907a893e6bd65badbdb721#L626)</b>
Описание:
 https://st.yandex-team.ru/MARKETOUT-45016 прокси плейс для получения данных об складах ритейла Еды<br/>
Пример использования:
```example: &place=get_eats_warehouses...```<br/><b>[..."&place=get_eats_warehouses"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_get_eats_warehouses.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L97)</b><br/><b>[..."&place=get_eats_warehouses"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_get_eats_warehouses.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L264)</b><br/>

---

#### Place: <b>[hot_offers](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.cpp?rev=20450873c10bb360c6907a893e6bd65badbdb721#L602)</b>
Описание:
 https://st.yandex-team.ru/MARKETOUT-28119 Ручка "hot offers" на Беру - товары, которые выгодно покупать на Беру<br/>
Пример использования:
```example: &place=hot_offers...```<br/><b>[..."&place=hot_offers"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_hot_offers.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L133)</b><br/><b>[..."&place=hot_offers"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_hot_offers.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L152)</b><br/><b>[..."&place=hot_offers"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_hot_offers.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L172)</b><br/>

---

#### Place: <b>[images](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.cpp?rev=20450873c10bb360c6907a893e6bd65badbdb721#L504)</b>
Описание:
 Показ маркета на сервисе яндекс картинок<br/>
Пример использования:
```example: &place=images...```<br/><b>[..."&place=image"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_hide_cpc_links.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L100)</b><br/><b>[..."&place=image"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_hide_cpc_links.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L151)</b><br/><b>[..."&place=images"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_hide_cpc_links.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L153)</b><br/>

---

#### Place: <b>[lavka](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.cpp?rev=20450873c10bb360c6907a893e6bd65badbdb721#L628)</b>
Описание:
 https://st.yandex-team.ru/MARKETOUT-38182ECOMSERP-79 плейс для поиска в лавке и еде<br/>
Пример использования:
```example: &place=lavka...```<br/><b>[..."&place=lavka"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_lavka.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L117)</b><br/><b>[..."&place=lavka"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_lavka.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L126)</b><br/><b>[..."&place=lavka"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_lavka.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L138)</b><br/>

---

#### Place: <b>[madv_incut](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.cpp?rev=20450873c10bb360c6907a893e6bd65badbdb721#L632)</b>
Описание:
 https://st.yandex-team.ru/MARKETOUT-46221 мпф врезка<br/>
Пример использования:
```example: &place=madv_incut...```<br/><b>[..."&place=madv_incut"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_madv_model_card_cmc_incut.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L45)</b><br/><b>[..."&place=madv_incut"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_madv_model_card_cmc_incut.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L80)</b><br/><b>[..."&place=madv_incut"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_madv_model_card_cmc_incut.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L88)</b><br/>

---

#### Place: <b>[miprime](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.cpp?rev=20450873c10bb360c6907a893e6bd65badbdb721#L509)</b>
Описание:
 современный аналог mimainreport, "урезанный" прайм для партнерского апи<br/>
Пример использования:
```example: &place=miprime...```<br/><b>[..."&place=miprime"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_miprime.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L69)</b><br/><b>[..."&place=miprime"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_miprime.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L145)</b><br/><b>[..."&place=miprime"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_miprime.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L178)</b><br/>

---

#### Place: <b>[model_bids_recommender](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.cpp?rev=20450873c10bb360c6907a893e6bd65badbdb721#L588)</b>
Описание:
 https://st.yandex-team.ru/MARKETOUT-19727, 28287 Рекомендатор ставок на модель<br/>
Пример использования:
```example: &place=model_bids_recommender...```<br/><b>[..."&place=model_bids_recommender"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_model_bids_recommender.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L230)</b><br/><b>[..."&place=model_bids_recommender"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_model_bids_recommender.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L231)</b><br/><b>[..."&place=model_bids_recommender"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_model_bids_recommender.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L288)</b><br/>

---

#### Place: <b>[model_modifications](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.cpp?rev=20450873c10bb360c6907a893e6bd65badbdb721#L545)</b>
Описание:
 https://st.yandex-team.ru/MARKETOUT-11578 Модификации групповой модели<br/>
Пример использования:
```example: &place=model_modifications...```<br/><b>[..."&place=model_modifications"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_model_modifications.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L30)</b><br/><b>[..."&place=model_modifications"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_model_modifications.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L48)</b><br/><b>[..."&place=model_modifications"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_model_modifications.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L135)</b><br/>

---

#### Place: <b>[model_skus_info](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.cpp?rev=20450873c10bb360c6907a893e6bd65badbdb721#L616)</b>
Описание:
 https://st.yandex-team.ru/MARKETOUT-33867 Ручка для выдачи информации по sku для модели по model_id<br/>
Пример использования:
```example: &place=model_skus_info...```<br/><b>[..."&place=model_skus_info"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_model_skus_info.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L45)</b><br/><b>[..."&place=model_skus_info"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_model_skus_info.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L48)</b><br/><b>[..."&place=model_skus_info"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_model_skus_info.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L51)</b><br/>

---

#### Place: <b>[model_statistics](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.cpp?rev=20450873c10bb360c6907a893e6bd65badbdb721#L637)</b>
Описание:

Пример использования:
```example: &place=model_statistics...```<br/><b>[..."&place=model_statistics"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_model_statistics.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L66)</b><br/><b>[..."&place=model_statistics"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_model_statistics.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L87)</b><br/><b>[..."&place=model_statistics"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_model_statistics.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L108)</b><br/>

---

#### Place: <b>[model_stats](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.cpp?rev=20450873c10bb360c6907a893e6bd65badbdb721#L520)</b>
Описание:
 Выдает количество оферов и min/max/med цены по регионам<br/>
Пример использования:
```example: &place=model_stats...```<br/><b>[..."&place=model_stats"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_model_stats.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L39)</b><br/><b>[..."&place=model_stats"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_model_stats.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L74)</b><br/><b>[..."&place=model_stats"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_model_stats.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L114)</b><br/>

---

#### Place: <b>[model_wizard_by_id](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.cpp?rev=20450873c10bb360c6907a893e6bd65badbdb721#L566)</b>
Описание:
 https://st.yandex-team.ru/MARKETOUT-16523 Отдает модельный колдунщик по id модели<br/>
Пример использования:
```example: &place=model_wizard_by_id...```<br/><b>[..."&place=model_wizard_by_id"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_model_wizard_by_id.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L142)</b><br/><b>[..."&place=model_wizard_by_id"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_model_wizard_by_id.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L223)</b><br/><b>[..."&place=model_wizard_by_id"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_model_wizard_by_id.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L311)</b><br/>

---

#### Place: <b>[modelinfo](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.cpp?rev=20450873c10bb360c6907a893e6bd65badbdb721#L519)</b>
Описание:
 Информация о карточке модели<br/>
Пример использования:
```example: &place=modelinfo...```<br/><b>[..."&place=modelinfo"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_blue_psku.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L822)</b><br/><b>[..."&place=modelinfo"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_blue_psku.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L850)</b><br/><b>[..."&place=modelinfo"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_medical_flags.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L402)</b><br/>

---

#### Place: <b>[modelwizardoffers](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.cpp?rev=20450873c10bb360c6907a893e6bd65badbdb721#L510)</b>
Описание:
 Модельный колдунщик<br/>
Пример использования:
```example: &place=modelwizardoffers...```<br/><b>[..."&place=modelwizardoffers"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_wizards.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L6473)</b><br/><b>[..."&place=modelwizardoffers"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_wizards.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L6570)</b><br/>

---

#### Place: <b>[multi_category](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.cpp?rev=20450873c10bb360c6907a893e6bd65badbdb721#L559)</b>
Описание:
 https://st.yandex-team.ru/MARKETOUT-15092 мультикатегорийная выдача<br/>
Пример использования:
```example: &place=multi_category...```<br/><b>[..."&place=multi_category"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_multicategory.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L124)</b><br/><b>[..."&place=multi_category"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_multicategory.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L303)</b><br/><b>[..."&place=multi_category"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_multicategory.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L330)</b><br/>

---

#### Place: <b>[nids_info](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.cpp?rev=20450873c10bb360c6907a893e6bd65badbdb721#L586)</b>
Описание:
 https://st.yandex-team.ru/MARKETOUT-20751 Информация о навигационном дереве<br/>
Пример использования:
```example: &place=nids_info...```<br/><b>[..."&place=nids_info"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_min_quantity.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L423)</b><br/><b>[..."&place=nids_info"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_nids_info.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L707)</b><br/><b>[..."&place=nids_info"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_nids_info.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L742)</b><br/>

---

#### Place: <b>[offer_search](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.cpp?rev=20450873c10bb360c6907a893e6bd65badbdb721#L636)</b>
Описание:
 https://st.yandex-team.ru/MARKETOUT-46647 поиск конкретных офферов для QA нужд<br/>
Пример использования:
```example: &place=offer_search...```<br/><b>[..."&place=offer_search"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_offer_search_base.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L52)</b><br/><b>[..."&place=offer_search"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_offer_search_by_promo.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L37)</b><br/>

---

#### Place: <b>[offer_status](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.cpp?rev=20450873c10bb360c6907a893e6bd65badbdb721#L610)</b>
Описание:
 https://st.yandex-team.ru/MARKETOUT-31749 Ручка для получения информации о состоянии оффера<br/>
Пример использования:
```example: &place=offer_status...```<br/><b>[..."&place=offer_status"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_offer_status.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L44)</b><br/>

---

#### Place: <b>[offerinfo](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.cpp?rev=20450873c10bb360c6907a893e6bd65badbdb721#L527)</b>
Описание:
 Информация о конкретном оффере<br/>
Пример использования:
```example: &place=offerinfo...```<br/><b>[..."&place=offerinfo"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_blue_psku.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L684)</b><br/><b>[..."&place=offerinfo"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_blue_psku.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L700)</b><br/><b>[..."&place=offerinfo"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_blue_psku.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L722)</b><br/>

---

#### Place: <b>[offerinfo_with_hidden_offers](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.cpp?rev=20450873c10bb360c6907a893e6bd65badbdb721#L528)</b>
Описание:
 Отображает скрытые офферы<br/>
Пример использования:
```example: &place=offerinfo_with_hidden_offers...```<br/>

---

#### Place: <b>[omm_electro](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.cpp?rev=20450873c10bb360c6907a893e6bd65badbdb721#L576)</b>
Описание:
 https://st.yandex-team.ru/MARKETOUT-18866 Отдает модели, рекомендуемые OMM на электричке<br/>
Пример использования:
```example: &place=omm_electro...```<br/><b>[..."&place=omm_electro"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_test_place.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L161)</b><br/>

---

#### Place: <b>[omm_findings](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.cpp?rev=20450873c10bb360c6907a893e6bd65badbdb721#L580)</b>
Описание:
 https://st.yandex-team.ru/MARKETOUT-18988 Отдает модели, рекомендуемые OMM на электричке<br/>
Пример использования:
```example: &place=omm_findings...```<br/><b>[..."&place=omm_findings"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_omm.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L193)</b><br/><b>[..."&place=omm_findings"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_omm.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L196)</b><br/><b>[..."&place=omm_findings"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_omm.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L283)</b><br/>

---

#### Place: <b>[omm_item2item](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.cpp?rev=20450873c10bb360c6907a893e6bd65badbdb721#L572)</b>
Описание:
 https://st.yandex-team.ru/MARKETOUT-17799 Отдает модели, рекомендуемые OMM на КМ<br/>
Пример использования:
```example: &place=omm_item2item...```<br/>

---

#### Place: <b>[omm_market](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.cpp?rev=20450873c10bb360c6907a893e6bd65badbdb721#L581)</b>
Описание:
 https://st.yandex-team.ru/MARKETOUT-18941 единый плейс, для всех OMM рекомндаций<br/>
Пример использования:
```example: &place=omm_market...```<br/>

---

#### Place: <b>[omm_parallel](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.cpp?rev=20450873c10bb360c6907a893e6bd65badbdb721#L574)</b>
Описание:
 https://st.yandex-team.ru/MARKETOUT-17799 Отдает модели, рекомендуемые OMM на мобильной морде<br/>
Пример использования:
```example: &place=omm_parallel...```<br/><b>[..."&place=omm_parallel"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_omm.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L682)</b><br/><b>[..."&place=omm_parallel"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_omm.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L686)</b><br/><b>[..."&place=omm_parallel"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_dj_parallel.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L21)</b><br/>

---

#### Place: <b>[omm_toloka](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.cpp?rev=20450873c10bb360c6907a893e6bd65badbdb721#L589)</b>
Описание:
 https://st.yandex-team.ru/MARKETOUT-21595 Офферы ОММ для оффлайн-метрики в Толоке<br/>
Пример использования:
```example: &place=omm_toloka...```<br/><b>[..."&place=omm_toloka"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_dj_place.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L915)</b><br/><b>[..."&place=omm_toloka"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_dj_place.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L966)</b><br/><b>[..."&place=omm_toloka"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_dj_place.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L973)</b><br/>

---

#### Place: <b>[omm_vertical](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.cpp?rev=20450873c10bb360c6907a893e6bd65badbdb721#L579)</b>
Описание:
 https://st.yandex-team.ru/MARKETOUT-18987 Отдает модели, рекомендуемые OMM для вертикали на тачовой морде и в поисковом приложении<br/>
Пример использования:
```example: &place=omm_vertical...```<br/><b>[..."&place=omm_vertical"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_omm_parallel.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1136)</b><br/>

---

#### Place: <b>[outlets](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.cpp?rev=20450873c10bb360c6907a893e6bd65badbdb721#L497)</b>
Описание:
 Список точек продаж<br/>
Пример использования:
```example: &place=outlets...```<br/><b>[..."&place=outlets"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_fast_data_outlets_schedule.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L12)</b><br/><b>[..."&place=outlets"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_fast_data_outlets_schedule.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L140)</b><br/><b>[..."&place=outlets"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_fast_data_outlets_schedule.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L206)</b><br/>

---

#### Place: <b>[parallel](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.cpp?rev=20450873c10bb360c6907a893e6bd65badbdb721#L492)</b>
Описание:
 Параллельный поиск. Выдаёт колдунщики: моделей, категорий, контекстные, универсальный, параметрический<br/>
Пример использования:
```example: &place=parallel...```<br/><b>[..."&place=parallel"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_cpa_only_parallel.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L46)</b><br/><b>[..."&place=parallel"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_model_wizard.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L336)</b><br/><b>[..."&place=parallel"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_model_wizard.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L497)</b><br/>

---

#### Place: <b>[parallel_blue_stats](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.cpp?rev=20450873c10bb360c6907a893e6bd65badbdb721#L493)</b>
Описание:
 Параллельный поиск<br/>
Пример использования:
```example: &place=parallel_blue_stats...```<br/>

---

#### Place: <b>[parallel_data](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.cpp?rev=20450873c10bb360c6907a893e6bd65badbdb721#L494)</b>
Описание:
 Параллельный поиск<br/>
Пример использования:
```example: &place=parallel_data...```<br/><b>[..."&place=parallel_data"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_parallel_data.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L28)</b><br/><b>[..."&place=parallel_data"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_parallel_data.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L52)</b><br/><b>[..."&place=parallel_data"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_parallel_data.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L60)</b><br/>

---

#### Place: <b>[parallel_prime](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.cpp?rev=20450873c10bb360c6907a893e6bd65badbdb721#L495)</b>
Описание:
 Параллельный поиск<br/>
Пример использования:
```example: &place=parallel_prime...```<br/><b>[..."&place=parallel_prime"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_parallel_prime.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L125)</b><br/><b>[..."&place=parallel_prime"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_parallel_prime.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L133)</b><br/><b>[..."&place=parallel_prime"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_parallel_prime.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L152)</b><br/>

---

#### Place: <b>[parallel_products](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.cpp?rev=20450873c10bb360c6907a893e6bd65badbdb721#L634)</b>
Описание:
 ECOMQUALITY-243 Экспериментальный плейс ТВ<br/>
Пример использования:
```example: &place=parallel_products...```<br/><b>[..."&place=parallel_products"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_parallel_products.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L81)</b><br/><b>[..."&place=parallel_products"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_parallel_products.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L89)</b><br/><b>[..."&place=parallel_products"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_parallel_products.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L94)</b><br/>

---

#### Place: <b>[parallel_slider](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.cpp?rev=20450873c10bb360c6907a893e6bd65badbdb721#L496)</b>
Описание:
 Параллельный поиск<br/>
Пример использования:
```example: &place=parallel_slider...```<br/><b>[..."&place=parallel_slider"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_parallel_sliders.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L221)</b><br/><b>[..."&place=parallel_slider"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_parallel_sliders.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L268)</b><br/><b>[..."&place=parallel_slider"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_parallel_sliders.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L304)</b><br/>

---

#### Place: <b>[parse_wh_compressed](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.cpp?rev=20450873c10bb360c6907a893e6bd65badbdb721#L627)</b>
Описание:
 https://st.yandex-team.ru/MARKETOUT-45138 Извлечение данных из сжатой строки со складами<br/>
Пример использования:
```example: &place=parse_wh_compressed...```<br/><b>[..."&place=parse_wh_compressed"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_get_eats_warehouses.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L141)</b><br/><b>[..."&place=parse_wh_compressed"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_get_eats_warehouses.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L160)</b><br/><b>[..."&place=parse_wh_compressed"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_get_eats_warehouses.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L178)</b><br/>

---

#### Place: <b>[partner_model_offers](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.cpp?rev=20450873c10bb360c6907a893e6bd65badbdb721#L518)</b>
Описание:
 Партнерский интерфейс показывающий информацию об офферах для каждой модели<br/>
Пример использования:
```example: &place=partner_model_offers...```<br/><b>[..."&place=partner_model_offers"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_partner_model_offers.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L99)</b><br/><b>[..."&place=partner_model_offers"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_partner_model_offers.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L199)</b><br/><b>[..."&place=partner_model_offers"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_partner_model_offers.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L228)</b><br/>

---

#### Place: <b>[partner_offer_counts](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.cpp?rev=20450873c10bb360c6907a893e6bd65badbdb721#L517)</b>
Описание:
 Партнерский интерфейс по расчету офферов для каждой модели https://st.yandex-team.ru/MARKETOUT-9243<br/>
Пример использования:
```example: &place=partner_offer_counts...```<br/><b>[..."&place=partner_offer_counts"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_partner_offer_counts.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L60)</b><br/><b>[..."&place=partner_offer_counts"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_partner_offer_counts.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L70)</b><br/><b>[..."&place=partner_offer_counts"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_partner_offer_counts.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L81)</b><br/>

---

#### Place: <b>[personal_categories](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.cpp?rev=20450873c10bb360c6907a893e6bd65badbdb721#L526)</b>
Описание:
 Выдает топ персональных категорий пользователя<br/>
Пример использования:
```example: &place=personal_categories...```<br/><b>[..."&place=personal_categories"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_personal_categories.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L183)</b><br/><b>[..."&place=personal_categories"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_personal_categories.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L186)</b><br/><b>[..."&place=personal_categories"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_personal_categories.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L201)</b><br/>

---

#### Place: <b>[personal_offers](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.cpp?rev=20450873c10bb360c6907a893e6bd65badbdb721#L546)</b>
Описание:
 https://st.yandex-team.ru/MARKETOUT-11452 Офферы из персональных категорий<br/>
Пример использования:
```example: &place=personal_offers...```<br/><b>[..."&place=personal_offers"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_personal_offers.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L133)</b><br/><b>[..."&place=personal_offers"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_personal_offers.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L151)</b><br/><b>[..."&place=personal_offers"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_personal_offers.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L155)</b><br/>

---

#### Place: <b>[personal_recommendations](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.cpp?rev=20450873c10bb360c6907a893e6bd65badbdb721#L531)</b>
Описание:
 Выдает список персональных товаров<br/>
Пример использования:
```example: &place=personal_recommendations...```<br/><b>[..."&place=personal_recommendations"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_personal_recommendations.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L171)</b><br/><b>[..."&place=personal_recommendations"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_personal_recommendations.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L177)</b><br/><b>[..."&place=personal_recommendations"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_personal_recommendations.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L187)</b><br/>

---

#### Place: <b>[personalcategorymodels](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.cpp?rev=20450873c10bb360c6907a893e6bd65badbdb721#L522)</b>
Описание:
 Выдает модели и кластера из персональных категорий пользователя<br/>
Пример использования:
```example: &place=personalcategorymodels...```<br/><b>[..."&place=personalcategorymodel"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_paging.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L173)</b><br/><b>[..."&place=personalcategorymodels"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_paging.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L176)</b><br/><b>[..."&place=personalcategorymodels"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_personal_category_models.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L150)</b><br/>

---

#### Place: <b>[popular_glfilters](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.cpp?rev=20450873c10bb360c6907a893e6bd65badbdb721#L606)</b>
Описание:
 https://st.yandex-team.ru/MARKETOUT-31655: Плейс для статистик по популярным фильтрам<br/>
Пример использования:
```example: &place=popular_glfilters...```<br/><b>[..."&place=popular_glfilters"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_popular_glfilters.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L26)</b><br/><b>[..."&place=popular_glfilters"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_popular_glfilters.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L32)</b><br/><b>[..."&place=popular_glfilters"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_popular_glfilters.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L35)</b><br/>

---

#### Place: <b>[popular_products](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.cpp?rev=20450873c10bb360c6907a893e6bd65badbdb721#L523)</b>
Описание:
 Выдает рекомендаованные популярные товары для пользователя<br/>
Пример использования:
```example: &place=popular_products...```<br/><b>[..."&place=popular_products"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_models_with_offers.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L358)</b><br/><b>[..."&place=popular_products"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_paging.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L240)</b><br/><b>[..."&place=popular_products"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_paging.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L249)</b><br/>

---

#### Place: <b>[price_recommender](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.cpp?rev=20450873c10bb360c6907a893e6bd65badbdb721#L562)</b>
Описание:
 https://st.yandex-team.ru/MARKETOUT-16157 Place for price recommendations about number of shows<br/>
Пример использования:
```example: &place=price_recommender...```<br/><b>[..."&place=price_recommender"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_price_recommender.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L296)</b><br/>

---

#### Place: <b>[pricedrop_kit](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.cpp?rev=20450873c10bb360c6907a893e6bd65badbdb721#L557)</b>
Описание:
 https://st.yandex-team.ru/MARKETRECOM-3600 Ручка для блока комплектов к товару на карточке<br/>
Пример использования:
```example: &place=pricedrop_kit...```<br/><b>[..."&place=pricedrop_kit"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_pricedrop_kit.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L531)</b><br/><b>[..."&place=pricedrop_kit"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_pricedrop_kit.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L542)</b><br/><b>[..."&place=pricedrop_kit"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_pricedrop_kit.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L547)</b><br/>

---

#### Place: <b>[prime](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.cpp?rev=20450873c10bb360c6907a893e6bd65badbdb721#L508)</b>
Описание:
 Основной (обычный) поиск<br/>
Пример использования:
```example: &place=prime...```<br/><b>[..."&place=prime"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_bids_recommender_formulas.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L28)</b><br/><b>[..."&place=prime"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_blue_psku.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L127)</b><br/><b>[..."&place=prime"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_blue_psku.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L230)</b><br/>

---

#### Place: <b>[prime_filters](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.cpp?rev=20450873c10bb360c6907a893e6bd65badbdb721#L550)</b>
Описание:
 https://st.yandex-team.ru/MARKETOUT-13590 Отдельный запрос за фильтрами для прайма.<br/>
Пример использования:
```example: &place=prime_filters...```<br/>

---

#### Place: <b>[print_doc](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.cpp?rev=20450873c10bb360c6907a893e6bd65badbdb721#L560)</b>
Описание:
 https://st.yandex-team.ru/MARKETOUT-6386 Плейс который находит документ и выводит все его проперти<br/>
Пример использования:
```example: &place=print_doc...```<br/><b>[..."&place=print_doc"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_rty_delivery.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L36)</b><br/><b>[..."&place=print_doc"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_rty_sort_index.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L35)</b><br/><b>[..."&place=print_doc"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_snippet_return_500_on_error.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L28)</b><br/>

---

#### Place: <b>[product_accessories](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.cpp?rev=20450873c10bb360c6907a893e6bd65badbdb721#L534)</b>
Описание:
 Выдает список сопутствующих товаров для данной модели<br/>
Пример использования:
```example: &place=product_accessories...```<br/><b>[..."&place=product_accessories"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_exclude_entities_filter.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L59)</b><br/><b>[..."&place=product_accessories"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_models_with_offers.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L256)</b><br/><b>[..."&place=product_accessories_blu"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_product_accessories_blue.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L32)</b><br/>

---

#### Place: <b>[product_accessories_blue](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.cpp?rev=20450873c10bb360c6907a893e6bd65badbdb721#L535)</b>
Описание:
 Выдает список сопутствующих товаров для данной модели<br/>
Пример использования:
```example: &place=product_accessories_blue...```<br/><b>[..."&place=product_accessories_blu"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_product_accessories_blue.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L32)</b><br/><b>[..."&place=product_accessories_blue"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_dj.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1653)</b><br/><b>[..."&place=product_accessories_blue"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_blue_promo_generic_bundle_model_places.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L613)</b><br/>

---

#### Place: <b>[product_analogs](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.cpp?rev=20450873c10bb360c6907a893e6bd65badbdb721#L536)</b>
Описание:
 Выдает список аналогичных товаров для данной модели<br/>
Пример использования:
```example: &place=product_analogs...```<br/>

---

#### Place: <b>[productoffers](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.cpp?rev=20450873c10bb360c6907a893e6bd65badbdb721#L516)</b>
Описание:
 Выдает офферы для карточки модели<br/>
Пример использования:
```example: &place=productoffers...```<br/><b>[..."&place=productoffers"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_default_offer_experiments.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L47)</b><br/><b>[..."&place=productoffers"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_default_offer_experiments.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L53)</b><br/><b>[..."&place=productoffers"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_default_offer_experiments.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L103)</b><br/>

---

#### Place: <b>[products_by_history](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.cpp?rev=20450873c10bb360c6907a893e6bd65badbdb721#L529)</b>
Описание:
 Список моделей на основе просмотренных<br/>
Пример использования:
```example: &place=products_by_history...```<br/><b>[..."&place=products_by_history"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_exclude_entities_filter.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L174)</b><br/><b>[..."&place=products_by_history"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_models_of_interest.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L96)</b><br/><b>[..."&place=products_by_history"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_models_of_interest.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L105)</b><br/>

---

#### Place: <b>[products_by_history_ex](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.cpp?rev=20450873c10bb360c6907a893e6bd65badbdb721#L530)</b>
Описание:
 Список моделей на основе просмотренных, а если ничего не нашлось - популярные модели<br/>
Пример использования:
```example: &place=products_by_history_ex...```<br/><b>[..."&place=products_by_history_ex"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_products_by_history_ex.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L135)</b><br/><b>[..."&place=products_by_history_ex"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_products_by_history_ex.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L140)</b><br/><b>[..."&place=products_by_history_ex"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_products_by_history_ex.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L147)</b><br/>

---

#### Place: <b>[promo](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.cpp?rev=20450873c10bb360c6907a893e6bd65badbdb721#L540)</b>
Описание:
 https://st.yandex-team.ru/MARKETOUT-10347 Информация о промо-акции<br/>
Пример использования:
```example: &place=promo...```<br/><b>[..."&place=promo"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_disabled_promo.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L38)</b><br/><b>[..."&place=promo_top_categories"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_promo_top_categories.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L115)</b><br/><b>[..."&place=promo_top_categories"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_promo_top_categories.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L144)</b><br/>

---

#### Place: <b>[promo_cart_discount](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.cpp?rev=20450873c10bb360c6907a893e6bd65badbdb721#L556)</b>
Описание:
 https://st.yandex-team.ru/MARKETOUT-24793 Ручка для отдачи офферов для попапа в корзине (promo-type=cart-discount)<br/>
Пример использования:
```example: &place=promo_cart_discount...```<br/><b>[..."&place=promo_cart_discoun"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_promo_by_cart.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1476)</b><br/><b>[..."&place=promo_cart_discount"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_promo_by_cart.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1491)</b><br/><b>[..."&place=promo_cart_discount"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_promo_by_cart.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1522)</b><br/>

---

#### Place: <b>[promo_list](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.cpp?rev=20450873c10bb360c6907a893e6bd65badbdb721#L552)</b>
Описание:
 Плейс отдающий список подходящих промо<br/>
Пример использования:
```example: &place=promo_list...```<br/><b>[..."&place=promo_list"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_promo_check_min_price.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L286)</b><br/><b>[..."&place=promo_list"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_promo_check_min_price.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L298)</b><br/><b>[..."&place=promo_list"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_promo_check_min_price.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L311)</b><br/>

---

#### Place: <b>[promo_models](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.cpp?rev=20450873c10bb360c6907a893e6bd65badbdb721#L551)</b>
Описание:
 https://st.yandex-team.ru/MARKETOUT-14728 Плейс для страницы промо-моделей маркета<br/>
Пример использования:
```example: &place=promo_models...```<br/>

---

#### Place: <b>[promo_recipes](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.cpp?rev=20450873c10bb360c6907a893e6bd65badbdb721#L554)</b>
Описание:
 Плейс для промо-рецептов<br/>
Пример использования:
```example: &place=promo_recipes...```<br/><b>[..."&place=promo_recipes"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_promo_recipes.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L31)</b><br/><b>[..."&place=promo_recipes"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_promo_recipes.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L47)</b><br/><b>[..."&place=promo_recipes"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_promo_recipes.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L70)</b><br/>

---

#### Place: <b>[promo_top_categories](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.cpp?rev=20450873c10bb360c6907a893e6bd65badbdb721#L555)</b>
Описание:
 https://st.yandex-team.ru/MARKETOUT-24315 Плейс для популярных промо-категорий<br/>
Пример использования:
```example: &place=promo_top_categories...```<br/><b>[..."&place=promo_top_categories"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_promo_top_categories.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L115)</b><br/><b>[..."&place=promo_top_categories"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_promo_top_categories.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L144)</b><br/><b>[..."&place=promo_top_categories"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_promo_top_categories.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L173)</b><br/>

---

#### Place: <b>[promoted_categories](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.cpp?rev=20450873c10bb360c6907a893e6bd65badbdb721#L570)</b>
Описание:
 https://st.yandex-team.ru/MARKETOUT-17043 Отдает продвигаемые категории в зависимости от пола пользователя<br/>
Пример использования:
```example: &place=promoted_categories...```<br/><b>[..."&place=promoted_categories"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_recommendations.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1681)</b><br/><b>[..."&place=promoted_categories"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_recommendations.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1692)</b><br/><b>[..."&place=promoted_categories"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_recommendations.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1718)</b><br/>

---

#### Place: <b>[recipe_by_glfilters](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.cpp?rev=20450873c10bb360c6907a893e6bd65badbdb721#L511)</b>
Описание:
 Выдает рецепт в точности совпадающий по переданным фильтрам<br/>
Пример использования:
```example: &place=recipe_by_glfilters...```<br/><b>[..."&place=recipe_by_glfilters"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_recipes.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L230)</b><br/><b>[..."&place=recipe_by_glfilters"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_recipes.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L233)</b><br/><b>[..."&place=recipe_by_glfilters"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_recipes.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L286)</b><br/>

---

#### Place: <b>[recipes_by_doc](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.cpp?rev=20450873c10bb360c6907a893e6bd65badbdb721#L532)</b>
Описание:
 Выдает рецепты по id документа (пока только для моделей)<br/>
Пример использования:
```example: &place=recipes_by_doc...```<br/><b>[..."&place=recipes_by_doc"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_recipes.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L268)</b><br/><b>[..."&place=recipes_by_doc"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_recipes.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L946)</b><br/><b>[..."&place=recipes_by_doc"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_recipes.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L947)</b><br/>

---

#### Place: <b>[recipes_contain_glfilters](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.cpp?rev=20450873c10bb360c6907a893e6bd65badbdb721#L513)</b>
Описание:
 Выдает рецепты содержащие все переданные фильтры (в порядке убывания популярности)<br/>
Пример использования:
```example: &place=recipes_contain_glfilters...```<br/><b>[..."&place=recipes_contain_glfilters"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_recipes.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L239)</b><br/><b>[..."&place=recipes_contain_glfilters"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_recipes.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L246)</b><br/><b>[..."&place=recipes_contain_glfilters"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_recipes.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L253)</b><br/>

---

#### Place: <b>[recom_models](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.cpp?rev=20450873c10bb360c6907a893e6bd65badbdb721#L625)</b>
Описание:
 https://st.yandex-team.ru/MARKETRECOM-3713 фильтрация входящих моделей по наличию и обогащение<br/>
Пример использования:
```example: &place=recom_models...```<br/><b>[..."&place=recom_models"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_recom_models.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L45)</b><br/><b>[..."&place=recom_models"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_recom_models.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L87)</b><br/><b>[..."&place=recom_models"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_recom_models.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L124)</b><br/>

---

#### Place: <b>[recom_universal](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.cpp?rev=20450873c10bb360c6907a893e6bd65badbdb721#L624)</b>
Описание:
 https://st.yandex-team.ru/MARKETOUT-38182 Ручка для рекомендательных подборок<br/>
Пример использования:
```example: &place=recom_universal...```<br/><b>[..."&place=recom_universal"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_recom_universal.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L168)</b><br/><b>[..."&place=recom_universal"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_recom_universal.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L190)</b><br/><b>[..."&place=recom_universal"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_recom_universal.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L221)</b><br/>

---

#### Place: <b>[recommendations_meta](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.cpp?rev=20450873c10bb360c6907a893e6bd65badbdb721#L583)</b>
Описание:
 https://st.yandex-team.ru/MARKETOUT-18882 Запускает рекомендательные плейсы и удаляет дубли из их выдачи<br/>
Пример использования:
```example: &place=recommendations_meta...```<br/><b>[..."&place=recommendations_meta"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_recommendations_meta.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L110)</b><br/><b>[..."&place=recommendations_meta"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_recom_banned_categories.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L519)</b><br/>

---

#### Place: <b>[report_status](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.cpp?rev=20450873c10bb360c6907a893e6bd65badbdb721#L549)</b>
Описание:
 https://st.yandex-team.ru/MARKETOUT-13169 управление отключением репорта от балансеров<br/>
Пример использования:
```example: &place=report_status...```<br/><b>[..."&place=report_status"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_report_status.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L24)</b><br/><b>[..."&place=report_status"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_report_status.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L35)</b><br/><b>[..."&place=report_status"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_report_status.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L36)</b><br/>

---

#### Place: <b>[same_shop_incut](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.cpp?rev=20450873c10bb360c6907a893e6bd65badbdb721#L630)</b>
Описание:
 https://st.yandex-team.ru/MARKETOUT-38182MARKETOUT-41498 врезка "Приедет в том же заказе" на таче<br/>
Пример использования:
```example: &place=same_shop_incut...```<br/>

---

#### Place: <b>[shop_info](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.cpp?rev=20450873c10bb360c6907a893e6bd65badbdb721#L543)</b>
Описание:
 https://st.yandex-team.ru/MARKETOUT-11519 Информация о магазине<br/>
Пример использования:
```example: &place=shop_info...```<br/><b>[..."&place=shop_info"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_new_pickup.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L304)</b><br/><b>[..."&place=shop_info"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_shop_cpc_filter.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L32)</b><br/><b>[..."&place=shop_info)"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_shop_cpc_filter.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L35)</b><br/>

---

#### Place: <b>[shop_vendor_promo_clicks_stats](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.cpp?rev=20450873c10bb360c6907a893e6bd65badbdb721#L587)</b>
Описание:
 https://st.yandex-team.ru/MARKETOUT-20909 Рецепты-фильтры для СЕО-страниц<br/>
Пример использования:
```example: &place=shop_vendor_promo_clicks_stats...```<br/><b>[..."&place=shop_vendor_promo_clicks_stats"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_shop_vendor_promo_clicks_stats.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L40)</b><br/><b>[..."&place=shop_vendor_promo_clicks_stats"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_shop_vendor_promo_clicks_stats.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L72)</b><br/><b>[..."&place=shop_vendor_promo_clicks_stats"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_shop_vendor_promo_clicks_stats.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L94)</b><br/>

---

#### Place: <b>[shopmodels](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.cpp?rev=20450873c10bb360c6907a893e6bd65badbdb721#L584)</b>
Описание:
 Модельная выдача магазина<br/>
Пример использования:
```example: &place=shopmodels...```<br/><b>[..."&place=shopmodels"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_shop_models.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L133)</b><br/><b>[..."&place=shopmodels"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_shop_models.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L137)</b><br/><b>[..."&place=shopmodels"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_shop_models.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L141)</b><br/>

---

#### Place: <b>[shopoffers](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.cpp?rev=20450873c10bb360c6907a893e6bd65badbdb721#L500)</b>
Описание:
 Показывает оффера магазина<br/>
Пример использования:
```example: &place=shopoffers...```<br/><b>[..."&place=shopoffers"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_shopoffers.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L47)</b><br/><b>[..."&place=shopoffers"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_shopoffers.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L64)</b><br/><b>[..."&place=shopoffers"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_shopoffers.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L87)</b><br/>

---

#### Place: <b>[shops_list](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.cpp?rev=20450873c10bb360c6907a893e6bd65badbdb721#L600)</b>
Описание:
 https://st.yandex-team.ru/MARKETOUT-26657 Список магазинов на маркете (по первой букве названия)<br/>
Пример использования:
```example: &place=shops_list...```<br/><b>[..."&place=shops_list"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_shops_list.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L27)</b><br/><b>[..."&place=shops_list"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_shops_list.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L53)</b><br/><b>[..."&place=shops_list"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_shops_list.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L78)</b><br/>

---

#### Place: <b>[sku_offers](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.cpp?rev=20450873c10bb360c6907a893e6bd65badbdb721#L563)</b>
Описание:
 https://st.yandex-team.ru/MARKETOUT-15988 Данные для отображения карточки СКУ<br/>
Пример использования:
```example: &place=sku_offers...```<br/><b>[..."&place=sku_offers"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_alice.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L57)</b><br/><b>[..."&place=sku_offers"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_blue_psku.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L167)</b><br/><b>[..."&place=sku_offers"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_blue_psku.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L209)</b><br/>

---

#### Place: <b>[sku_search](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.cpp?rev=20450873c10bb360c6907a893e6bd65badbdb721#L564)</b>
Описание:
 https://st.yandex-team.ru/MARKETOUT-17956 Поиск карточки СКУ по тексту<br/>
Пример использования:
```example: &place=sku_search...```<br/><b>[..."&place=sku_search"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_used_goods.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L358)</b><br/><b>[..."&place=sku_search"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_sku_docs.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L107)</b><br/><b>[..."&place=sku_search"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_sku_docs.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L109)</b><br/>

---

#### Place: <b>[sponsored_products](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.cpp?rev=20450873c10bb360c6907a893e6bd65badbdb721#L601)</b>
Описание:
 https://st.yandex-team.ru/MARKETOUT-28025 Реклама на беру<br/>
Пример использования:
```example: &place=sponsored_products...```<br/><b>[..."&place=sponsored_product"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_sponsored_products.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L228)</b><br/><b>[..."&place=sponsored_products"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_sponsored_products.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L236)</b><br/><b>[..."&place=sponsored_products"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_sponsored_products.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L285)</b><br/>

---

#### Place: <b>[stat_numbers](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.cpp?rev=20450873c10bb360c6907a893e6bd65badbdb721#L594)</b>
Описание:
 https://st.yandex-team.ru/MARKETOUT-23720 подсчёт количественных статистик с заданными параметрами<br/>
Пример использования:
```example: &place=stat_numbers...```<br/><b>[..."&place=stat_numbers"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_pickup_modifiers.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L166)</b><br/><b>[..."&place=stat_numbers"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_pickup_modifiers.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L171)</b><br/><b>[..."&place=stat_numbers"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_blue_promo_blue_cashback.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2602)</b><br/>

---

#### Place: <b>[static_info](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.cpp?rev=20450873c10bb360c6907a893e6bd65badbdb721#L622)</b>
Описание:
 https://st.yandex-team.ru/MARKETOUT-36086 ручка для получения константной инфы (пока только набор размеров тамбнейлов)<br/>
Пример использования:
```example: &place=static_info...```<br/><b>[..."&place=static_info"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_static_info.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L12)</b><br/>

---

#### Place: <b>[supplier_high_prices](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.cpp?rev=20450873c10bb360c6907a893e6bd65badbdb721#L613)</b>
Описание:
 https://st.yandex-team.ru/MARKETOUT-33381 Ручка репорта для выдачи проблемных офферов поставщика для таба "Высокие цены"<br/>
Пример использования:
```example: &place=supplier_high_prices...```<br/><b>[..."&place=supplier_high_prices"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_supplier_high_prices.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L160)</b><br/><b>[..."&place=supplier_high_prices"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_supplier_high_prices.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L164)</b><br/><b>[..."&place=supplier_high_prices"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_supplier_high_prices.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L168)</b><br/>

---

#### Place: <b>[supplier_info](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.cpp?rev=20450873c10bb360c6907a893e6bd65badbdb721#L604)</b>
Описание:
 https://st.yandex-team.ru/MARKETOUT-30382 Ручка для отдачи информации о поставщиках маркетплейсов<br/>
Пример использования:
```example: &place=supplier_info...```<br/><b>[..."&place=supplier_info"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_place_supplier_info.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L21)</b><br/><b>[..."&place=supplier_info"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_place_supplier_info.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L38)</b><br/>

---

#### Place: <b>[top_categories](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.cpp?rev=20450873c10bb360c6907a893e6bd65badbdb721#L514)</b>
Описание:
 Показывает популярные категории бренда https://st.yandex-team.ru/MARKETOUT-8385<br/>
Пример использования:
```example: &place=top_categories...```<br/><b>[..."&place=top_categories"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_top_categories.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L112)</b><br/><b>[..."&place=top_categories"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_top_categories.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L134)</b><br/><b>[..."&place=top_categories"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_top_categories.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L145)</b><br/>

---

#### Place: <b>[turbo](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.cpp?rev=20450873c10bb360c6907a893e6bd65badbdb721#L592)</b>
Описание:
 https://st.yandex-team.ru/MARKETOUT-21703 Ручка для турбо страниц<br/>
Пример использования:
```example: &place=turbo...```<br/><b>[..."&place=turbo"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_turbo_place_sku.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L155)</b><br/><b>[..."&place=turbo"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_turbo_place_sku.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L259)</b><br/><b>[..."&place=turbo"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_turbo_place_sku.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L267)</b><br/>

---

#### Place: <b>[user_feed](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.cpp?rev=20450873c10bb360c6907a893e6bd65badbdb721#L539)</b>
Описание:
 Лента персональных офферов для пользователя<br/>
Пример использования:
```example: &place=user_feed...```<br/><b>[..."&place=user_feed"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_user_feed.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L62)</b><br/><b>[..."&place=user_feed"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_user_feed.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L71)</b><br/><b>[..."&place=user_feed"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_user_feed.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L79)</b><br/>

---

#### Place: <b>[vendor_incut](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.cpp?rev=20450873c10bb360c6907a893e6bd65badbdb721#L609)</b>
Описание:
 https://st.yandex-team.ru/MARKETOUT-31649 Вендорская врезка<br/>
Пример использования:
```example: &place=vendor_incut...```<br/><b>[..."&place=vendor_incut"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_soft_cpa_only.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L614)</b><br/><b>[..."&place=vendor_incut"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_vendor_reserve_prices.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L116)</b><br/><b>[..."&place=vendor_incut"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_vendor_reserve_prices.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L157)</b><br/>

---

#### Place: <b>[vendor_offers_models](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.cpp?rev=20450873c10bb360c6907a893e6bd65badbdb721#L515)</b>
Описание:
 Показывает популярные товары бренда https://st.yandex-team.ru/MARKETOUT-8383<br/>
Пример использования:
```example: &place=vendor_offers_models...```<br/><b>[..."&place=vendor_offers_models"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_vendor_offers_models.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L234)</b><br/><b>[..."&place=vendor_offers_models"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_vendor_offers_models.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L266)</b><br/><b>[..."&place=vendor_offers_models"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_vendor_offers_models.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L280)</b><br/>

---

#### Place: <b>[virtual_cards_info](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.cpp?rev=20450873c10bb360c6907a893e6bd65badbdb721#L633)</b>
Описание:
 https://st.yandex-team.ru/MARKETOUT-45049 плейс для сервиса content-storage для получения инфы по виртуальным карточкам<br/>
Пример использования:
```example: &place=virtual_cards_info...```<br/><b>[..."&place=virtual_cards_info"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_virtual_cards_info.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L122)</b><br/><b>[..."&place=virtual_cards_info"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_virtual_cards_info.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L178)</b><br/><b>[..."&place=virtual_cards_info"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_virtual_cards_info.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L299)</b><br/>

---

#### Place: <b>[visual_search](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.cpp?rev=20450873c10bb360c6907a893e6bd65badbdb721#L635)</b>
Описание:
 https://st.yandex-team.ru/MSI-1000 визуальный поиск<br/>
Пример использования:
```example: &place=visual_search...```<br/><b>[..."&place=visual_searc"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_visual_search.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L71)</b><br/><b>[..."&place=visual_search"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_visual_search.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L149)</b><br/><b>[..."&place=visual_search"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_visual_search.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L152)</b><br/>

---

#### Place: <b>[visualanalog](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.cpp?rev=20450873c10bb360c6907a893e6bd65badbdb721#L501)</b>
Описание:
 Предположительно по картинке кластера находит похожие кластеры<br/>
Пример использования:
```example: &place=visualanalog...```<br/><b>[..."&place=visualanalog"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_visualanalog.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L85)</b><br/><b>[..."&place=visualanalog"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_visualanalog.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L105)</b><br/><b>[..."&place=visualanalog"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_visualanalog.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L120)</b><br/>

---


<br>

## Section 2 Cgi
<br>

#### Cgi: <b>[<b>[analytics-debug-only](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L375)</b>](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L376)</b>
Описание:
https://st.yandex-team.ru/MARKETOUT-29764<br/><b>Возвращаемое значение</b>: value of &debug=... CGI-parameter<br/><b>Заметка</b>: выдает много отладочной информации<br/>
Пример использования:
```example: &<b>[analytics-debug-only](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L375)</b>=[SOME_VALUE]...```<br/>

---

#### Cgi: <b>[[service]-history](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1208)</b>
Описание:
 Return saved requests to an external service<br/>https://st.yandex-team.ru/MARKETOUT-9044<br/><b>Возвращаемое значение</b>: CGI-value &[service]-history=, e. g. &reqwizard-history=<br/>
Пример использования:
```example: &[service]-history=[SOME_VALUE]...```<br/>

---

#### Cgi: <b>[](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2941)</b>
Описание:

Пример использования:


---

#### Cgi: <b>[](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2943)</b>
Описание:

Пример использования:


---

#### Cgi: <b>[](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2945)</b>
Описание:

Пример использования:


---

#### Cgi: <b>[](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L472)</b>
Описание:
 Check that page > 1 && platform == app<br/><b>Возвращаемое значение</b> boolean<br/>
Пример использования:


---

#### Cgi: <b>[](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L932)</b>
Описание:

Пример использования:


---

#### Cgi: <b>[actualize_outlets](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L296)</b>
Описание:
<b>Возвращаемое значение</b>: value of &actualize_outlets=<br/>https://st.yandex-team.ru/MARKETOUT-42440<br/>
Пример использования:
```example: &actualize_outlets=[SOME_VALUE]...```<br/><b>[..."actualize_outlets="...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_actual_delivery_grouped_outlets.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L701)</b><br><b>[..."actualize_outlets="...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_actual_delivery_grouped_outlets.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L948)</b><br><b>[..."actualize_outlets="...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_actual_delivery_grouped_outlets.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L996)</b><br>

---

#### Cgi: <b>[ad-work-mode](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2807)</b>
Описание:
https://wiki.yandex-team.ru/users/vladankor/actualdelivery/<br/><b>Возвращаемое значение</b>: value of CGI parameter &ad-work-mode<br/>
Пример использования:
```example: &ad-work-mode=[SOME_VALUE]...```<br/><b>[..."ad-work-mode="...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_actual_delivery_work_mode.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L577)</b><br><b>[..."ad-work-mode="...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_actual_delivery_work_mode.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L585)</b><br><b>[..."ad-work-mode="...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_actual_delivery_work_mode.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L595)</b><br>

---

#### Cgi: <b>[add-more-hyperids](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1946)</b>
Описание:
<b>Возвращаемое значение</b>: value of CGI parameter &add-more-hyperids<br/>https://st.yandex-team.ru/MARKETOUT-19594<br/>
Пример использования:
```example: &add-more-hyperids=[SOME_VALUE]...```<br/><b>[..."add-more-hyperids=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_omm_parallel.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1191)</b><br>

---

#### Cgi: <b>[add-offerinfo-jump-and-size-table](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2939)</b>
Описание:
<b>Возвращаемое значение</b>: Fill offer filters with Jump Table params, and addd sizes table to offers<br/>https://st.yandex-team.ru/MARKETOUT-46774<br/>
Пример использования:
```example: &add-offerinfo-jump-and-size-table=[SOME_VALUE]...```<br/><b>[..."add-offerinfo-jump-and-size-table=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_table_of_sizes.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1670)</b><br>

---

#### Cgi: <b>[add-original-ratio-thumbs](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2279)</b>
Описание:
<b>Возвращаемое значение</b>: value of CGI-parameter &add-original-ratio-thumbs<br/>https://st.yandex-team.ru/MARKETOUT-30942<br/>
Пример использования:
```example: &add-original-ratio-thumbs=[SOME_VALUE]...```<br/><b>[..."add-original-ratio-thumbs=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_picture_thumbnails.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L436)</b><br><b>[..."add-original-ratio-thumbs=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_picture_thumbnails.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L437)</b><br><b>[..."add-original-ratio-thumbs=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_picture_thumbnails.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L442)</b><br>

---

#### Cgi: <b>[add-sku-stats](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2617)</b>
Описание:
<b>Возвращаемое значение</b>: value of CGI-parameter &add-sku-stats<br/>
Пример использования:
```example: &add-sku-stats=[SOME_VALUE]...```<br/><b>[..."add-sku-stats=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_jumptable_with_modifications.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L266)</b><br><b>[..."add-sku-stats=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_nailed_documents_white_list.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L135)</b><br><b>[..."add-sku-stats=0"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_productoffers_filters.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2422)</b><br>

---

#### Cgi: <b>[add-vendor-color](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2626)</b>
Описание:
<b>Возвращаемое значение</b>: value of CGI-parameter &add-vendor-color<br/>
Пример использования:
```example: &add-vendor-color=[SOME_VALUE]...```<br/><b>[..."add-vendor-color=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_filters_lists.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L736)</b><br><b>[..."add-vendor-color=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_filters_lists.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L792)</b><br><b>[..."add-vendor-color=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_sku_white_prime.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L316)</b><br>

---

#### Cgi: <b>[additional_entities](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1202)</b>
Описание:
 Show additional entities in SERP.<br/> For example collections or articles<br/>
Пример использования:
```example: &additional_entities=[SOME_VALUE]...```<br/><b>[..."additional_entities=articles"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_ugc.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L349)</b><br><b>[..."additional_entities=articles"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_ugc.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L377)</b><br><b>[..."additional_entities=articles"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_ugc.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L378)</b><br>

---

#### Cgi: <b>[address](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2670)</b>
Описание:
 Presets of user address<br/> - place=actual_delivery<br/> Used to check delivery available in favourite user addresses<br/>https://st.yandex-team.ru/MARKETOUT-36864<br/><b>Возвращаемое значение</b>: value of CGI parameter "&address"<br/>
Пример использования:
```example: &address=[SOME_VALUE]...```<br/><b>[..."address="...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_actual_delivery_presets.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L785)</b><br>

---

#### Cgi: <b>[adult](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L542)</b>
Описание:
 Indicates forced adult queries<br/><b>Возвращаемое значение</b>: value of CGI-parameter &adult<br/>
Пример использования:
```example: &adult=[SOME_VALUE]...```<br/><b>[..."adult=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_partner_model_offers.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L99)</b><br><b>[..."adult=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_partner_model_offers.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L440)</b><br><b>[..."adult=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_partner_model_offers.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L445)</b><br>

---

#### Cgi: <b>[ag0](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2674)</b>
Описание:
<b>Возвращаемое значение</b>: value of CGI-parameter &ag0 request grouping parameter<br/>
Пример использования:
```example: &ag0=[SOME_VALUE]...```<br/><b>[..."ag0=previous_market"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_reask_gallery_wizard.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L445)</b><br><b>[..."ag0=market"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_reask_gallery_wizard.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L478)</b><br>

---

#### Cgi: <b>[alice-native](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1695)</b>
Описание:
 Used for marker a native scenario activation in alice bot<br/>
Пример использования:
```example: &alice-native=[SOME_VALUE]...```<br/>

---

#### Cgi: <b>[alice](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1691)</b>
Описание:
 Used for marker scenario in alice bot<br/>
Пример использования:
```example: &alice=[SOME_VALUE]...```<br/><b>[..."alice=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_blue_psku.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L424)</b><br><b>[..."alice=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_blue_psku.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L434)</b><br><b>[..."alice=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_adult.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L294)</b><br>

---

#### Cgi: <b>[all-gl-mbo-params](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1558)</b>
Описание:
https://st.yandex-team.ru/MARKETOUT-14241<br/> выводить все параметры модели одним списком<br/>
Пример использования:
```example: &all-gl-mbo-params=[SOME_VALUE]...```<br/><b>[..."all-gl-mbo-params=true"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_modelinfo.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L344)</b><br><b>[..."all-gl-mbo-params=true"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_modelinfo.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L396)</b><br>

---

#### Cgi: <b>[allow-collapsing](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1249)</b>
Описание:
 Explicitly enable collapsing<br/>https://st.yandex-team.ru/MARKETOUT-10776 and https://st.yandex-team.ru/MARKETVERSTKA-20374<br/><b>Возвращаемое значение</b>: value of CGI-parmeter "&allow-collapsing"<br/> Если выставлен, то офферы/ску на выдаче будут превращаться (схлопываться) в соотв. модели<br/>
Пример использования:
```example: &allow-collapsing=[SOME_VALUE]...```<br/><b>[..."allow-collapsing=0"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_boost_express_offers.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L344)</b><br><b>[..."allow-collapsing=0"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_boost_express_offers.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L448)</b><br><b>[..."allow-collapsing=0"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_boost_express_offers.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L485)</b><br>

---

#### Cgi: <b>[allow-disabled-lms-relations](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1973)</b>
Описание:
<b>Возвращаемое значение</b>: value of CGI-parameter &allow-disabled-lms-relations<br/>https://st.yandex-team.ru/MARKETOUT-23807<br/>
Пример использования:
```example: &allow-disabled-lms-relations=[SOME_VALUE]...```<br/><b>[..."allow-disabled-lms-relations=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_lms.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2187)</b><br><b>[..."allow-disabled-lms-relations=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_lms.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2188)</b><br><b>[..."allow-disabled-lms-relations=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_lms.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2189)</b><br>

---

#### Cgi: <b>[allow-filters-without-hid](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2635)</b>
Описание:
<b>Возвращаемое значение</b>: value of CGI-parameter &allow-filters-without-hid<br/>
Пример использования:
```example: &allow-filters-without-hid=[SOME_VALUE]...```<br/><b>[..."allow-filters-without-hid=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_sku_white_prime.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L353)</b><br><b>[..."allow-filters-without-hid=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_sku_white_prime.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L362)</b><br>

---

#### Cgi: <b>[allow-incomplete-offers](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1678)</b>
Описание:
<b>Возвращаемое значение</b>: &allow-incomplete-offers<br/> Is used for place=actual_delivery.<br/>
Пример использования:
```example: &allow-incomplete-offers=[SOME_VALUE]...```<br/><b>[..."allow-incomplete-offers=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_actual_delivery.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2533)</b><br><b>[..."allow-incomplete-offers=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_actual_delivery.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2565)</b><br><b>[..."allow-incomplete-offers=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_actual_delivery.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2570)</b><br>

---

#### Cgi: <b>[allow-strategies-list](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2269)</b>
Описание:
<b>Возвращаемое значение</b>: value of CGI-parameter &allow-strategies-list<br/>https://st.yandex-team.ru/MARKETOUT-36052<br/>
Пример использования:
```example: &allow-strategies-list=[SOME_VALUE]...```<br/><b>[..."allow-strategies-list="...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_combine_with_supplier_replace.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L678)</b><br><b>[..."allow-strategies-list="...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_combine_with_supplier_replace.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L791)</b><br><b>[..."allow-strategies-list="...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_combine_with_supplier_replace.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L856)</b><br>

---

#### Cgi: <b>[allow-ungrouping](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2631)</b>
Описание:
<b>Возвращаемое значение</b>: value of CGI-parameter &allow-ungrouping<br/><b>Заметка</b>: if set to 1, allow report to ungroup models into several items with different UngroupedModelKeyBlue<br/>
Пример использования:
```example: &allow-ungrouping=[SOME_VALUE]...```<br/><b>[..."allow-ungrouping=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_prime_jump_table.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L244)</b><br><b>[..."allow-ungrouping=0"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_through_filters.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L218)</b><br><b>[..."allow-ungrouping=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_optimize_do_search.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L123)</b><br>

---

#### Cgi: <b>[allowed-promos](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1271)</b>
Описание:
 A list of allowed promo identifiers<br/>https://st.yandex-team.ru/MARKETOUT-26364<br/><b>Возвращаемое значение</b>: value of CGI parameter "&allowed-promos"<br/>
Пример использования:
```example: &allowed-promos=[SOME_VALUE]...```<br/><b>[..."allowed-promos="...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_multipromo_priority.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L316)</b><br><b>[..."allowed-promos="...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_promo_self_intersection.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L78)</b><br><b>[..."allowed-promos="...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_promo_self_intersection.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L79)</b><br>

---

#### Cgi: <b>[also-viewed-short-format-with-sku](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2021)</b>
Описание:
<b>Возвращаемое значение</b>: value of CGI-parameter &also-viewed-short-format-with-sku<br/> use short format with sku and additional info on also_viewed place<br/>https://st.yandex-team.ru/MARKETRECOM-4997<br/>
Пример использования:
```example: &also-viewed-short-format-with-sku=[SOME_VALUE]...```<br/><b>[..."also-viewed-short-format-with-sku=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_also_viewed.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L420)</b><br>

---

#### Cgi: <b>[also-viewed-short-format](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2015)</b>
Описание:
<b>Возвращаемое значение</b>: value of CGI-parameter &also-viewed-short-format<br/> use short format on also_viewed place<br/>https://st.yandex-team.ru/MARKETOUT-22338<br/>
Пример использования:
```example: &also-viewed-short-format=[SOME_VALUE]...```<br/><b>[..."also-viewed-short-format=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_also_viewed_blue.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L207)</b><br><b>[..."also-viewed-short-format=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_also_viewed.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L376)</b><br><b>[..."also-viewed-short-format=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_also_viewed.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L384)</b><br>

---

#### Cgi: <b>[analog-filter](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L802)</b>
Описание:
 Degree of crude picture filtration for place=visualanalog.<br/> Can be:<br/> * 0 -- filtration is totally disabled<br/> * 1 -- weak filtration, slow search speed<br/> * 2 -- medium filtration, normal search speed<br/> * 3 -- strong filtration, high search speed<br/><b>Возвращаемое значение</b>: value of CGI-parameter analog-filter<br/>
Пример использования:
```example: &analog-filter=[SOME_VALUE]...```<br/><b>[..."analog-filter=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_visualanalog.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L85)</b><br><b>[..."analog-filter=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_visualanalog.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L105)</b><br><b>[..."analog-filter=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_visualanalog.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L120)</b><br>

---

#### Cgi: <b>[analog](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L124)</b>
Описание:
 Models IDs for microcard<br/> Add information about specific model on microcard place<br/>
Пример использования:
```example: &analog=[SOME_VALUE]...```<br/>

---

#### Cgi: <b>[anaplan-promo-id](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2200)</b>
Описание:
<b>Возвращаемое значение</b>: value of CGI-parameter &anaplan-promo-id<br/>https://st.yandex-team.ru/MARKETOUT-32809<br/>
Пример использования:
```example: &anaplan-promo-id=[SOME_VALUE]...```<br/><b>[..."anaplan-promo-id="...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_blue_promo_filters.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L976)</b><br>

---

#### Cgi: <b>[api](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1348)</b>
Описание:
 API source, e.g. partner<br/><b>Возвращаемое значение</b>: value of CGI parameter "&api"<br/>
Пример использования:
```example: &api=[SOME_VALUE]...```<br/><b>[..."api=content"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_hide_cpc_links.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L137)</b><br><b>[..."api=content"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_hide_cpc_links.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L145)</b><br><b>[..."api=content"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_ugc.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L692)</b><br>

---

#### Cgi: <b>[api_offerid_to_rate](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L807)</b>
Описание:
 Offer identifier to calculate cp on<br/><b>Возвращаемое значение</b>: value of CGI-parameter &api_offerid_to_rate<br/>
Пример использования:
```example: &api_offerid_to_rate=[SOME_VALUE]...```<br/><b>[..."api_offerid_to_rate=FRNxd7-S67VQQyexo4gQqA"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_apiofferauction.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L24)</b><br><b>[..."api_offerid_to_rate=FRNxd7-S67VQQyexo4gQqA"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_apiofferauction.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L42)</b><br><b>[..."api_offerid_to_rate=VZJptjZEjnC7k00uGbFa-A"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_show_log.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1273)</b><br>

---

#### Cgi: <b>[api_shopid_to_rate](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L812)</b>
Описание:
 Shop indentifier for the offer &api_offerid_to_rate<br/><b>Возвращаемое значение</b>: value of CGI-parameter &api_shopid_to_rate<br/>
Пример использования:
```example: &api_shopid_to_rate=[SOME_VALUE]...```<br/><b>[..."api_shopid_to_rate=200"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_apiofferauction.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L24)</b><br><b>[..."api_shopid_to_rate=200"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_apiofferauction.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L42)</b><br><b>[..."api_shopid_to_rate=3"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_show_log.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1273)</b><br>

---

#### Cgi: <b>[appmetrica-deviceid](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2993)</b>
Описание:
<b>Возвращаемое значение</b>: X-AppMetrica-DeviceId<br/>https://st.yandex-team.ru/MARKETOUT-46961<br/>
Пример использования:
```example: &appmetrica-deviceid=[SOME_VALUE]...```<br/>

---

#### Cgi: <b>[askreqwizard](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L729)</b>
Описание:
 Allow to rewrite config flag ReqWizardRequestsEnabled<br/><b>Возвращаемое значение</b>: true to force to ask reqwizard, if no reqwizard data has passed through CGI<br/><b>Заметка</b>: parses CGI-parameter &askreqwizard<br/> @default: returns false<br/>
Пример использования:
```example: &askreqwizard=[SOME_VALUE]...```<br/><b>[..."askreqwizard=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_wizards.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2296)</b><br><b>[..."askreqwizard=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_wizards.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2363)</b><br><b>[..."askreqwizard=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_wizards.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L8675)</b><br>

---

#### Cgi: <b>[assert-begemot-works](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2027)</b>
Описание:
<b>Возвращаемое значение</b>: value of CGI-parameter &assert-begemot-works<br/><b>Заметка</b>: bool, default false<br/>https://st.yandex-team.ru/MARKETOUT-25991<br/>
Пример использования:
```example: &assert-begemot-works=[SOME_VALUE]...```<br/><b>[..."assert-begemot-works=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_reqwizard.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L219)</b><br><b>[..."assert-begemot-works=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_reqwizard.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L222)</b><br><b>[..."assert-begemot-works=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_reqwizard.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L256)</b><br>

---

#### Cgi: <b>[at-beru-warehouse](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L202)</b>
Описание:

Пример использования:
```example: &at-beru-warehouse=[SOME_VALUE]...```<br/><b>[..."at-beru-warehouse=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_buybox_by_supplier_on_white.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L530)</b><br><b>[..."at-beru-warehouse="...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_blue_market.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2229)</b><br><b>[..."at-beru-warehouse="...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_blue_market.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2230)</b><br>

---

#### Cgi: <b>[available-for-business](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2851)</b>
Описание:
 This parameter means B2B marketplace context when it's enabled and disables<br/> promos, express delivery and some filters<br/> Also it enables offer filtering by search literal "is_b2b"<br/><b>Возвращаемое значение</b>: cgi: "available-for-business"<br/>https://st.yandex-team.ru/MARKETOUT-44462<br/>
Пример использования:
```example: &available-for-business=[SOME_VALUE]...```<br/><b>[..."available-for-business=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_market_b2b_b2c_filtering.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L67)</b><br><b>[..."available-for-business=0"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_market_b2b_b2c_filtering.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L81)</b><br><b>[..."available-for-business=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_redirects.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L724)</b><br>

---

#### Cgi: <b>[ban-mode](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2071)</b>
Описание:
<b>Возвращаемое значение</b>: value of CGI-parameter &ban-mode<br/>https://st.yandex-team.ru/MARKETOUT-26033<br/>
Пример использования:
```example: &ban-mode=[SOME_VALUE]...```<br/><b>[..."ban-mode="...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_recom_soft_ban.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L118)</b><br><b>[..."ban-mode=foo"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_recom_soft_ban.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L206)</b><br>

---

#### Cgi: <b>[bank](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1324)</b>
Описание:
 Bank to use for currency converting (bank)<br/>https://st.yandex-team.ru/MARKETOUT-11532<br/><b>Возвращаемое значение</b>: value of CGI parameter "&bank"<br/>
Пример использования:
```example: &bank=[SOME_VALUE]...```<br/><b>[..."bank=BANK-KZT"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_currency_convert.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L225)</b><br>

---

#### Cgi: <b>[baobab_event_id](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L622)</b>
Описание:
<b>Возвращаемое значение</b>: value of &baobab_event_id=... CGI-parameter<br/>
Пример использования:
```example: &baobab_event_id=[SOME_VALUE]...```<br/><b>[..."baobab_event_id=kuiggrsq9q"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_click_log.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1546)</b><br><b>[..."baobab_event_id=kuiggrsq9q"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_show_log.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1737)</b><br>

---

#### Cgi: <b>[base](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1015)</b>
Описание:
 used in making urls to outlets, calls, etc<br/><b>Возвращаемое значение</b>: value of CGI-parameter &base<br/>
Пример использования:
```example: &base=[SOME_VALUE]...```<br/><b>[..."base=default.market-exp-prestable.yandex.ru"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_shop_info.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1371)</b><br><b>[..."base=default.market-exp-prestable.yandex.ru"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_shop_info.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1403)</b><br><b>[..."base=default.market-exp-prestable.yandex.ru"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_shop_info.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1430)</b><br>

---

#### Cgi: <b>[batch-bids-recommendations](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L918)</b>
Описание:
 Use Batch Bids Recommender<br/>https://st.yandex-team.ru/MARKETOUT-28173<br/><b>Возвращаемое значение</b>: the value of CGI-parameter &batch-bids-recommendations<br/>
Пример использования:
```example: &batch-bids-recommendations=[SOME_VALUE]...```<br/><b>[..."batch-bids-recommendations=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_bids_recommender_cpa_uncollapse.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L293)</b><br><b>[..."batch-bids-recommendations=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_bids_recommender_cpa_uncollapse.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L363)</b><br><b>[..."batch-bids-recommendations=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_bids_recommender_sku.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L88)</b><br>

---

#### Cgi: <b>[batch-bids-text](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L924)</b>
Описание:
 Text values for Batch Bids Recommender<br/>https://st.yandex-team.ru/MARKETOUT-28173<br/><b>Возвращаемое значение</b>: the value of CGI-parameter &batch-bids-text<br/>
Пример использования:
```example: &batch-bids-text=[SOME_VALUE]...```<br/><b>[..."batch-bids-text=search"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_bids_recommender.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1542)</b><br><b>[..."batch-bids-text=auction"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_bids_recommender.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1597)</b><br><b>[..."batch-bids-text=cpa"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_bids_recommender.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1603)</b><br>

---

#### Cgi: <b>[beru-order-params](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2415)</b>
Описание:
 Common client specific params for beruOrder url<br/><b>Возвращаемое значение</b>: value of CGI parameter "&beru-order-params"<br/>
Пример использования:
```example: &beru-order-params=[SOME_VALUE]...```<br/><b>[..."beru-order-params=purchase-referrer%3Dberu_in_yamarket%26clid%3D123%26vid%3D456"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_beru_order.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L123)</b><br>

---

#### Cgi: <b>[bid](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1462)</b>
Описание:
 Parameter passed to bids recommender or predictor to have recommendations by specifing bid<br/>
Пример использования:
```example: &bid=[SOME_VALUE]...```<br/>

---

#### Cgi: <b>[bigb_response_market_parallel_b64](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2527)</b>
Описание:

Пример использования:
```example: &bigb_response_market_parallel_b64=[SOME_VALUE]...```<br/><b>[..."bigb_response_market_parallel_b64="...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_wizards_cpa_incut.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2145)</b><br>

---

#### Cgi: <b>[bk-ads](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1053)</b>
Описание:
 Indicates that report should return block bkAds<br/><b>Возвращаемое значение</b>: CGI-value &bk-ads, false if not set<br/>
Пример использования:
```example: &bk-ads=[SOME_VALUE]...```<br/><b>[..."bk-ads=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_bk.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L133)</b><br><b>[..."bk-ads=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_bk.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L141)</b><br><b>[..."bk-ads=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_bk.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L145)</b><br>

---

#### Cgi: <b>[blender](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2709)</b>
Описание:
https://st.yandex-team.ru/MARKETOUT-37950<br/>
Пример использования:
```example: &blender=[SOME_VALUE]...```<br/><b>[..."blender=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_access_log.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L263)</b><br><b>[..."blender=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_incuts_from_serp.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L118)</b><br><b>[..."blender="...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_blender.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L755)</b><br>

---

#### Cgi: <b>[bonus_id](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1277)</b>
Описание:
 A list of requested Beru bonus identifiers<br/>https://st.yandex-team.ru/MARKETOUT-29129<br/><b>Возвращаемое значение</b>: value of CGI parameter "&bonus_id"<br/>
Пример использования:
```example: &bonus_id=[SOME_VALUE]...```<br/><b>[..."bonus_id="...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_beru_bonus_prime.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L263)</b><br>

---

#### Cgi: <b>[book-now-incut-page](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L968)</b>
Описание:
 Set book-now-incut page<br/><b>Возвращаемое значение</b>: CGI-value &book-now-incut-page<br/>
Пример использования:
```example: &book-now-incut-page=[SOME_VALUE]...```<br/><b>[..."book-now-incut-page=2"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_book_now_ctr.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L59)</b><br><b>[..."book-now-incut-page=2000"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_book_now.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L766)</b><br><b>[..."book-now-incut-page=2000"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_book_now.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L822)</b><br>

---

#### Cgi: <b>[book-now-outlet-id](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L973)</b>
Описание:
 Filter offers by booking avalaibility in specified outlet<br/><b>Возвращаемое значение</b>: CGI-value &book-now-outlet-id<br/>
Пример использования:
```example: &book-now-outlet-id=[SOME_VALUE]...```<br/><b>[..."book-now-outlet-id=201"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_book_now.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1879)</b><br><b>[..."book-now-outlet-id=202"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_book_now.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1912)</b><br><b>[..."book-now-outlet-id=201"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_book_now.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2303)</b><br>

---

#### Cgi: <b>[boost-discount-abs-from](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2694)</b>
Описание:
<b>Возвращаемое значение</b>: CGI discount params for boosting recommender<br/>https://st.yandex-team.ru/MARKETRECOM-3458<br/>
Пример использования:
```example: &boost-discount-abs-from=[SOME_VALUE]...```<br/><b>[..."boost-discount-abs-from=1000"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_omm_parallel.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2801)</b><br><b>[..."boost-discount-abs-from=2000"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_omm_parallel.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2810)</b><br>

---

#### Cgi: <b>[boost-discount-from](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2697)</b>
Описание:

Пример использования:
```example: &boost-discount-from=[SOME_VALUE]...```<br/><b>[..."boost-discount-from=10"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_omm_parallel.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2852)</b><br><b>[..."boost-discount-from=20"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_omm_parallel.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2861)</b><br>

---

#### Cgi: <b>[boost-discount](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2701)</b>
Описание:
https://st.yandex-team.ru/MARKETYA-35<br/>
Пример использования:
```example: &boost-discount=[SOME_VALUE]...```<br/><b>[..."boost-discount=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_omm_parallel.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L3035)</b><br><b>[..."boost-discount=0"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_omm_parallel.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L3044)</b><br><b>[..."boost-discount=5"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_omm_parallel.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L3053)</b><br>

---

#### Cgi: <b>[boostParentPromoId](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2184)</b>
Описание:
 A single parentPromoId used for boosting offers in DJ<br/><b>Возвращаемое значение</b>: value of CGI-parameter &boostParentPromoId<br/>https://st.yandex-team.ru/MARKETOUT-46239<br/>
Пример использования:
```example: &boostParentPromoId=[SOME_VALUE]...```<br/><b>[..."boostParentPromoId=four"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_dj.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2605)</b><br><b>[..."boostParentPromoId="...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_dj_place.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1945)</b><br>

---

#### Cgi: <b>[boostShopPromoId](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2190)</b>
Описание:
 a list of shopPromoId used for boosting offers in DJ<br/><b>Возвращаемое значение</b>: value of CGI-parameter &boostShopPromoId<br/>https://st.yandex-team.ru/MARKETOUT-46239<br/>
Пример использования:
```example: &boostShopPromoId=[SOME_VALUE]...```<br/>

---

#### Cgi: <b>[bsformat](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L484)</b>
Описание:
<b>Возвращаемое значение</b>: output format (cgi: &bsformat=...)<br/>
Пример использования:
```example: &bsformat=[SOME_VALUE]...```<br/><b>[..."bsformat=2"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_bids_recommender_cpa_uncollapse.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L293)</b><br><b>[..."bsformat=2"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_bids_recommender_cpa_uncollapse.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L363)</b><br><b>[..."bsformat=2"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_bids_recommender_cpa_uncollapse.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L441)</b><br>

---

#### Cgi: <b>[business-id](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2890)</b>
Описание:
<b>Возвращаемое значение</b>: list of business identifiers. Now used just for some places. Be carefull<br/>
Пример использования:
```example: &business-id=[SOME_VALUE]...```<br/><b>[..."business-id=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_get_eats_warehouses.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L160)</b><br><b>[..."business-id=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_get_eats_warehouses.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L178)</b><br><b>[..."business-id=3"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_get_eats_warehouses.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L197)</b><br>

---

#### Cgi: <b>[by-letter](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L598)</b>
Описание:
 First letter of shop name for place=shops_list<br/><b>Возвращаемое значение</b>: value of CGI-parameter &by-letter<br/>
Пример использования:
```example: &by-letter=[SOME_VALUE]...```<br/><b>[..."by-letter=a"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_shops_list.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L27)</b><br><b>[..."by-letter=б"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_shops_list.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L53)</b><br><b>[..."by-letter=%D0%B1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_shops_list.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L78)</b><br>

---

#### Cgi: <b>[cache-feed-info](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2381)</b>
Описание:
https://st.yandex-team.ru/MARKETOUT-39160<br/>
Пример использования:
```example: &cache-feed-info=[SOME_VALUE]...```<br/><b>[..."cache-feed-info="...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_direct_offers_wizard.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L198)</b><br><b>[..."cache-feed-info="...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_direct_offers_wizard.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L230)</b><br><b>[..."cache-feed-info="...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_direct_offers_wizard.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L257)</b><br>

---

#### Cgi: <b>[calc-pack](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1237)</b>
Описание:
 Calculate-mode for single pack price recalculation<br/><b>Возвращаемое значение</b>: value of CGI-parameter &calc-pack<br/>
Пример использования:
```example: &calc-pack=[SOME_VALUE]...```<br/><b>[..."calc-pack=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_alt_same_shop.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2533)</b><br><b>[..."calc-pack="...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_alt_same_shop.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2620)</b><br><b>[..."calc-pack=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_alt_same_shop.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2622)</b><br>

---

#### Cgi: <b>[calculate-delivery](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2167)</b>
Описание:
<b>Возвращаемое значение</b>: value of CGI-parameter &calculate-delivery<br/> Is used in blue prime, blue_tariffs<br/>https://st.yandex-team.ru/BMP-1662<br/>
Пример использования:
```example: &calculate-delivery=[SOME_VALUE]...```<br/><b>[..."calculate-delivery="...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_white_cpa_on_blue.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L637)</b><br><b>[..."calculate-delivery=0"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_place_blue_tariffs.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1110)</b><br><b>[..."calculate-delivery=0"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_place_blue_tariffs.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1114)</b><br>

---

#### Cgi: <b>[capi-parser](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L160)</b>
Описание:
https://st.yandex-team.ru/MARKETOUT-31622<br/>
Пример использования:
```example: &capi-parser=[SOME_VALUE]...```<br/><b>[..."capi-parser=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_pruning_tbs_tpsz.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L601)</b><br><b>[..."capi-parser=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_pruning_tbs_tpsz.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L604)</b><br><b>[..."capi-parser=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_pruning_tbs_tpsz.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L612)</b><br>

---

#### Cgi: <b>[card-analogs-count](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2579)</b>
Описание:
<b>Возвращаемое значение</b>: value of CGI-parameter &card-analogs-count<br/>https://st.yandex-team.ru/MARKETOUT-37797<br/>
Пример использования:
```example: &card-analogs-count=[SOME_VALUE]...```<br/><b>[..."card-analogs-count=100"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_productoffers_analogs.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1346)</b><br>

---

#### Cgi: <b>[cart, cart-fo, cart-sku](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1300)</b>
Описание:
 WareMd5 or FeedOfferId  of offers in user cart (to give somo promo)<br/> &cart, &cart-fo &cart-sku<br/>https://st.yandex-team.ru/MARKETOUT-24781<br/>
Пример использования:
```example: &cart=[SOME_VALUE]...```<br/><b>[..."cart=Kalach____1P_________g"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_split_cart.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L110)</b><br><b>[..."cart=Pastila___3P_________g"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_split_cart.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L127)</b><br><b>[..."cart="...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_pricedrop_kit.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L105)</b><br>```example: &cart-fo=[SOME_VALUE]...```<br/><b>[..."cart-fo=BLUEModel1FEED3333wwww"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_pricedrop_kit.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L554)</b><br><b>[..."cart-fo=feed_offer_id"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_promo_by_cart.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1401)</b><br>```example: &cart-sku=[SOME_VALUE]...```<br/><b>[..."cart-sku=BLUEModel3FEED1111gggg"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_pricedrop_kit.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L554)</b><br><b>[..."cart-sku=247300012"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_beru_bonuses.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L450)</b><br><b>[..."cart-sku=msk"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_promo_by_cart.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1401)</b><br>

---

#### Cgi: <b>[cashback-percent-from](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L190)</b>
Описание:

Пример использования:
```example: &cashback-percent-from=[SOME_VALUE]...```<br/>

---

#### Cgi: <b>[categories-only-with-reviews](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1820)</b>
Описание:
<b>Возвращаемое значение</b>: value of CGI parameter &categories-only-with-reviews<br/>https://st.yandex-team.ru/MARKETOUT-18402<br/> для списка категорий в виджете "почитать отзывы"<br/>
Пример использования:
```example: &categories-only-with-reviews=[SOME_VALUE]...```<br/><b>[..."categories-only-with-reviews=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_categories_and_models_by_history.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L348)</b><br>

---

#### Cgi: <b>[cc](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2950)</b>
Описание:
<b>Возвращаемое значение</b>: encoded click context<br/>https://st.yandex-team.ru/MARKETOUT-47151<br/>
Пример использования:
```example: &cc=[SOME_VALUE]...```<br/><b>[..."cc="...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_productoffers_filters.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L750)</b><br><b>[..."cc="...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_click_log.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1359)</b><br><b>[..."cc="...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_click_log.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1393)</b><br>

---

#### Cgi: <b>[cflags](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1220)</b>
Описание:
 Flags for CPA fraud detection, default 0<br/>https://st.yandex-team.ru/MARKETOUT-10344<br/><b>Возвращаемое значение</b>: value of CGI-parameter "&cflags="<br/>
Пример использования:
```example: &cflags=[SOME_VALUE]...```<br/><b>[..."cflags=10"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_show_log.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1318)</b><br>

---

#### Cgi: <b>[character](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1607)</b>
Описание:

Пример использования:
```example: &character=[SOME_VALUE]...```<br/><b>[..."character=4"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_brand_products.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1626)</b><br><b>[..."character=2"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_brand_products.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1640)</b><br><b>[..."character=2"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_brand_products.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1654)</b><br>

---

#### Cgi: <b>[check-availability](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2488)</b>
Описание:
 Marker for query, checking enough count of pricedrop models (for place=promo_cart_discount)<br/>https://st.yandex-team.ru/MARKETRECOM-2548<br/><b>Возвращаемое значение</b>: value of CGI parameter "&check-availability"<br/>
Пример использования:
```example: &check-availability=[SOME_VALUE]...```<br/><b>[..."check-availability=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_promo_by_cart.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L3840)</b><br><b>[..."check-availability=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_promo_by_cart.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L3863)</b><br>

---

#### Cgi: <b>[check-models](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2136)</b>
Описание:
<b>Возвращаемое значение</b>: if is true TPlaceBrandProducts place should only check is model on sale or not<br/>https://st.yandex-team.ru/MARKETOUT-46732<br/>
Пример использования:
```example: &check-models=[SOME_VALUE]...```<br/><b>[..."check-models=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_brand_products.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1082)</b><br><b>[..."check-models=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_brand_products.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1106)</b><br>

---

#### Cgi: <b>[check-offers-filter](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2439)</b>
Описание:
 Parameter to enable/disble checking offers filter reason<br/> Ручка причин отсутствия офферов. offer disabled reasons<br/>https://st.yandex-team.ru/MARKETOUT-32251<br/>
Пример использования:
```example: &check-offers-filter=[SOME_VALUE]...```<br/><b>[..."check-offers-filter=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_check_offers.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L144)</b><br>

---

#### Cgi: <b>[chosen-hyperid](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1951)</b>
Описание:
<b>Возвращаемое значение</b>: value of CGI parameter &chosen-hyperid<br/>https://st.yandex-team.ru/MARKETOUT-19594<br/>
Пример использования:
```example: &chosen-hyperid=[SOME_VALUE]...```<br/>

---

#### Cgi: <b>[chunk](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1018)</b>
Описание:

Пример использования:
```example: &chunk=[SOME_VALUE]...```<br/>

---

#### Cgi: <b>[click-n-collect](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L181)</b>
Описание:

Пример использования:
```example: &click-n-collect=[SOME_VALUE]...```<br/><b>[..."click-n-collect=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_click_n_collect.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L606)</b><br>

---

#### Cgi: <b>[clid](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1801)</b>
Описание:
<b>Возвращаемое значение</b>: value of CGI parameter &clid<br/>https://st.yandex-team.ru/MARKETOUT-17784<br/> clid - это число, обозначающее, из какого внещнего источника ссылка на маркет<br/>
Пример использования:
```example: &clid=[SOME_VALUE]...```<br/><b>[..."clid=456"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_alice.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L38)</b><br><b>[..."clid=456"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_alice.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L62)</b><br><b>[..."clid=632"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_model_wizard.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L343)</b><br>

---

#### Cgi: <b>[client](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1254)</b>
Описание:
 Client id<br/><b>Возвращаемое значение</b>: value of CGI-parameter &client<br/>
Пример использования:
```example: &client=[SOME_VALUE]...```<br/><b>[..."client=other"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_eats_hyperlocality_time.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L102)</b><br><b>[..."client=sovetnik"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_hide_cpc_links.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L121)</b><br><b>[..."client=sovetnik"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_hide_cpc_links.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L129)</b><br>

---

#### Cgi: <b>[client](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1259)</b>
Описание:
https://st.yandex-team.ru/MARKETRECOM-2294<br/><b>Возвращаемое значение</b>: value of CGI-parameter &client<br/>
Пример использования:
```example: &client=[SOME_VALUE]...```<br/><b>[..."client=other"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_eats_hyperlocality_time.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L102)</b><br><b>[..."client=sovetnik"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_hide_cpc_links.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L121)</b><br><b>[..."client=sovetnik"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_hide_cpc_links.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L129)</b><br>

---

#### Cgi: <b>[co-from](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1362)</b>
Описание:
 Checkouter part<br/>
Пример использования:
```example: &co-from=[SOME_VALUE]...```<br/><b>[..."co-from=shopadmin-stub"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_delivery.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1675)</b><br><b>[..."co-from=shopadmin-stub"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_delivery.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1686)</b><br><b>[..."co-from=shopadmin-stub"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_delivery_literal.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1645)</b><br>

---

#### Cgi: <b>[columns-in-grid](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2802)</b>
Описание:
<b>Возвращаемое значение</b>: value of &columns-in-grid CGI-parameter<br/>
Пример использования:
```example: &columns-in-grid=[SOME_VALUE]...```<br/><b>[..."columns-in-grid=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_blender.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1750)</b><br><b>[..."columns-in-grid=3"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_blender_blending.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L663)</b><br><b>[..."columns-in-grid=2"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_blender_blending.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L729)</b><br>

---

#### Cgi: <b>[combinator](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2459)</b>
Описание:
 Return delivery calculated by combinator<br/><b>Возвращаемое значение</b>: value of CGI-parameter &combinator<br/>
Пример использования:
```example: &combinator=[SOME_VALUE]...```<br/><b>[..."combinator=0"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_adjust_shipment_by_supplier.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L219)</b><br><b>[..."combinator=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_deferred_courier_delivery.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L155)</b><br><b>[..."combinator=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_flat_courier_options.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L80)</b><br>

---

#### Cgi: <b>[commonly-purchased-ordered](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2032)</b>
Описание:
<b>Возвращаемое значение</b>: value of CGI-parameter &commonly-purchased-ordered<br/>https://st.yandex-team.ru/MARKETOUT-25324<br/>
Пример использования:
```example: &commonly-purchased-ordered=[SOME_VALUE]...```<br/>

---

#### Cgi: <b>[compact-offer-output](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2749)</b>
Описание:
https://st.yandex-team.ru/MARKETOUT-38876<br/>
Пример использования:
```example: &compact-offer-output=[SOME_VALUE]...```<br/><b>[..."compact-offer-output="...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_blue_promo_blue_flash.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L412)</b><br>

---

#### Cgi: <b>[compact-regions](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2725)</b>
Описание:
https://st.yandex-team.ru/MARKETOUT-39905<br/>
Пример использования:
```example: &compact-regions=[SOME_VALUE]...```<br/><b>[..."compact-regions=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_outlet_delivery.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L800)</b><br>

---

#### Cgi: <b>[compress-working-time](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1777)</b>
Описание:
 MARKETOUT-17943 compress working time representation<br/>
Пример использования:
```example: &compress-working-time=[SOME_VALUE]...```<br/><b>[..."compress-working-time=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_outlet_delivery.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L3631)</b><br><b>[..."compress-working-time=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_outlet_delivery.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L3684)</b><br>

---

#### Cgi: <b>[condition](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2919)</b>
Описание:
<b>Возвращаемое значение</b>: value of filter condition=new/cutprice<br/>https://st.yandex-team.ru/MARKETOUT-45920<br/>
Пример использования:
```example: &condition=[SOME_VALUE]...```<br/><b>[..."condition="...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_used_goods.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L138)</b><br>

---

#### Cgi: <b>[content-api-client](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1353)</b>
Описание:
 Content API client<br/><b>Возвращаемое значение</b>: value of CGI parameter "&content-api-client"<br/>
Пример использования:
```example: &content-api-client=[SOME_VALUE]...```<br/><b>[..."content-api-client=11652"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_blue_on_green.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L382)</b><br><b>[..."content-api-client=14012"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_blue_on_green.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L385)</b><br><b>[..."content-api-client=14012"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_blue_on_green.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L389)</b><br>

---

#### Cgi: <b>[cost-of-delivery](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L849)</b>
Описание:
 Filter by cost of delivery option<br/><b>Возвращаемое значение</b>: value of CGI-parameter &cost-of-delivery<br/>
Пример использования:
```example: &cost-of-delivery=[SOME_VALUE]...```<br/><b>[..."cost-of-delivery=free"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_pickup_included_filter.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L352)</b><br><b>[..."cost-of-delivery=free"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_pickup_included_filter.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L398)</b><br><b>[..."cost-of-delivery=included"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_pickup_included_filter.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L688)</b><br>

---

#### Cgi: <b>[cpa-out-of-stock-models](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2729)</b>
Описание:
https://st.yandex-team.ru/MARKETOUT-38808<br/>
Пример использования:
```example: &cpa-out-of-stock-models=[SOME_VALUE]...```<br/><b>[..."cpa-out-of-stock-models=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_out_of_stock_models.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L80)</b><br><b>[..."cpa-out-of-stock-models=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_out_of_stock_models.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L106)</b><br><b>[..."cpa-out-of-stock-models=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_out_of_stock_models.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L120)</b><br>

---

#### Cgi: <b>[cpa-pof](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L700)</b>
Описание:
 Pof-value for CPA-offers<br/><b>Возвращаемое значение</b>: CGI-parameter &cpa-pof<br/>
Пример использования:
```example: &cpa-pof=[SOME_VALUE]...```<br/><b>[..."cpa-pof=newpof"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_click_log.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L467)</b><br><b>[..."cpa-pof=cpapof"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_click_log.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L471)</b><br><b>[..."cpa-pof=somepof"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_cpa.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L684)</b><br>

---

#### Cgi: <b>[cpa](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L497)</b>
Описание:
<b>Возвращаемое значение</b>: &cpa= parameter. CGI-parameter<br/>
Пример использования:
```example: &cpa=[SOME_VALUE]...```<br/><b>[..."cpa=-n"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_hide_cpc_links.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L234)</b><br><b>[..."cpa=-no"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_hide_cpc_links.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L239)</b><br><b>[..."cpa=-n"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_hide_cpc_links.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L247)</b><br>

---

#### Cgi: <b>[cpc](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L859)</b>
Описание:
 Explicitly passed Click Price<br/><b>Возвращаемое значение</b>: value of CGI-parameter &cpc<br/>
Пример использования:
```example: &cpc=[SOME_VALUE]...```<br/><b>[..."cpc=%s"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_cpa_in_top_ranging.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1465)</b><br><b>[..."cpc=%s"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_cpa_in_top_ranging.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1517)</b><br><b>[..."cpc=%s"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_cpa_in_top_ranging.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1563)</b><br>

---

#### Cgi: <b>[cpmdo](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1699)</b>
Описание:
 Use most cpm offer instead of default offer<br/>
Пример использования:
```example: &cpmdo=[SOME_VALUE]...```<br/><b>[..."cpmdo=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_default_offer_alice.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L68)</b><br><b>[..."cpmdo=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_default_offer_alice.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L74)</b><br>

---

#### Cgi: <b>[credit-template-id](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L844)</b>
Описание:
 Show offers only with credit and this credit template id<br/><b>Возвращаемое значение</b>: value of CGI-parameter &credit-template-id<br/>
Пример использования:
```example: &credit-template-id=[SOME_VALUE]...```<br/><b>[..."credit-template-id=300"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_credit.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1262)</b><br><b>[..."credit-template-id=301"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_credit.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1272)</b><br>

---

#### Cgi: <b>[credit-type](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L834)</b>
Описание:
 Filter by credit type<br/><b>Возвращаемое значение</b>: value of CGI-parameter &credit-type<br/>
Пример использования:
```example: &credit-type=[SOME_VALUE]...```<br/><b>[..."credit-type=credit"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_credit.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L230)</b><br><b>[..."credit-type=installment"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_credit.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L273)</b><br><b>[..."credit-type=credit"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_credit.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L363)</b><br>

---

#### Cgi: <b>[currency-from](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1306)</b>
Описание:
 Currency to convert from (currency-from)<br/>https://st.yandex-team.ru/MARKETOUT-11520<br/><b>Возвращаемое значение</b>: value of CGI parameter "&currency-from"<br/>
Пример использования:
```example: &currency-from=[SOME_VALUE]...```<br/><b>[..."currency-from=RUB"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_currencies_complete.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L77)</b><br><b>[..."currency-from=RUB"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_currency_convert.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L40)</b><br><b>[..."currency-from=RUB"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_currency_convert.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L48)</b><br>

---

#### Cgi: <b>[currency-to](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1312)</b>
Описание:
 Currency to convert to (currency-to)<br/>https://st.yandex-team.ru/MARKETOUT-11520<br/><b>Возвращаемое значение</b>: value of CGI parameter "&currency-to"<br/>
Пример использования:
```example: &currency-to=[SOME_VALUE]...```<br/><b>[..."currency-to=RUB"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_currencies_complete.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L77)</b><br><b>[..."currency-to=RUB"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_currency_convert.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L44)</b><br><b>[..."currency-to=RUB"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_currency_convert.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L48)</b><br>

---

#### Cgi: <b>[currency-value](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1318)</b>
Описание:
 Amount to convert between currencies (currency-value)<br/>https://st.yandex-team.ru/MARKETOUT-11520<br/><b>Возвращаемое значение</b>: value of CGI parameter "&currency-value"<br/>
Пример использования:
```example: &currency-value=[SOME_VALUE]...```<br/><b>[..."currency-value=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_currencies_complete.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L77)</b><br><b>[..."currency-value=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_currency_convert.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L52)</b><br><b>[..."currency-value=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_currency_convert.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L56)</b><br>

---

#### Cgi: <b>[currency](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L358)</b>
Описание:
<b>Возвращаемое значение</b>: value of &currency=... CGI-parameter<br/> @todo: use stricter type<br/>
Пример использования:
```example: &currency=[SOME_VALUE]...```<br/><b>[..."currency=RUR"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_place_credit_info.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L208)</b><br><b>[..."currency=RUR"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_place_credit_info.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L313)</b><br><b>[..."currency=RUR"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_place_credit_info.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L382)</b><br>

---

#### Cgi: <b>[cvredirect](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L573)</b>
Описание:
 Enable/disable redirects<br/><b>Возвращаемое значение</b>: value of CGI-parameter &cvredirect<br/>
Пример использования:
```example: &cvredirect=[SOME_VALUE]...```<br/><b>[..."cvredirect=0"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_model_wizard.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1008)</b><br><b>[..."cvredirect=0"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_model_wizard.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1016)</b><br><b>[..."cvredirect=0"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_model_wizard.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1024)</b><br>

---

#### Cgi: <b>[debug-all-courier-options](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1683)</b>
Описание:
<b>Возвращаемое значение</b>: &debug-all-courier-options<br/> and deprecated &all-courier-options<br/>
Пример использования:
```example: &debug-all-courier-options=[SOME_VALUE]...```<br/><b>[..."debug-all-courier-options=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_delivery.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1621)</b><br><b>[..."debug-all-courier-options=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_delivery.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1622)</b><br><b>[..."debug-all-courier-options=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_delivery_literal.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1338)</b><br>

---

#### Cgi: <b>[debug-daily-deal-timestamp](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L871)</b>
Описание:
 Timestamp for DailyOffers place<br/><b>Возвращаемое значение</b>: value of CGI-parameter &debug-daily-deal-timestamp<br/>
Пример использования:
```example: &debug-daily-deal-timestamp=[SOME_VALUE]...```<br/>

---

#### Cgi: <b>[debug-doc-count](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L866)</b>
Описание:
 Maximal count of documents from single shard that will be processed during relevance calculation to collect debug info.<br/> Documents are sorted by relevance.<br/> Debug data for documents on page output will be collected in any case.<br/><b>Возвращаемое значение</b>: value of CGI-parameter &debug-doc-count<br/>
Пример использования:
```example: &debug-doc-count=[SOME_VALUE]...```<br/><b>[..."debug-doc-count=10"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_parallel.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L352)</b><br><b>[..."debug-doc-count="...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_parallel.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L491)</b><br><b>[..."debug-doc-count=20"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_parallel.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L498)</b><br>

---

#### Cgi: <b>[debug-ignore-vendor-min-publish-timestamp](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1780)</b>
Описание:

Пример использования:
```example: &debug-ignore-vendor-min-publish-timestamp=[SOME_VALUE]...```<br/><b>[..."debug-ignore-vendor-min-publish-timestamp=true"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_sku_offers.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L521)</b><br><b>[..."debug-ignore-vendor-min-publish-timestamp=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_vendor_min_publish_timestamp.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L111)</b><br>

---

#### Cgi: <b>[debug-trace-filter](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L385)</b>
Описание:
<b>Возвращаемое значение</b>: list of strings to filter logicTrace of debug<br/><b>Заметка</b>: позволяет пофильтровать дебажную инфу по подстроке<br/> передайте "-подстрока1,-подстрока2" чтобы удалить вывод содержащий подстроки подстрока1 или подстрока2<br/> передайте "подстрока1,подстрока2" чтобы оставить вывод содержащий только данные подстроки<br/> передайте "all" чтобы убрать любую фильтрацию<br/> передайте "no" чтобы убрать весь logicTrace<br/>
Пример использования:
```example: &debug-trace-filter=[SOME_VALUE]...```<br/><b>[..."debug-trace-filter=prime_base"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_debug.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L849)</b><br><b>[..."debug-trace-filter=-prime_base"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_debug.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L857)</b><br><b>[..."debug-trace-filter=prime_base"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_debug.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L866)</b><br>

---

#### Cgi: <b>[debug-trace-time](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L390)</b>
Описание:
<b>Возвращаемое значение</b>: value of &debug-trace-time=[0/1] default: 1<br/><b>Заметка</b>: добавляет в дебажные сообщения точное время<br/>
Пример использования:
```example: &debug-trace-time=[SOME_VALUE]...```<br/>

---

#### Cgi: <b>[debug-truncated](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L401)</b>
Описание:
<b>Возвращаемое значение</b>: value of &debug-trace-truncate (default: 1)<br/> truncate output strings in logicTrace up to 250 symbols<br/> do not work if debug-trace-filter=substr (positive filtration)<br/>
Пример использования:
```example: &debug-truncated=[SOME_VALUE]...```<br/>

---

#### Cgi: <b>[default-offer-min-price](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1496)</b>
Описание:
 Enable default offer with min price<br/>https://st.yandex-team.ru/MARKETPROJECT-558<br/><b>Возвращаемое значение</b>: value of CGI parameter "&default-offer-min-price"<br/>
Пример использования:
```example: &default-offer-min-price=[SOME_VALUE]...```<br/><b>[..."default-offer-min-price=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_default_offer.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1781)</b><br>

---

#### Cgi: <b>[default-parent-promo](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2203)</b>
Описание:

Пример использования:
```example: &default-parent-promo=[SOME_VALUE]...```<br/>

---

#### Cgi: <b>[delivery-interval](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2454)</b>
Описание:
 Delivery interval chosen by user. Used as a filter for delivery route search<br/><b>Возвращаемое значение</b>: value of CGI-parameter &delivery-interval<br/>
Пример использования:
```example: &delivery-interval=[SOME_VALUE]...```<br/><b>[..."delivery-interval="...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_combinator_string_delivery_dates.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L234)</b><br><b>[..."delivery-interval="...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_deferred_courier_delivery.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L172)</b><br><b>[..."delivery-interval="...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_on_demand_delivery.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L294)</b><br>

---

#### Cgi: <b>[delivery-methods](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2812)</b>
Описание:
https://wiki.yandex-team.ru/users/vladankor/actualdelivery/<br/><b>Возвращаемое значение</b>: value of CGI parameter &delivery-methods<br/>
Пример использования:
```example: &delivery-methods=[SOME_VALUE]...```<br/><b>[..."delivery-methods="...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_actual_delivery_work_mode.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L596)</b><br><b>[..."delivery-methods="...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_actual_delivery_work_mode.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L720)</b><br><b>[..."delivery-methods="...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_actual_delivery_work_mode.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L803)</b><br>

---

#### Cgi: <b>[delivery-stats](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2076)</b>
Описание:
<b>Возвращаемое значение</b>: value of CGI-parameter &delivery-stats<br/>https://st.yandex-team.ru/MARKETOUT-26939<br/>
Пример использования:
```example: &delivery-stats=[SOME_VALUE]...```<br/><b>[..."delivery-stats=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_pickup_modifiers.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L166)</b><br><b>[..."delivery-stats=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_pickup_modifiers.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L171)</b><br><b>[..."delivery-stats=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_courier_modifiers.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L524)</b><br>

---

#### Cgi: <b>[delivery-status-id](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1444)</b>
Описание:
 Delivery status id for delivery_status<br/>https://st.yandex-team.ru/MARKETOUT-13021<br/>
Пример использования:
```example: &delivery-status-id=[SOME_VALUE]...```<br/><b>[..."delivery-status-id=0"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_delivery_status.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L38)</b><br><b>[..."delivery-status-id=0"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_delivery_status.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L45)</b><br><b>[..."delivery-status-id=0"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_delivery_status.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L62)</b><br>

---

#### Cgi: <b>[delivery-subtype](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2449)</b>
Описание:
 Return delivery subtype (ordinary/on-demand/etc.) for delivery options calculation in combinator<br/><b>Возвращаемое значение</b>: value of CGI-parameter &delivery-subtype<br/>
Пример использования:
```example: &delivery-subtype=[SOME_VALUE]...```<br/><b>[..."delivery-subtype="...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_deferred_courier_delivery.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L170)</b><br><b>[..."delivery-subtype="...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_on_demand_delivery.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L293)</b><br><b>[..."delivery-subtype=ordinary"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_subscription_goods_free_delivery.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L379)</b><br>

---

#### Cgi: <b>[delivery-type](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2444)</b>
Описание:
 Return delivery type (courier/pickup/post) for delivery route search in combinator<br/><b>Возвращаемое значение</b>: value of CGI-parameter &delivery-type<br/>
Пример использования:
```example: &delivery-type=[SOME_VALUE]...```<br/><b>[..."delivery-type="...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_combinator_string_delivery_dates.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L232)</b><br><b>[..."delivery-type="...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_deferred_courier_delivery.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L169)</b><br><b>[..."delivery-type="...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_delivery_route_error_log.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L88)</b><br>

---

#### Cgi: <b>[deliveryServiceId](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L299)</b>
Описание:

Пример использования:
```example: &deliveryServiceId=[SOME_VALUE]...```<br/><b>[..."deliveryServiceId=103"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_multi_service_pickup.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L586)</b><br><b>[..."deliveryServiceId=123"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_multi_service_pickup.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L589)</b><br><b>[..."deliveryServiceId=103"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_multi_service_pickup.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L593)</b><br>

---

#### Cgi: <b>[delivery_interval](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L896)</b>
Описание:
 Return offers that can be delivered in specified time<br/><b>Возвращаемое значение</b>: value of CGI-parameter &delivery_interval<br/>
Пример использования:
```example: &delivery_interval=[SOME_VALUE]...```<br/><b>[..."delivery_interval=2"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_geo.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L42)</b><br><b>[..."delivery_interval=2"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_productoffers_filters.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L34)</b><br><b>[..."delivery_interval="...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_dsbs_delivery.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1120)</b><br>

---

#### Cgi: <b>[deliveryincluded](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L824)</b>
Описание:
 Set if delivery price should be included in offer price<br/><b>Возвращаемое значение</b>: value of CGI-parameter &deliveryincluded<br/>
Пример использования:
```example: &deliveryincluded=[SOME_VALUE]...```<br/><b>[..."deliveryincluded=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_default_offer.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L577)</b><br><b>[..."deliveryincluded=0"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_default_offer.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L584)</b><br><b>[..."deliveryincluded=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_default_offer.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1060)</b><br>

---

#### Cgi: <b>[deug-bs-req](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L395)</b>
Описание:
<b>Возвращаемое значение</b>: value of &debug-bs-req<br/> turn on to debug output full request to basesearch and full SortingSpec proto<br/>
Пример использования:
```example: &deug-bs-req=[SOME_VALUE]...```<br/>

---

#### Cgi: <b>[device](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1791)</b>
Описание:

Пример использования:
```example: &device=[SOME_VALUE]...```<br/><b>[..."device=touch"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_place_images.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L153)</b><br><b>[..."device=touch"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_place_images.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L174)</b><br><b>[..."device=touch"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_place_images.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L188)</b><br>

---

#### Cgi: <b>[deviceid](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2560)</b>
Описание:
<b>Возвращаемое значение</b>: value of CGI parameter "&deviceid"<br/>
Пример использования:
```example: &deviceid=[SOME_VALUE]...```<br/><b>[..."deviceid="...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_dj.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2403)</b><br><b>[..."deviceid="...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_dj.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2410)</b><br>

---

#### Cgi: <b>[disable-accessories-merge](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2833)</b>
Описание:
<b>Возвращаемое значение</b>: cgi: "disable-accessories-merge"<br/>https://st.yandex-team.ru/MARKETRECOM-4207<br/>
Пример использования:
```example: &disable-accessories-merge=[SOME_VALUE]...```<br/><b>[..."disable-accessories-merge=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_complementary_product_groups_blue.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L436)</b><br>

---

#### Cgi: <b>[disable-force-pull-to-min-bid](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2556)</b>
Описание:
 Disable forcing pulling to min bid (e.g. by '&api=partner')<br/><b>Возвращаемое значение</b>: value of CGI parameter "&disable-force-pull-to-min-bid"<br/>
Пример использования:
```example: &disable-force-pull-to-min-bid=[SOME_VALUE]...```<br/>

---

#### Cgi: <b>[disable-model-stats](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1752)</b>
Описание:
 MARKETOUT-17701 - Ускоряем поиск. Нам не всегда нужны дин статистики.<br/>
Пример использования:
```example: &disable-model-stats=[SOME_VALUE]...```<br/>

---

#### Cgi: <b>[disable-rotation-on-blue](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1687)</b>
Описание:
<b>Возвращаемое значение</b>: &disable-rotation-on-blue<br/>
Пример использования:
```example: &disable-rotation-on-blue=[SOME_VALUE]...```<br/><b>[..."disable-rotation-on-blue=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_documents_tracer.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L871)</b><br><b>[..."disable-rotation-on-blue=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_documents_tracer.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1025)</b><br><b>[..."disable-rotation-on-blue=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_blue_market.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2212)</b><br>

---

#### Cgi: <b>[disable-snippet-request](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2519)</b>
Описание:
 Switch off snippet requests for PriceLabs<br/>https://st.yandex-team.ru/MARKETOUT-33725<br/>
Пример использования:
```example: &disable-snippet-request=[SOME_VALUE]...```<br/>

---

#### Cgi: <b>[disable-testing-features](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1179)</b>
Описание:
 Overrides config EnableTestingFeatures option<br/><b>Возвращаемое значение</b>: CGI-value &disable-testing-features=<br/>
Пример использования:
```example: &disable-testing-features=[SOME_VALUE]...```<br/><b>[..."disable-testing-features=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_book_now.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2106)</b><br><b>[..."disable-testing-features=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_book_now.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2120)</b><br><b>[..."disable-testing-features=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_features_log.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L519)</b><br>

---

#### Cgi: <b>[disabled-promo-thresholds](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1748)</b>
Описание:

Пример использования:
```example: &disabled-promo-thresholds=[SOME_VALUE]...```<br/><b>[..."disabled-promo-thresholds=something_else"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_blue_promo_blue_promocode.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1182)</b><br>

---

#### Cgi: <b>[disabled_restrictions](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1028)</b>
Описание:
 Allows to disable some restrictions by name<br/><b>Возвращаемое значение</b>: CGI-value &disabled_restrictions<br/>
Пример использования:
```example: &disabled_restrictions=[SOME_VALUE]...```<br/>

---

#### Cgi: <b>[discount-abs-from](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L954)</b>
Описание:
<b>Возвращаемое значение</b>: CGI-value &discount-abs-from<br/>
Пример использования:
```example: &discount-abs-from=[SOME_VALUE]...```<br/><b>[..."discount-abs-from=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_discount_range_filter_blue.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L82)</b><br><b>[..."discount-abs-from=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_discount_range_filter_blue.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L92)</b><br><b>[..."discount-abs-from=100"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_discount_range_filter_blue.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L100)</b><br>

---

#### Cgi: <b>[discount-abs-to](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L958)</b>
Описание:
<b>Возвращаемое значение</b>: CGI-value &discount-abs-to<br/>
Пример использования:
```example: &discount-abs-to=[SOME_VALUE]...```<br/><b>[..."discount-abs-to=10000"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_discount_range_filter_blue.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L82)</b><br><b>[..."discount-abs-to=2"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_discount_range_filter_blue.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L92)</b><br><b>[..."discount-abs-to=200"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_discount_range_filter_blue.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L100)</b><br>

---

#### Cgi: <b>[discount-check-min-price](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L163)</b>
Описание:

Пример использования:
```example: &discount-check-min-price=[SOME_VALUE]...```<br/><b>[..."discount-check-min-price=50"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_default_offer.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L464)</b><br><b>[..."discount-check-min-price=0"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_default_offer.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L471)</b><br><b>[..."discount-check-min-price=0"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_default_offer.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L474)</b><br>

---

#### Cgi: <b>[discount-from](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L193)</b>
Описание:

Пример использования:
```example: &discount-from=[SOME_VALUE]...```<br/><b>[..."discount-from=0"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_discount_range_filter_blue.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L140)</b><br><b>[..."discount-from=0"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_discount_range_filter_blue.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L153)</b><br><b>[..."discount-from=0"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_discount_range_filter_blue.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L165)</b><br>

---

#### Cgi: <b>[discount-to](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L196)</b>
Описание:

Пример использования:
```example: &discount-to=[SOME_VALUE]...```<br/><b>[..."discount-to=100"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_discount_range_filter_blue.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L140)</b><br><b>[..."discount-to=100"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_discount_range_filter_blue.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L153)</b><br><b>[..."discount-to=22"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_discount_range_filter_blue.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L165)</b><br>

---

#### Cgi: <b>[dj-cluster](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2292)</b>
Описание:

Пример использования:
```example: &dj-cluster=[SOME_VALUE]...```<br/>

---

#### Cgi: <b>[dj-default-item-count](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2307)</b>
Описание:

Пример использования:
```example: &dj-default-item-count=[SOME_VALUE]...```<br/><b>[..."dj-default-item-count=16"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_dj.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L436)</b><br>

---

#### Cgi: <b>[dj-hid](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2876)</b>
Описание:
<b>Возвращаемое значение</b>: value of CGI-parameter dj-hid<br/>https://st.yandex-team.ru/MARKETRECOM-4242<br/>
Пример использования:
```example: &dj-hid=[SOME_VALUE]...```<br/>

---

#### Cgi: <b>[dj-match-warehouse](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L199)</b>
Описание:

Пример использования:
```example: &dj-match-warehouse=[SOME_VALUE]...```<br/><b>[..."dj-match-warehouse=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_dj.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2839)</b><br>

---

#### Cgi: <b>[dj-nid](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2881)</b>
Описание:
<b>Возвращаемое значение</b>: value of CGI-parameter dj-nid<br/>https://st.yandex-team.ru/MARKETRECOM-4242<br/>
Пример использования:
```example: &dj-nid=[SOME_VALUE]...```<br/>

---

#### Cgi: <b>[dj-output-items](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2316)</b>
Описание:

Пример использования:
```example: &dj-output-items=[SOME_VALUE]...```<br/><b>[..."dj-output-items=offers"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_popular_products.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L173)</b><br><b>[..."dj-output-items=offers"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_popular_products.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L193)</b><br><b>[..."dj-output-items=models"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_dj.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L580)</b><br>

---

#### Cgi: <b>[dj-output-mode](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2301)</b>
Описание:

Пример использования:
```example: &dj-output-mode=[SOME_VALUE]...```<br/><b>[..."dj-output-mode=loop"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_dj.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L298)</b><br><b>[..."dj-output-mode=loop"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_dj.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L333)</b><br>

---

#### Cgi: <b>[dj-place](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2289)</b>
Описание:
https://st.yandex-team.ru/MARKETRECOM-2205<br/>
Пример использования:
```example: &dj-place=[SOME_VALUE]...```<br/><b>[..."dj-place=test_soft_bans"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_recom_soft_ban.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L130)</b><br><b>[..."dj-place=dj_links_experiment"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_dj_thematic_nid_response.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L105)</b><br><b>[..."dj-place=dj_links_experiment_short"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_dj_thematic_nid_response.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L127)</b><br>

---

#### Cgi: <b>[dj-stats-source-policy](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2304)</b>
Описание:

Пример использования:
```example: &dj-stats-source-policy=[SOME_VALUE]...```<br/><b>[..."dj-stats-source-policy=default_offers"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_dj.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L298)</b><br><b>[..."dj-stats-source-policy=default_offers"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_dj.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L333)</b><br><b>[..."dj-stats-source-policy=default_offers"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_dj.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L436)</b><br>

---

#### Cgi: <b>[dj-timeout](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2295)</b>
Описание:

Пример использования:
```example: &dj-timeout=[SOME_VALUE]...```<br/><b>[..."dj-timeout="...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_dj_place.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L344)</b><br>

---

#### Cgi: <b>[dj-use-default-models](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2310)</b>
Описание:

Пример использования:
```example: &dj-use-default-models=[SOME_VALUE]...```<br/><b>[..."dj-use-default-models=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_dj.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L333)</b><br><b>[..."dj-use-default-models=0"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_dj.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1837)</b><br>

---

#### Cgi: <b>[dj-yamarec-place](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2313)</b>
Описание:

Пример использования:
```example: &dj-yamarec-place=[SOME_VALUE]...```<br/><b>[..."dj-yamarec-place=default-dj-commonly-purchased-models"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_dj.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L436)</b><br>

---

#### Cgi: <b>[djid](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2298)</b>
Описание:

Пример использования:
```example: &djid=[SOME_VALUE]...```<br/><b>[..."djid=test_soft_bans"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_recom_soft_ban.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L130)</b><br><b>[..."djid=discovery_block"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_djid.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L808)</b><br><b>[..."djid="...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_djid.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L851)</b><br>

---

#### Cgi: <b>[do-from-collapsing](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2969)</b>
Описание:
https://st.yandex-team.ru/MARKETOUT-47193<br/>
Пример использования:
```example: &do-from-collapsing=[SOME_VALUE]...```<br/>

---

#### Cgi: <b>[do-waremd5](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L178)</b>
Описание:

Пример использования:
```example: &do-waremd5=[SOME_VALUE]...```<br/><b>[..."do-waremd5="...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_business_offer.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1698)</b><br><b>[..."do-waremd5=aaaaaaaaaaaaaaaaaaaaaQ"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_discounts_in_default_offers.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L121)</b><br><b>[..."do-waremd5=gTL-3D5IXpiHAL-CvNRmNQ"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_wizards_cpa_incut.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L783)</b><br>

---

#### Cgi: <b>[docid_cache_request_type](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L3003)</b>
Описание:
https://st.yandex-team.ru/MARKETOUT-47532<br/> It is used in requests filling docid cache with qtree because we can not deduce request type from them<br/>
Пример использования:
```example: &docid_cache_request_type=[SOME_VALUE]...```<br/><b>[..."docid_cache_request_type=category_no_text"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_docid_cache.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L98)</b><br>

---

#### Cgi: <b>[docs-per-cat](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L476)</b>
Описание:
https://st.yandex-team.ru/MARKETOUT-17273<br/>
Пример использования:
```example: &docs-per-cat=[SOME_VALUE]...```<br/>

---

#### Cgi: <b>[dynamic-filters](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L568)</b>
Описание:
 Whether dynamic filtration is enabled<br/><b>Возвращаемое значение</b>: value of &dynamic-filters, default is true<br/>
Пример использования:
```example: &dynamic-filters=[SOME_VALUE]...```<br/><b>[..."dynamic-filters=0"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_disabled_literal.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L124)</b><br><b>[..."dynamic-filters=no"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_dynamic_filters.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L335)</b><br><b>[..."dynamic-filters=no"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_offer_promo.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1877)</b><br>

---

#### Cgi: <b>[emb](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1957)</b>
Описание:
<b>Возвращаемое значение</b>: value of CGI-parameter &emb<br/>https://st.yandex-team.ru/MARKETRECOM-1431<br/> May be used for similar purposes elsewhere.<br/>
Пример использования:
```example: &emb=[SOME_VALUE]...```<br/>

---

#### Cgi: <b>[enable-foodtech-offers](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2737)</b>
Описание:
https://st.yandex-team.ru/ECOMSERP-79<br/>
Пример использования:
```example: &enable-foodtech-offers=[SOME_VALUE]...```<br/><b>[..."enable-foodtech-offers=eda_retail"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_eats_hyperlocality_time.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L104)</b><br><b>[..."enable-foodtech-offers=eda_retail"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_food_filter.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L21)</b><br><b>[..."enable-foodtech-offers=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_lavka.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L112)</b><br>

---

#### Cgi: <b>[enable-reasons-to-buy](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2161)</b>
Описание:
<b>Возвращаемое значение</b>: value of CGI-parameter &enable-reasons-to-buy<br/>https://st.yandex-team.ru/MARKETRECOM-2992<br/>
Пример использования:
```example: &enable-reasons-to-buy=[SOME_VALUE]...```<br/><b>[..."enable-reasons-to-buy="...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_dj_parallel.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L243)</b><br>

---

#### Cgi: <b>[enable-reasons](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2156)</b>
Описание:
<b>Возвращаемое значение</b>: value of CGI-parameter &enable-reasons<br/>https://st.yandex-team.ru/MARKETOUT-29641<br/>
Пример использования:
```example: &enable-reasons=[SOME_VALUE]...```<br/>

---

#### Cgi: <b>[enable-resale-goods](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2978)</b>
Описание:
https://st.yandex-team.ru/MARKETOUT-47112<br/>
Пример использования:
```example: &enable-resale-goods=[SOME_VALUE]...```<br/><b>[..."enable-resale-goods=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_parametric.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L4680)</b><br><b>[..."enable-resale-goods="...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_resale_goods.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L135)</b><br><b>[..."enable-resale-goods=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_resale_goods.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L352)</b><br>

---

#### Cgi: <b>[encrypted-hyperids](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1886)</b>
Описание:
<b>Возвращаемое значение</b>: value of CGI parameter &encrypted-hyperids<br/>https://st.yandex-team.ru/MARKETOUT-19594<br/>
Пример использования:
```example: &encrypted-hyperids=[SOME_VALUE]...```<br/><b>[..."encrypted-hyperids="...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_omm_parallel.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1168)</b><br><b>[..."encrypted-hyperids=abyrv"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_omm_parallel.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1191)</b><br><b>[..."encrypted-hyperids="...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_omm_parallel.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1763)</b><br>

---

#### Cgi: <b>[entities](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1226)</b>
Описание:
 Entities to show (offer or product)<br/>https://st.yandex-team.ru/MARKETOUT-9351<br/><b>Возвращаемое значение</b>: value of CGI-paramter "&entities"<br/>
Пример использования:
```example: &entities=[SOME_VALUE]...```<br/><b>[..."entities=offer"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_lavka.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L111)</b><br><b>[..."entities=offer"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_white_boosted_offers.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L289)</b><br><b>[..."entities=offer"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_white_boosted_offers.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L346)</b><br>

---

#### Cgi: <b>[exact-match](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L288)</b>
Описание:
<b>Возвращаемое значение</b>: value of &exact-match=<br/> default value: false<br/>https://st.yandex-team.ru/MARKETOUT-18381<br/>
Пример использования:
```example: &exact-match=[SOME_VALUE]...```<br/><b>[..."exact-match=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_pickup_modifiers.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L129)</b><br><b>[..."exact-match=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_pickup_modifiers.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L135)</b><br><b>[..."exact-match=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_pickup_modifiers.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L193)</b><br>

---

#### Cgi: <b>[expand-dimensions-for-box](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1805)</b>
Описание:
<b>Возвращаемое значение</b>: value of CGI parameter &expand-dimensions-for-box<br/>
Пример использования:
```example: &expand-dimensions-for-box=[SOME_VALUE]...```<br/><b>[..."expand-dimensions-for-box=0"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_actual_delivery.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L4495)</b><br><b>[..."expand-dimensions-for-box=0"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_actual_delivery.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L4518)</b><br><b>[..."expand-dimensions-for-box=0"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_actual_delivery.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L4531)</b><br>

---

#### Cgi: <b>[express-warehouse-id](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1910)</b>
Описание:
 Filter express by warehouse<br/>https://st.yandex-team.ru/MARKETOUT-44120<br/>
Пример использования:
```example: &express-warehouse-id=[SOME_VALUE]...```<br/><b>[..."express-warehouse-id="...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_express_offers_hyperlocality.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1489)</b><br>

---

#### Cgi: <b>[express-warehouses](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2041)</b>
Описание:
<b>Возвращаемое значение</b>: warehouse ids as vector of int<br/>
Пример использования:
```example: &express-warehouses=[SOME_VALUE]...```<br/><b>[..."express-warehouses"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_business_offer.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1656)</b><br><b>[..."express-warehouses=11"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_express_offers_hyperlocality.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L931)</b><br><b>[..."express-warehouses=12"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_express_offers_hyperlocality.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L981)</b><br>

---

#### Cgi: <b>[extra-cashback-offers](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2195)</b>
Описание:
<b>Возвращаемое значение</b>: value of CGI-parameter &extra-cashback-offers<br/>https://st.yandex-team.ru/MARKETOUT-44527<br/>
Пример использования:
```example: &extra-cashback-offers=[SOME_VALUE]...```<br/><b>[..."extra-cashback-offers="...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_blue_promo_blue_cashback.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L3425)</b><br>

---

#### Cgi: <b>[extra-promo-hid](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1294)</b>
Описание:
 &extra-promo-hid=1,2<br/>
Пример использования:
```example: &extra-promo-hid=[SOME_VALUE]...```<br/><b>[..."extra-promo-hid=32"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_promo_top_categories.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L218)</b><br>

---

#### Cgi: <b>[family](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L537)</b>
Описание:
 Forces family (without porn) search<br/><b>Возвращаемое значение</b>: value of CGI-parameter &family<br/>
Пример использования:
```example: &family=[SOME_VALUE]...```<br/><b>[..."family=2"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_parallel.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1139)</b><br><b>[..."family=2"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_parallel.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1143)</b><br><b>[..."family=2"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_parallel.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1147)</b><br>

---

#### Cgi: <b>[fapi](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L672)</b>
Описание:
<b>Возвращаемое значение</b>: value of CGI-parameter fapi<br/>
Пример использования:
```example: &fapi=[SOME_VALUE]...```<br/>

---

#### Cgi: <b>[fee](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1458)</b>
Описание:
 Parameter passed to bids recommender or predictor to have recommendations by specifing fee<br/>
Пример использования:
```example: &fee=[SOME_VALUE]...```<br/>

---

#### Cgi: <b>[feed_shoffer_id](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L907)</b>
Описание:
 @DEPRECATED:<br/> Feed Offer ID and Feed ID mixed identifier<br/><b>Возвращаемое значение</b>: value of CGI-parameter &feed_shoffer_id<br/>
Пример использования:
```example: &feed_shoffer_id=[SOME_VALUE]...```<br/><b>[..."feed_shoffer_id="...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_bids_recommender_formulas.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L38)</b><br><b>[..."feed_shoffer_id=9000-9001"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_bids_recommender_cpa_uncollapse.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L293)</b><br><b>[..."feed_shoffer_id=9000-9001"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_bids_recommender_cpa_uncollapse.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L363)</b><br>

---

#### Cgi: <b>[feed_shoffer_id_base64](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L912)</b>
Описание:
 Feed Offer ID and Feed ID mixed identifier encoded in base64<br/><b>Возвращаемое значение</b>: value of CGI-parameter &feed_shoffer_id_base64<br/>
Пример использования:
```example: &feed_shoffer_id_base64=[SOME_VALUE]...```<br/><b>[..."feed_shoffer_id_base64="...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_offer_status.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L41)</b><br><b>[..."feed_shoffer_id_base64="...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_check_offers.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L132)</b><br><b>[..."feed_shoffer_id_base64="...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_bids_recommender.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1333)</b><br>

---

#### Cgi: <b>[feedid](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L553)</b>
Описание:
 The feed id to filter offers by on &place=shopoffers and place=sku_offers.<br/>https://st.yandex-team.ru/MARKETOUT-5940<br/><b>Возвращаемое значение</b>: &feedid= parameter value.<br/>
Пример использования:
```example: &feedid=[SOME_VALUE]...```<br/><b>[..."feedid="...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_miprime.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L178)</b><br><b>[..."feedid=101101"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_shopoffers.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L150)</b><br><b>[..."feedid=101102"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_shopoffers.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L154)</b><br>

---

#### Cgi: <b>[fesh](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L105)</b>
Описание:
 Нам могут передавать айдишники магазинов в параметре &fesh<br/> Может быть передано несклько айдишников в нескольких параметрах. В одном параметре тоже может быть<br/> несколько айди, разделенных запятыми. Перед айди может идти знак '-', что означает, что надо исключить<br/> этот магазин из выдачи<br/>
Пример использования:
```example: &fesh=[SOME_VALUE]...```<br/><b>[..."fesh=1001"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_accessories.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L135)</b><br><b>[..."fesh=1001"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_accessories_facets.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L64)</b><br><b>[..."fesh=1001"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_accessories_facets.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L115)</b><br>

---

#### Cgi: <b>[fill-cache](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2843)</b>
Описание:
<b>Возвращаемое значение</b>: cgi: "fill-cache"<br/>https://st.yandex-team.ru/MARKETOUT-38136<br/>
Пример использования:
```example: &fill-cache=[SOME_VALUE]...```<br/><b>[..."fill-cache=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_docid_cache.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L98)</b><br>

---

#### Cgi: <b>[fill-offer-filters-with-jumptable](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2934)</b>
Описание:
<b>Возвращаемое значение</b>: Fill offer filters with Jump Table params<br/>https://st.yandex-team.ru/MARKETOUT-46114<br/>
Пример использования:
```example: &fill-offer-filters-with-jumptable=[SOME_VALUE]...```<br/><b>[..."fill-offer-filters-with-jumptable=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_offerinfo.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2000)</b><br>

---

#### Cgi: <b>[filter-by-cms-promo](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1928)</b>
Описание:
 show cms promo sku/models only<br/>https://st.yandex-team.ru/MARKETOUT-21867<br/>
Пример использования:
```example: &filter-by-cms-promo=[SOME_VALUE]...```<br/><b>[..."filter-by-cms-promo="...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_cms_promo.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L332)</b><br><b>[..."filter-by-cms-promo=cmspromo2000"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_cms_promo.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L394)</b><br><b>[..."filter-by-cms-promo=123"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_cms_promo.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L407)</b><br>

---

#### Cgi: <b>[filter-by-min-model-price](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2146)</b>
Описание:
<b>Возвращаемое значение</b>: value of CGI-parameter &filter-by-min-model-price<br/>https://st.yandex-team.ru/MARKETOUT-29499<br/>
Пример использования:
```example: &filter-by-min-model-price=[SOME_VALUE]...```<br/><b>[..."filter-by-min-model-price=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_prime.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L5918)</b><br><b>[..."filter-by-min-model-price=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_prime.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L5946)</b><br>

---

#### Cgi: <b>[filter-by-model-rating](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1716)</b>
Описание:
<b>Возвращаемое значение</b>: value of CGI parameter &filter-by-model-rating<br/>https://st.yandex-team.ru/MARKETOUT-43055<br/>
Пример использования:
```example: &filter-by-model-rating=[SOME_VALUE]...```<br/><b>[..."filter-by-model-rating=true"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_advertising_carousel.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L258)</b><br>

---

#### Cgi: <b>[filter-by-promo-id](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1372)</b>
Описание:
<b>Возвращаемое значение</b>: value of CGI parameter filter-by-promo-id<br/>
Пример использования:
```example: &filter-by-promo-id=[SOME_VALUE]...```<br/><b>[..."filter-by-promo-id=xMpQQQC5I4INzFCab3WEmw"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_promo_v3.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L676)</b><br><b>[..."filter-by-promo-id=xMpQQQC5I4INzFCab3WEmw"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_promo_v3.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L700)</b><br>

---

#### Cgi: <b>[filter-currency](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L362)</b>
Описание:
<b>Возвращаемое значение</b>: value of &filter-currency=... CGI-parameter (used together with mcpricefrom/mcpriceto)<br/>
Пример использования:
```example: &filter-currency=[SOME_VALUE]...```<br/><b>[..."filter-currency=UE"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_prime_non_gl_filters.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L339)</b><br><b>[..."filter-currency=RUB"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_prime_non_gl_filters.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L346)</b><br><b>[..."filter-currency=UE"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_prime_non_gl_filters.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L358)</b><br>

---

#### Cgi: <b>[filter-delivery-perks-eligible](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1769)</b>
Описание:
<b>Возвращаемое значение</b>: CGI-value &filter-delivery-perks-eligible<br/>
Пример использования:
```example: &filter-delivery-perks-eligible=[SOME_VALUE]...```<br/><b>[..."filter-delivery-perks-eligible=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_filter_delivery_perks_eligible.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L331)</b><br>

---

#### Cgi: <b>[filter-delivery-type](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L245)</b>
Описание:
 possible values:<br/> 'any'     - filters by any kind of delivery<br/> 'pickup'  - filters by including pickup delivery<br/> 'courier' - filters by including courier delivery<br/>https://st.yandex-team.ru/MARKETOUT-38509<br/>
Пример использования:
```example: &filter-delivery-type=[SOME_VALUE]...```<br/><b>[..."filter-delivery-type=any"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_filter_offer_type_delivery_type.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L621)</b><br><b>[..."filter-delivery-type=pickup"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_filter_offer_type_delivery_type.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L643)</b><br><b>[..."filter-delivery-type=courier"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_filter_offer_type_delivery_type.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L673)</b><br>

---

#### Cgi: <b>[filter-discount-only](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L950)</b>
Описание:
 Filter out all offers without discount (see MARKETOUT-7822).<br/><b>Возвращаемое значение</b>: CGI-value &filter-discount-only<br/>
Пример использования:
```example: &filter-discount-only=[SOME_VALUE]...```<br/><b>[..."filter-discount-only=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_personal_offers.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L550)</b><br><b>[..."filter-discount-only=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_personal_offers.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L566)</b><br><b>[..."filter-discount-only=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_popular_products.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1048)</b><br>

---

#### Cgi: <b>[filter-express-delivery-today](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L220)</b>
Описание:

Пример использования:
```example: &filter-express-delivery-today=[SOME_VALUE]...```<br/><b>[..."filter-express-delivery-today=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_express_delivery.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2529)</b><br><b>[..."filter-express-delivery-today=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_express_delivery.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2564)</b><br><b>[..."filter-express-delivery-today=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_express_delivery.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2582)</b><br>

---

#### Cgi: <b>[filter-express-delivery](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L217)</b>
Описание:

Пример использования:
```example: &filter-express-delivery=[SOME_VALUE]...```<br/><b>[..."filter-express-delivery=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_eats_hyperlocality.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L239)</b><br><b>[..."filter-express-delivery=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_business_offer.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1392)</b><br><b>[..."filter-express-delivery="...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_filter_offer_type_delivery_type.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L342)</b><br>

---

#### Cgi: <b>[filter-goods-of-the-week](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1403)</b>
Описание:
 @legacy:<br/>
Пример использования:
```example: &filter-goods-of-the-week=[SOME_VALUE]...```<br/><b>[..."filter-goods-of-the-week=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_productoffers.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L3455)</b><br>

---

#### Cgi: <b>[filter-jumptable-params-in-specs](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2838)</b>
Описание:
<b>Возвращаемое значение</b>: cgi: "filter-jumptable-params-in-specs"<br/>https://st.yandex-team.ru/MARKETPROJECT-7530<br/>
Пример использования:
```example: &filter-jumptable-params-in-specs=[SOME_VALUE]...```<br/><b>[..."filter-jumptable-params-in-specs=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_modelinfo_sku.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1201)</b><br><b>[..."filter-jumptable-params-in-specs=0"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_modelinfo_sku.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1253)</b><br>

---

#### Cgi: <b>[filter-links](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L769)</b>
Описание:
<b>Возвращаемое значение</b>: value of CGI parameter &filter-links<br/>https://st.yandex-team.ru/MARKETOUT-43974<br/>
Пример использования:
```example: &filter-links=[SOME_VALUE]...```<br/><b>[..."filter-links="...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_entity_links.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L238)</b><br><b>[..."filter-links="...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_entity_links.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L273)</b><br><b>[..."filter-links="...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_entity_links.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L310)</b><br>

---

#### Cgi: <b>[filter-medical-analogs](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2762)</b>
Описание:
 To get right response you need to specify "vendor_id"<br/>https://st.yandex-team.ru/MARKETOUT-40097<br/>
Пример использования:
```example: &filter-medical-analogs=[SOME_VALUE]...```<br/><b>[..."filter-medical-analogs="...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_filter_medical_analogs.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L404)</b><br><b>[..."filter-medical-analogs="...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_filter_medical_analogs.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L420)</b><br><b>[..."filter-medical-analogs="...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_filter_medical_analogs.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L451)</b><br>

---

#### Cgi: <b>[filter-medical-booking](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2769)</b>
Описание:
 Filter offers by "medical-booking" search-literal<br/> Medical partners who can make ready-to-ship in 15 minutes<br/>https://st.yandex-team.ru/MARKETOUT-45032<br/>https://st.yandex-team.ru/MARKETOUT-45070<br/>
Пример использования:
```example: &filter-medical-booking=[SOME_VALUE]...```<br/><b>[..."filter-medical-booking=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_combine_shopping_list.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2292)</b><br><b>[..."filter-medical-booking=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_combine_shopping_list.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2608)</b><br>

---

#### Cgi: <b>[filter-models](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1995)</b>
Описание:
 Filter out offers and models with hyperid from filter<br/><b>Заметка</b>: can not be negative<br/>
Пример использования:
```example: &filter-models=[SOME_VALUE]...```<br/><b>[..."filter-models=102"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_filter_docs.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L75)</b><br><b>[..."filter-models=101"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_filter_docs.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L88)</b><br><b>[..."filter-models=101"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_filter_docs.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L101)</b><br>

---

#### Cgi: <b>[filter-offer-type](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L237)</b>
Описание:
 possible values:<br/> 'medicine' - filters by medicine<br/> 'lavka'<br/> 'eda_retail'<br/> 'eda_restaurants'<br/> 'without_express'<br/>https://st.yandex-team.ru/MARKETOUT-38509<br/>
Пример использования:
```example: &filter-offer-type=[SOME_VALUE]...```<br/><b>[..."filter-offer-type="...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_lavka.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L375)</b><br><b>[..."filter-offer-type=medicine"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_filter_offer_type_delivery_type.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L593)</b><br><b>[..."filter-offer-type=medicine"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_filter_offer_type_delivery_type.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L745)</b><br>

---

#### Cgi: <b>[filter-promo-or-discount](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1384)</b>
Описание:
https://st.yandex-team.ru/MARKETOUT-14686<br/><b>Возвращаемое значение</b>: the existence of CGI parameter value "&filter-promo-or-discount"<br/>
Пример использования:
```example: &filter-promo-or-discount=[SOME_VALUE]...```<br/><b>[..."filter-promo-or-discount=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_model_modifications.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L534)</b><br><b>[..."filter-promo-or-discount=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_recipes.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L305)</b><br><b>[..."filter-promo-or-discount=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_recipes.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L317)</b><br>

---

#### Cgi: <b>[filter-smb](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2339)</b>
Описание:
<b>Возвращаемое значение</b>: value of CGI-parameter &filter-smb<br/>https://st.yandex-team.ru/MARKETOUT-30470<br/>
Пример использования:
```example: &filter-smb=[SOME_VALUE]...```<br/><b>[..."filter-smb=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_smb.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L108)</b><br>

---

#### Cgi: <b>[filter-vendor-recommended](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1159)</b>
Описание:
 Filter offers by offers recommended shop flag<br/><b>Возвращаемое значение</b>: CGI-value &filter-vendor-recommended<br/>
Пример использования:
```example: &filter-vendor-recommended=[SOME_VALUE]...```<br/>

---

#### Cgi: <b>[filter-warnings](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1399)</b>
Описание:
https://st.yandex-team.ru/MARKETOUT-18461<br/><b>Возвращаемое значение</b>: warnings which should be filtered out<br/>
Пример использования:
```example: &filter-warnings=[SOME_VALUE]...```<br/><b>[..."filter-warnings=medicine2"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_restriction.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L914)</b><br><b>[..."filter-warnings=supplement"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_restriction.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L920)</b><br><b>[..."filter-warnings=other"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_restriction.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L926)</b><br>

---

#### Cgi: <b>[filter-with-picture](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1408)</b>
Описание:
https://st.yandex-team.ru/MARKETOUT-17422<br/><b>Возвращаемое значение</b>: the existence of CGI parameter value "&filter-with-picture"<br/>
Пример использования:
```example: &filter-with-picture=[SOME_VALUE]...```<br/><b>[..."filter-with-picture=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_picture_filtering.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L86)</b><br>

---

#### Cgi: <b>[filterList](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L764)</b>
Описание:
<b>Возвращаемое значение</b>: value of CGI parameter &filterList<br/>https://st.yandex-team.ru/MARKETOUT-7879<br/>
Пример использования:
```example: &filterList=[SOME_VALUE]...```<br/><b>[..."filterList=all"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_nid_multihid.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L891)</b><br><b>[..."filterList=all"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_nid_multihid.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L895)</b><br><b>[..."filterList=all"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_nid_multihid.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1039)</b><br>

---

#### Cgi: <b>[filters-key](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2285)</b>
Описание:
<b>Возвращаемое значение</b>: value of CGI-parameter &filters-key<br/>https://st.yandex-team.ru/MARKETOUT-31655<br/>https://st.yandex-team.ru/MARKETOUT-42206, actual_delivery for outlets filters<br/>
Пример использования:
```example: &filters-key=[SOME_VALUE]...```<br/><b>[..."filters-key=7893318"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_popular_glfilters.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L26)</b><br><b>[..."filters-key=7893318"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_popular_glfilters.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L32)</b><br><b>[..."filters-key=7893318"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_popular_glfilters.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L35)</b><br>

---

#### Cgi: <b>[filters-preset-id](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2909)</b>
Описание:
<b>Возвращаемое значение</b>: Selected filters preset<br/>https://st.yandex-team.ru/MARKETOUT-46298<br/>
Пример использования:
```example: &filters-preset-id=[SOME_VALUE]...```<br/><b>[..."filters-preset-id=42"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_filters_presets.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L425)</b><br><b>[..."filters-preset-id=42"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_filters_presets.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L427)</b><br><b>[..."filters-preset-id=42"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_filters_presets.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L429)</b><br>

---

#### Cgi: <b>[foodtech-cgi](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2753)</b>
Описание:
https://st.yandex-team.ru/ECOMSERP-92<br/>
Пример использования:
```example: &foodtech-cgi=[SOME_VALUE]...```<br/><b>[..."foodtech-cgi=text%3Dлавка"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_lavka.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L330)</b><br>

---

#### Cgi: <b>[force-delivery-id](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2464)</b>
Описание:
 Delivery service id that has to be used for the order.<br/><b>Возвращаемое значение</b>: value of CGI-parameter &force-delivery-id<br/>
Пример использования:
```example: &force-delivery-id=[SOME_VALUE]...```<br/><b>[..."force-delivery-id="...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_actual_delivery_combinator.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2282)</b><br><b>[..."force-delivery-id="...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_delivery_route.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2433)</b><br>

---

#### Cgi: <b>[force-gl-filters](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2350)</b>
Описание:
<b>Возвращаемое значение</b>: value of CGI-parameter &force-gl-filters<br/> Do not ignore glfilters in any cases<br/>https://st.yandex-team.ru/MARKETOUT-30646<br/>
Пример использования:
```example: &force-gl-filters=[SOME_VALUE]...```<br/><b>[..."force-gl-filters="...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_productoffers.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L3356)</b><br><b>[..."force-gl-filters=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_productoffers.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L3361)</b><br>

---

#### Cgi: <b>[force-promo-offer-search](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L995)</b>
Описание:
https://st.yandex-team.ru/MARKETOUT-19092<br/> Force to search dicount and promos in offers only<br/><b>Возвращаемое значение</b>: CGI-value @force-promo-offer-search<br/>
Пример использования:
```example: &force-promo-offer-search=[SOME_VALUE]...```<br/><b>[..."force-promo-offer-search=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_promo_type_filter.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L762)</b><br><b>[..."force-promo-offer-search=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_promo_type_filter.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L770)</b><br>

---

#### Cgi: <b>[force-relevance-promo](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1923)</b>
Описание:
 move cms promo offers on first place<br/>https://st.yandex-team.ru/MARKETOUT-21867<br/>
Пример использования:
```example: &force-relevance-promo=[SOME_VALUE]...```<br/><b>[..."force-relevance-promo="...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_cms_promo.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L176)</b><br>

---

#### Cgi: <b>[force-show-offers-without-hyper](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1838)</b>
Описание:
<b>Возвращаемое значение</b>: value of CGI parameter &force-show-offers-without-hyper<br/>https://st.yandex-team.ru/MARKETOUT-18613<br/>
Пример использования:
```example: &force-show-offers-without-hyper=[SOME_VALUE]...```<br/><b>[..."force-show-offers-without-hyper=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_show_offers.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L132)</b><br><b>[..."force-show-offers-without-hyper=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_show_offers.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L135)</b><br><b>[..."force-show-offers-without-hyper=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_show_offers.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L213)</b><br>

---

#### Cgi: <b>[force-use-delivery-calc](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1810)</b>
Описание:
<b>Возвращаемое значение</b>: value of CGI parameter &force-use-delivery-calc<br/> Always use request to delivery calculator on place actual_delivery<br/>
Пример использования:
```example: &force-use-delivery-calc=[SOME_VALUE]...```<br/><b>[..."force-use-delivery-calc=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_actual_delivery_saashub.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L269)</b><br><b>[..."force-use-delivery-calc=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_actual_delivery_saashub.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L301)</b><br><b>[..."force-use-delivery-calc=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_actual_delivery_beru_post_terminals.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L364)</b><br>

---

#### Cgi: <b>[force-white-offer-options](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1833)</b>
Описание:
<b>Возвращаемое значение</b>: value of CGI parameter &force-white-offer-options<br/>https://st.yandex-team.ru/MARKETOUT-39002<br/>
Пример использования:
```example: &force-white-offer-options=[SOME_VALUE]...```<br/><b>[..."force-white-offer-options=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_actual_delivery_unified_tariffs.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L364)</b><br><b>[..."force-white-offer-options=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_actual_delivery_unified_tariffs.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L427)</b><br><b>[..."force-white-offer-options=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_actual_delivery_unified_tariffs.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L496)</b><br>

---

#### Cgi: <b>[franchise](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1604)</b>
Описание:

Пример использования:
```example: &franchise=[SOME_VALUE]...```<br/><b>[..."franchise=3"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_brand_products.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1610)</b><br>

---

#### Cgi: <b>[free-delivery-or-pickup](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L891)</b>
Описание:
 Return only offers with free delivery<br/><b>Возвращаемое значение</b>: value of CGI-parameter &free-delivery-or-pickup<br/>
Пример использования:
```example: &free-delivery-or-pickup=[SOME_VALUE]...```<br/>

---

#### Cgi: <b>[free_delivery](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L886)</b>
Описание:
 Return only offers with free delivery<br/><b>Возвращаемое значение</b>: value of CGI-parameter &free_delivery | free-delivery<br/>
Пример использования:
```example: &free_delivery=[SOME_VALUE]...```<br/><b>[..."free_delivery=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_geo.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L42)</b><br><b>[..."free_delivery=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_productoffers_filters.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L33)</b><br><b>[..."free_delivery=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_buybox_with_dsbs.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L59)</b><br>

---

#### Cgi: <b>[fulfillment-offers-only](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L415)</b>
Описание:
 Отображение только тех офферов, которые мы исполняем сами (товары с нашего склада)<br/> Актуально для красного и синего<br/>
Пример использования:
```example: &fulfillment-offers-only=[SOME_VALUE]...```<br/><b>[..."fulfillment-offers-only=da"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_blue_market.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L4870)</b><br>

---

#### Cgi: <b>[gaid](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1891)</b>
Описание:
<b>Возвращаемое значение</b>: value of CGI parameter &gaid<br/>https://st.yandex-team.ru/MARKETOUT-18941<br/>
Пример использования:
```example: &gaid=[SOME_VALUE]...```<br/><b>[..."gaid=23"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_dj.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1248)</b><br><b>[..."gaid=456"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_dj.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2164)</b><br><b>[..."gaid="...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_dj.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2403)</b><br>

---

#### Cgi: <b>[geo-attraction-distance](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L268)</b>
Описание:
 Зона притяжения к точкам на карте (см. AttractionPoints).<br/>
Пример использования:
```example: &geo-attraction-distance=[SOME_VALUE]...```<br/><b>[..."geo-attraction-distance=7000"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_geo.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2326)</b><br><b>[..."geo-attraction-distance=7000"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_outlet_delivery.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L3179)</b><br><b>[..."geo-attraction-distance=7000"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_outlet_delivery.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L3185)</b><br>

---

#### Cgi: <b>[geo-attraction](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L264)</b>
Описание:
 Точки притяжения на карте.<br/> Оутлеты, которые расположены близко к точкам выдачи будут иметь приоритет перед остальными.<br/> Порядок добавления точек важен - приоритет у первой точки.<br/> Точки добавляются в конец списка после стандартных точек, предусмотренных в place<br/>
Пример использования:
```example: &geo-attraction=[SOME_VALUE]...```<br/><b>[..."geo-attraction="...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_geo.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2371)</b><br><b>[..."geo-attraction="...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_geo.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2372)</b><br>

---

#### Cgi: <b>[geo-location](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L254)</b>
Описание:

Пример использования:
```example: &geo-location=[SOME_VALUE]...```<br/><b>[..."geo-location=37.15"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_cpa_category_geo.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L169)</b><br><b>[..."geo-location=37.15"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_cpa_category_geo.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L205)</b><br><b>[..."geo-location=37.15"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_cpa_category_geo.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L248)</b><br>

---

#### Cgi: <b>[geo-sort-gran](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1102)</b>
Описание:
 Max outlets from one shop on a single geo results iteration round<br/><b>Возвращаемое значение</b>: value of CGI-parameter &geo-sort-gran<br/>
Пример использования:
```example: &geo-sort-gran=[SOME_VALUE]...```<br/><b>[..."geo-sort-gran=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_geo.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L911)</b><br><b>[..."geo-sort-gran=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_geo.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L924)</b><br><b>[..."geo-sort-gran=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_geo.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L936)</b><br>

---

#### Cgi: <b>[geo](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L710)</b>
Описание:
 Defines geo mode<br/><b>Возвращаемое значение</b>: CGI-parameter &geo<br/>
Пример использования:
```example: &geo=[SOME_VALUE]...```<br/><b>[..."geo=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_geo.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1563)</b><br><b>[..."geo=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_geo.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1661)</b><br><b>[..."geo=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_geo.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1666)</b><br>

---

#### Cgi: <b>[geo_bounds_lb, geo_bounds_rt](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L257)</b>
Описание:

Пример использования:
```example: &geo_bounds_lb=[SOME_VALUE]...```<br/><b>[..."geo_bounds_lb=37.0"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_credit.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1212)</b><br><b>[..."geo_bounds_lb=37.2"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_cpa_category_geo.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L169)</b><br><b>[..."geo_bounds_lb=37.4"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_cpa_category_geo.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L205)</b><br>```example: &geo_bounds_rt=[SOME_VALUE]...```<br/><b>[..."geo_bounds_rt=37.3"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_credit.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1212)</b><br><b>[..."geo_bounds_rt=37.4"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_cpa_category_geo.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L169)</b><br><b>[..."geo_bounds_rt=37.6"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_cpa_category_geo.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L205)</b><br>

---

#### Cgi: <b>[get-category-path](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1490)</b>
Описание:
 Get all document categories<br/>https://st.yandex-team.ru/MARKETOUT-38237<br/><b>Возвращаемое значение</b>: value of CGI parameter "&get-category-path"<br/>
Пример использования:
```example: &get-category-path=[SOME_VALUE]...```<br/><b>[..."get-category-path=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_categories_path.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L44)</b><br><b>[..."get-category-path=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_categories_path.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L64)</b><br><b>[..."get-category-path=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_categories_path.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L88)</b><br>

---

#### Cgi: <b>[get-category-pictures](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1484)</b>
Описание:
 Enable category picture lookup<br/>https://st.yandex-team.ru/MARKETOUT-12914<br/><b>Возвращаемое значение</b>: value of CGI parameter "&get-category-pictures"<br/>
Пример использования:
```example: &get-category-pictures=[SOME_VALUE]...```<br/><b>[..."get-category-pictures=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_personal_categories.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L24)</b><br>

---

#### Cgi: <b>[glfilter](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L936)</b>
Описание:
<b>Возвращаемое значение</b>: values of CGI-parameter &glfilter without category context<br/>
Пример использования:
```example: &glfilter=[SOME_VALUE]...```<br/><b>[..."glfilter=213"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_top_glfilter_values.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L748)</b><br><b>[..."glfilter=213"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_top_glfilter_values.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L749)</b><br><b>[..."glfilter=933"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_nid_multihid.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L489)</b><br>

---

#### Cgi: <b>[glfilter](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L940)</b>
Описание:
<b>Возвращаемое значение</b>: values of CGI-parameter &glfilter<br/>
Пример использования:
```example: &glfilter=[SOME_VALUE]...```<br/><b>[..."glfilter=213"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_top_glfilter_values.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L748)</b><br><b>[..."glfilter=213"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_top_glfilter_values.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L749)</b><br><b>[..."glfilter=933"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_nid_multihid.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L489)</b><br>

---

#### Cgi: <b>[glfilters-order](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2778)</b>
Описание:
 SERP filters order<br/>https://st.yandex-team.ru/MARKETOUT-40946<br/>
Пример использования:
```example: &glfilters-order=[SOME_VALUE]...```<br/><b>[..."glfilters-order=checked_first"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_glparams_order.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L51)</b><br><b>[..."glfilters-order=cpa"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_glparams_order.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L61)</b><br><b>[..."glfilters-order=cpa"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_glparams_order.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L67)</b><br>

---

#### Cgi: <b>[good-state](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L119)</b>
Описание:
 "new" or "cutprice"<br/>
Пример использования:
```example: &good-state=[SOME_VALUE]...```<br/><b>[..."good-state=cutprice"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_productoffers_pp.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L105)</b><br><b>[..."good-state=cutprice"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_productoffers_pp.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L111)</b><br><b>[..."good-state=cutprice"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_productoffers_premium.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L383)</b><br>

---

#### Cgi: <b>[gps](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2662)</b>
Описание:
 GPS-coordinates of a user<br/> Used to calculate on-demand delivery options upon requests to:<br/> - place=actual_delivery<br/> - place=delivery_route<br/>https://st.yandex-team.ru/MARKETOUT-36093<br/><b>Возвращаемое значение</b>: value of CGI parameter "&gps"<br/>
Пример использования:
```example: &gps=[SOME_VALUE]...```<br/><b>[..."gps=lat"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_deferred_courier_delivery.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L159)</b><br><b>[..."gps=lat"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_flat_courier_options.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L82)</b><br><b>[..."gps=lat"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_on_demand_delivery.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L270)</b><br>

---

#### Cgi: <b>[grcutprice](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L684)</b>
Описание:
<b>Возвращаемое значение</b>: value of CGI-parameter grcutprice<br/> Used for cutprice top6 for experiment<br/>
Пример использования:
```example: &grcutprice=[SOME_VALUE]...```<br/>

---

#### Cgi: <b>[grhow](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L679)</b>
Описание:
<b>Возвращаемое значение</b>: value of CGI-parameter grhow<br/> Used by function calculateGrouping in MarketServant constructor<br/> to generate enum GroupBy value<br/> Added in https://st.yandex-team.ru/MARKETOUT-5709<br/>
Пример использования:
```example: &grhow=[SOME_VALUE]...```<br/><b>[..."grhow=shop"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_model_wizard_by_id.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L156)</b><br><b>[..."grhow=shop"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_model_wizard_by_id.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L159)</b><br><b>[..."grhow=shop"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_model_wizard_by_id.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L180)</b><br>

---

#### Cgi: <b>[groupid](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L302)</b>
Описание:

Пример использования:
```example: &groupid=[SOME_VALUE]...```<br/>

---

#### Cgi: <b>[has-installments](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L227)</b>
Описание:
 В with-installments можно выбрать конкретно bnpl рассрочку, а тут нет<br/>
Пример использования:
```example: &has-installments=[SOME_VALUE]...```<br/>

---

#### Cgi: <b>[has-promo](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L156)</b>
Описание:
 default value is false<br/> @sildtm todo wtf ?<br/>
Пример использования:
```example: &has-promo=[SOME_VALUE]...```<br/><b>[..."has-promo=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_promo_personalization.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L134)</b><br><b>[..."has-promo=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_offer_collapsing.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1234)</b><br><b>[..."has-promo=0"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_promo_v3.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L693)</b><br>

---

#### Cgi: <b>[has_cpa_offers](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2121)</b>
Описание:
<b>Возвращаемое значение</b>: value of CGI-parameter &has_cpa_offers used in TPlaceBrandProducts place<br/>https://st.yandex-team.ru/MARKETOUT-35811<br/>
Пример использования:
```example: &has_cpa_offers=[SOME_VALUE]...```<br/>

---

#### Cgi: <b>[hid-by-market-sku](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L518)</b>
Описание:

Пример использования:
```example: &hid-by-market-sku=[SOME_VALUE]...```<br/><b>[..."hid-by-market-sku=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_msku_transitions.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L260)</b><br><b>[..."hid-by-market-sku=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_msku_transitions.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L293)</b><br><b>[..."hid-by-market-sku=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_msku_transitions.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L313)</b><br>

---

#### Cgi: <b>[hid](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L510)</b>
Описание:
 Category identifier<br/><b>Заметка</b>: CGI-parameter hid contains comma-separated category ID values<br/><b>Исключение</b>: std::exception if hid is not a non-negative number or equals to 90401 (all categories)<br/><b>Возвращаемое значение</b>: value of CGI-parameter &hid<br/>
Пример использования:
```example: &hid=[SOME_VALUE]...```<br/><b>[..."hid=2"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_articles.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L174)</b><br><b>[..."hid=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_blue_psku.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L127)</b><br><b>[..."hid=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_blue_psku.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L230)</b><br>

---

#### Cgi: <b>[hid](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L525)</b>
Описание:
 Raw category identifier from request, no filtration logic applied<br/><b>Заметка</b>: CGI-parameter hid contains comma-separated category ID values<br/><b>Исключение</b>: std::exception if hid is not a non-negative number or equals to 90401 (all categories)<br/><b>Возвращаемое значение</b>: value of CGI-parameter &hid<br/>
Пример использования:
```example: &hid=[SOME_VALUE]...```<br/><b>[..."hid=2"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_articles.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L174)</b><br><b>[..."hid=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_blue_psku.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L127)</b><br><b>[..."hid=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_blue_psku.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L230)</b><br>

---

#### Cgi: <b>[hid](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L532)</b>
Описание:
 Category filter<br/><b>Заметка</b>: CGI-parameter hid contains comma-separated category ID values with optional '-' sign<br/><b>Исключение</b>: std::exception if hid equals to 90401 (all categories)<br/><b>Возвращаемое значение</b>: list of values with negation flag<br/>
Пример использования:
```example: &hid=[SOME_VALUE]...```<br/><b>[..."hid=2"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_articles.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L174)</b><br><b>[..."hid=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_blue_psku.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L127)</b><br><b>[..."hid=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_blue_psku.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L230)</b><br>

---

#### Cgi: <b>[hid_by_hyper_id](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L515)</b>
Описание:
 The mode of getting Hid from the model by HyperId<br/><b>Возвращаемое значение</b>: value of CGI-parameter &hid_by_hyper_id<br/>
Пример использования:
```example: &hid_by_hyper_id=[SOME_VALUE]...```<br/><b>[..."hid_by_hyper_id=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_gl_request_params.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L581)</b><br><b>[..."hid_by_hyper_id=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_productoffers.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L5742)</b><br><b>[..."hid_by_hyper_id=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_productoffers.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L5754)</b><br>

---

#### Cgi: <b>[hide-filter](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1531)</b>
Описание:
<b>Возвращаемое значение</b>: value of CGI parameter &hide-filter<br/>https://st.yandex-team.ru/MARKETOUT-13851<br/>
Пример использования:
```example: &hide-filter=[SOME_VALUE]...```<br/><b>[..."hide-filter=fastest-delivery-12"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_delivery_interval.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1439)</b><br><b>[..."hide-filter=fastest-delivery-0"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_delivery_interval.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1440)</b><br><b>[..."hide-filter=fastest-delivery-1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_delivery_interval.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1441)</b><br>

---

#### Cgi: <b>[hide-global-cpa](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1154)</b>
Описание:
 Do not show global CPA offers.<br/>https://st.yandex-team.ru/MARKETOUT-10862<br/><b>Возвращаемое значение</b>: value of CGI-parameter "&hide-global-cpa"<br/>
Пример использования:
```example: &hide-global-cpa=[SOME_VALUE]...```<br/><b>[..."hide-global-cpa=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_is_global_shop.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L190)</b><br>

---

#### Cgi: <b>[hide-msku-without-offers](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2046)</b>
Описание:
<b>Возвращаемое значение</b>: value of CGI-parameter &hide-msku-without-offers<br/>https://st.yandex-team.ru/MARKETOUT-25974<br/>
Пример использования:
```example: &hide-msku-without-offers=[SOME_VALUE]...```<br/><b>[..."hide-msku-without-offers=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_blue_market.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L5235)</b><br>

---

#### Cgi: <b>[hide-offer-promo](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1290)</b>
Описание:
 Don't show promo block in offer output<br/> Used in place=prime<br/>https://st.yandex-team.ru/MARKETOUT-24159<br/>
Пример использования:
```example: &hide-offer-promo=[SOME_VALUE]...```<br/><b>[..."hide-offer-promo=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_prime_hide_promo.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L72)</b><br><b>[..."hide-offer-promo=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_prime_hide_promo.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L93)</b><br>

---

#### Cgi: <b>[hide-offers-without-cpc-link](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1468)</b>
Описание:
https://st.yandex-team.ru/MARKETOUT-13207<br/> Parameter that forces hiding offers without CPC link<br/> default: false<br/>
Пример использования:
```example: &hide-offers-without-cpc-link=[SOME_VALUE]...```<br/><b>[..."hide-offers-without-cpc-link="...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_hide_cpc_links.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L126)</b><br><b>[..."hide-offers-without-cpc-link=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_hide_cpc_links.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L129)</b><br><b>[..."hide-offers-without-cpc-link="...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_hide_cpc_links.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L142)</b><br>

---

#### Cgi: <b>[hide-test-shops](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1472)</b>
Описание:
https://st.yandex-team.ru/MARKETOUT-19019<br/>
Пример использования:
```example: &hide-test-shops=[SOME_VALUE]...```<br/><b>[..."hide-test-shops=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_hide_test_shops.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L39)</b><br><b>[..."hide-test-shops=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_hide_test_shops.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L47)</b><br><b>[..."hide-test-shops=0"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_hide_test_shops.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L55)</b><br>

---

#### Cgi: <b>[hide_plus_subscriptions](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2974)</b>
Описание:
https://st.yandex-team.ru/MARKETOUT-47482<br/><b>Возвращаемое значение</b>: Для прохождения ревью от Apple на платформе IOS необходимо скрыть подписку Плюса, скрываем ее по этому параметру<br/>
Пример использования:
```example: &hide_plus_subscriptions=[SOME_VALUE]...```<br/><b>[..."hide_plus_subscriptions="...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_dsbs_digital.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L115)</b><br><b>[..."hide_plus_subscriptions="...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_promo_type_filter.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L838)</b><br>

---

#### Cgi: <b>[hideduplicate](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1038)</b>
Описание:
 Hides duplicate offers<br/><b>Возвращаемое значение</b>: CGI-value &hideduplicate<br/>
Пример использования:
```example: &hideduplicate=[SOME_VALUE]...```<br/><b>[..."hideduplicate=0"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_prime.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1590)</b><br>

---

#### Cgi: <b>[hideglfilters](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L759)</b>
Описание:
<b>Возвращаемое значение</b>: value of CGI parameter &hideglfilters<br/>https://st.yandex-team.ru/MARKETOUT-42352<br/>
Пример использования:
```example: &hideglfilters=[SOME_VALUE]...```<br/><b>[..."hideglfilters=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_productoffers_filters.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2388)</b><br><b>[..."hideglfilters=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_glparams.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L654)</b><br>

---

#### Cgi: <b>[hidenonglfilters](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L754)</b>
Описание:
<b>Возвращаемое значение</b>: value of CGI parameter &hidenonglfilters<br/>https://st.yandex-team.ru/MARKETOUT-12717<br/>
Пример использования:
```example: &hidenonglfilters=[SOME_VALUE]...```<br/><b>[..."hidenonglfilters=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_productoffers_filters.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2354)</b><br>

---

#### Cgi: <b>[high-price-problem](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2514)</b>
Описание:
https://st.yandex-team.ru/MARKETOUT-33381<br/><b>Возвращаемое значение</b>: value of CGI parameter "&high-price-problem"<br/>
Пример использования:
```example: &high-price-problem=[SOME_VALUE]...```<br/><b>[..."high-price-problem=2"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_supplier_high_prices.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L160)</b><br><b>[..."high-price-problem=2"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_supplier_high_prices.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L164)</b><br><b>[..."high-price-problem=2"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_supplier_high_prices.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L207)</b><br>

---

#### Cgi: <b>[history](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2096)</b>
Описание:
<b>Возвращаемое значение</b>: value of CGI-parameter &history<br/>https://st.yandex-team.ru/MARKETRECOM-1848<br/>
Пример использования:
```example: &history=[SOME_VALUE]...```<br/><b>[..."history=blue"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_products_by_history_blue.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L103)</b><br><b>[..."history=blue"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_products_by_history_blue.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L152)</b><br><b>[..."history=blue"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_products_by_history_blue.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L208)</b><br>

---

#### Cgi: <b>[home-rids](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L786)</b>
Описание:
 Region where client is located (calculated by IP or settings)<br/><b>Заметка</b>: Differs from region where user wants to search for offers (&rids)<br/><b>Заметка</b>: Parameter home-rids can be used to determine client timezone, for example<br/><b>Возвращаемое значение</b>: CGI-parameter &home-rids<br/>
Пример использования:
```example: &home-rids=[SOME_VALUE]...```<br/><b>[..."home-rids=213"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_outlet_delivery.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1209)</b><br><b>[..."home-rids=54"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_outlet_delivery.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1223)</b><br><b>[..."home-rids=22"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_outlet_delivery.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1237)</b><br>

---

#### Cgi: <b>[home_region](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L588)</b>
Описание:
 Filter offers by shop home region<br/><b>Возвращаемое значение</b>: value of CGI-parameter home_region: "205,225,..."<br/>
Пример использования:
```example: &home_region=[SOME_VALUE]...```<br/>

---

#### Cgi: <b>[how-hot](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2116)</b>
Описание:
<b>Возвращаемое значение</b>: threshold in percent answering the question 'How much better than MinRefPrice?'<br/>https://st.yandex-team.ru/MARKETOUT-28136<br/>
Пример использования:
```example: &how-hot=[SOME_VALUE]...```<br/><b>[..."how-hot=26"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_hot_offers.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L321)</b><br>

---

#### Cgi: <b>[how](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L563)</b>
Описание:
<b>Возвращаемое значение</b>: &how= parameter. CGI-parameter<br/><b>Заметка</b>: how to sort the results: aprice, dprice ... etc<br/>
Пример использования:
```example: &how=[SOME_VALUE]...```<br/><b>[..."how=aprice"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_missing_data_files.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L74)</b><br><b>[..."how=guru_popularity"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_model_modifications.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L181)</b><br><b>[..."how=aprice"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_model_modifications.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L194)</b><br>

---

#### Cgi: <b>[hr](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1043)</b>
Описание:
 human-readable output for proto places<br/><b>Возвращаемое значение</b>: CGI-value &hr<br/>
Пример использования:
```example: &hr=[SOME_VALUE]...```<br/><b>[..."hr=json"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_parallel.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L734)</b><br><b>[..."hr=json"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_parallel_products.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L739)</b><br>

---

#### Cgi: <b>[htmldesc](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1214)</b>
Описание:
 When not set, strip out html tags from short description, default false<br/>https://st.yandex-team.ru/MARKETOUT-9946<br/><b>Возвращаемое значение</b>: value of CGI-parameter "&htmldesc="<br/>
Пример использования:
```example: &htmldesc=[SOME_VALUE]...```<br/>

---

#### Cgi: <b>[hyperid](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L111)</b>
Описание:
 Model IDs for microcard, modelwizardoffers<br/><b>Заметка</b> can not be negative<br/><b>Устаревший параметр</b> use modelid in combination with entities if necessary<br/>
Пример использования:
```example: &hyperid=[SOME_VALUE]...```<br/><b>[..."hyperid=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_accessories.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L135)</b><br><b>[..."hyperid=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_accessories_facets.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L64)</b><br><b>[..."hyperid=2"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_accessories_facets.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L115)</b><br>

---

#### Cgi: <b>[hyperlocal-mode](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2741)</b>
Описание:
https://st.yandex-team.ru/MARKETOUT-43897<br/>
Пример использования:
```example: &hyperlocal-mode=[SOME_VALUE]...```<br/><b>[..."hyperlocal-mode=only_express"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_shop_info.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2745)</b><br><b>[..."hyperlocal-mode=only_express"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_shop_info.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2803)</b><br>

---

#### Cgi: <b>[i2i-folder](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2861)</b>
Описание:
<b>Возвращаемое значение</b>: value of CGI-parameter i2i-folder<br/>https://st.yandex-team.ru/MARKETRECOM-4418<br/>
Пример использования:
```example: &i2i-folder=[SOME_VALUE]...```<br/><b>[..."i2i-folder=games"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_dj.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2743)</b><br>

---

#### Cgi: <b>[i2i-group-key-filter](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2871)</b>
Описание:
<b>Возвращаемое значение</b>: value of CGI-parameter i2i-group-key-filter<br/>https://st.yandex-team.ru/MARKETRECOM-4418<br/>
Пример использования:
```example: &i2i-group-key-filter=[SOME_VALUE]...```<br/><b>[..."i2i-group-key-filter=accessories"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_complementary_product_groups.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L938)</b><br><b>[..."i2i-group-key-filter=complementary_items"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_complementary_product_groups.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L962)</b><br><b>[..."i2i-group-key-filter=accessories_and_complementary_items"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_complementary_product_groups.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L986)</b><br>

---

#### Cgi: <b>[i2i-version](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2866)</b>
Описание:
<b>Возвращаемое значение</b>: value of CGI-parameter i2i-version<br/>https://st.yandex-team.ru/MARKETRECOM-4418<br/>
Пример использования:
```example: &i2i-version=[SOME_VALUE]...```<br/><b>[..."i2i-version=v1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_dj.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2743)</b><br>

---

#### Cgi: <b>[idfa](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1896)</b>
Описание:
<b>Возвращаемое значение</b>: value of CGI parameter &idfa<br/>https://st.yandex-team.ru/MARKETOUT-18941<br/>
Пример использования:
```example: &idfa=[SOME_VALUE]...```<br/><b>[..."idfa=21"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_dj.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1248)</b><br><b>[..."idfa=789"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_dj.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2164)</b><br>

---

#### Cgi: <b>[ignore-has-gone](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1855)</b>
Описание:
 Ignoring offer flag HAS_GONE and show offers hided by indexer<br/> Some statistics or fields can have different values because trivial base search is used<br/>
Пример использования:
```example: &ignore-has-gone=[SOME_VALUE]...```<br/><b>[..."ignore-has-gone=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_new_blue_erf.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L103)</b><br><b>[..."ignore-has-gone=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_ignore_has_gone.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L61)</b><br><b>[..."ignore-has-gone=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_ignore_has_gone.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L117)</b><br>

---

#### Cgi: <b>[ignore-mn](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1636)</b>
Описание:
<b>Возвращаемое значение</b>: value of CGI parameter &ignore-mn<br/>
Пример использования:
```example: &ignore-mn=[SOME_VALUE]...```<br/><b>[..."ignore-mn=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_parallel.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L89)</b><br><b>[..."ignore-mn=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_parallel.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L94)</b><br><b>[..."ignore-mn=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_parallel_products.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L89)</b><br>

---

#### Cgi: <b>[ignore-offers](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1937)</b>
Описание:
https://st.yandex-team.ru/MARKETOUT-23472<br/>
Пример использования:
```example: &ignore-offers=[SOME_VALUE]...```<br/>

---

#### Cgi: <b>[included-in-price](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L251)</b>
Описание:

Пример использования:
```example: &included-in-price=[SOME_VALUE]...```<br/><b>[..."included-in-price=pickup"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_delivery_modifier.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1593)</b><br><b>[..."included-in-price=delivery"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_delivery_modifier.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1595)</b><br><b>[..."included-in-price=pickup"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_delivery_modifier.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1635)</b><br>

---

#### Cgi: <b>[inlet-shipment-day](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1413)</b>
Описание:
<b>Возвращаемое значение</b>: &inlet-shipment-day= parameter.<br/> It is preferable inlet shipment day.<br/>
Пример использования:
```example: &inlet-shipment-day=[SOME_VALUE]...```<br/><b>[..."inlet-shipment-day=0"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_business_calendar.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L336)</b><br><b>[..."inlet-shipment-day=0"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_business_calendar.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L337)</b><br><b>[..."inlet-shipment-day="...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_delivery.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1317)</b><br>

---

#### Cgi: <b>[intents-height](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2243)</b>
Описание:
<b>Возвращаемое значение</b>: value of CGI-parameter &intents-height<br/> Height of intents tree after target nid or hid<br/>https://st.yandex-team.ru/MARKETOUT-45606<br/>
Пример использования:
```example: &intents-height=[SOME_VALUE]...```<br/><b>[..."intents-height="...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_intents.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L233)</b><br><b>[..."intents-height="...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_intents.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L241)</b><br><b>[..."intents-height="...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_intents.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L250)</b><br>

---

#### Cgi: <b>[ip-rids](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L328)</b>
Описание:
<b>Возвращаемое значение</b>: value of &ip-rids CGI-parameter<br/> вообще фронтенд шлёт нам всегда ip-rids=213 для любых регионов за пределами РКУБ<br/>
Пример использования:
```example: &ip-rids=[SOME_VALUE]...```<br/><b>[..."ip-rids=10"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_partner_model_offers.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L440)</b><br><b>[..."ip-rids=10"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_partner_model_offers.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L445)</b><br><b>[..."ip-rids=10"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_partner_model_offers.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L450)</b><br>

---

#### Cgi: <b>[ip](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L638)</b>
Описание:
<b>Возвращаемое значение</b>: value of CGI-parameter ip<br/>
Пример использования:
```example: &ip=[SOME_VALUE]...```<br/><b>[..."ip=127.0.0.1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_apiofferauction.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L42)</b><br><b>[..."ip=127.0.0.1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_articles.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L255)</b><br><b>[..."ip=127.0.0.1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_partner_offer_counts.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L128)</b><br>

---

#### Cgi: <b>[is-global-shop](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1148)</b>
Описание:
 Show global offers and models on top of the list.<br/> Filter out models with no global offers.<br/>https://st.yandex-team.ru/MARKETOUT-10480<br/><b>Возвращаемое значение</b>: value of CGI-parameter "&is-global-shop"<br/>
Пример использования:
```example: &is-global-shop=[SOME_VALUE]...```<br/><b>[..."is-global-shop=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_is_global_shop.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L91)</b><br><b>[..."is-global-shop=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_is_global_shop.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L150)</b><br><b>[..."is-global-shop=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_is_global_shop.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L156)</b><br>

---

#### Cgi: <b>[is-return](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1795)</b>
Описание:
https://st.yandex-team.ru/MARKETOUT-18164<br/>
Пример использования:
```example: &is-return=[SOME_VALUE]...```<br/><b>[..."is-return=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_shop_info.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1018)</b><br><b>[..."is-return=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_shop_info.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1019)</b><br><b>[..."is-return=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_actual_delivery_return.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L565)</b><br>

---

#### Cgi: <b>[is-turbo-app](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2482)</b>
Описание:
<b>Возвращаемое значение</b>: value of &is-turbo-app=<br/> default value: false<br/>https://st.yandex-team.ru/MARKETOUT-33058<br/> additional indication that this is a turbo app<br/>
Пример использования:
```example: &is-turbo-app=[SOME_VALUE]...```<br/><b>[..."is-turbo-app=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_productoffers_pp.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L105)</b><br>

---

#### Cgi: <b>[isbn](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L115)</b>
Описание:
 isbn to search books without pessimization<br/>
Пример использования:
```example: &isbn=[SOME_VALUE]...```<br/><b>[..."isbn=9785699120147"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_filtering_by_relevance.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L708)</b><br><b>[..."isbn=978-5-902719-15-1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_print_doc.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L482)</b><br><b>[..."isbn=9785699120147"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_books_pessimization.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L417)</b><br>

---

#### Cgi: <b>[klp-code](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2924)</b>
Описание:
<b>Возвращаемое значение</b>: common part of klp & SMNN code from ЕСКЛП system, example: if klp code is "21.20.10.221-000010-1-00174-2000000735385", then return "21.20.10.221-000010-1-00174"<br/>https://st.yandex-team.ru/MARKETOUT-45649<br/>
Пример использования:
```example: &klp-code=[SOME_VALUE]...```<br/><b>[..."klp-code="...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_filter_klp_code.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L314)</b><br><b>[..."klp-code="...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_filter_klp_code.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L330)</b><br><b>[..."klp-code="...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_filter_klp_code.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L361)</b><br>

---

#### Cgi: <b>[kubr](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L334)</b>
Описание:
<b>Возвращаемое значение</b>: value of &kubr CGI-parameter<br/>https://st.yandex-team.ru/MARKETOUT-31773<br/> пришёл ли пользователь из КУБР: Казахстан, Украина, Россия, Беларусь<br/>
Пример использования:
```example: &kubr=[SOME_VALUE]...```<br/>

---

#### Cgi: <b>[lang](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2274)</b>
Описание:
<b>Возвращаемое значение</b>: value of CGI-parameter &lang<br/>https://st.yandex-team.ru/MARKETOUT-30421<br/>
Пример использования:
```example: &lang=[SOME_VALUE]...```<br/><b>[..."lang=ru%2Cen%2C*"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_rerequests.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L238)</b><br><b>[..."lang=ru"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_wizards_translation.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L109)</b><br><b>[..."lang=en"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_wizards_translation.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L135)</b><br>

---

#### Cgi: <b>[licensor](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1601)</b>
Описание:
https://st.yandex-team.ru/MARKETOUT-15273:<br/> BVL(Disney) - фильтр по лицензиару, франшизе, персонажу<br/>
Пример использования:
```example: &licensor=[SOME_VALUE]...```<br/><b>[..."licensor=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_brand_products.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1596)</b><br><b>[..."licensor=3"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_brand_products.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1654)</b><br>

---

#### Cgi: <b>[light-consistency-check](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L410)</b>
Описание:

Пример использования:
```example: &light-consistency-check=[SOME_VALUE]...```<br/><b>[..."light-consistency-check=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_consistency_check.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L27)</b><br>

---

#### Cgi: <b>[light-pack](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1242)</b>
Описание:
 only offer IDs in pack<br/><b>Возвращаемое значение</b>: value of CGI-parameter &light-pack<br/>
Пример использования:
```example: &light-pack=[SOME_VALUE]...```<br/><b>[..."light-pack=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_alt_same_shop.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L3228)</b><br>

---

#### Cgi: <b>[list-banks](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1330)</b>
Описание:
 List banks available for currency converting (bank)<br/>https://st.yandex-team.ru/MARKETOUT-11532<br/><b>Возвращаемое значение</b>: value of CGI parameter "&list-banks"<br/>
Пример использования:
```example: &list-banks=[SOME_VALUE]...```<br/><b>[..."list-banks=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_currency_convert.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L68)</b><br><b>[..."list-banks=0"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_currency_convert.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L75)</b><br><b>[..."list-banks=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_currency_convert.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L216)</b><br>

---

#### Cgi: <b>[local-offers-first](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L819)</b>
Описание:
 checkbox Предложения из моего региона<br/> возвращает черту "Доставка из других регионов"<br/>https://st.yandex-team.ru/MARKETOUT-10253<br/><b>Возвращаемое значение</b>: value of CGI-parameter &local-offers-first<br/>
Пример использования:
```example: &local-offers-first=[SOME_VALUE]...```<br/><b>[..."local-offers-first=0"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_boost_express_offers.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L229)</b><br><b>[..."local-offers-first=0"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_model_modifications.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L234)</b><br><b>[..."local-offers-first=0"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_model_wizard.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L893)</b><br>

---

#### Cgi: <b>[local-sources-only](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L774)</b>
Описание:
 Enable search only in local collections<br/><b>Возвращаемое значение</b>: value of CGI-parameter &local-sources-only, default -- false<br/>
Пример использования:
```example: &local-sources-only=[SOME_VALUE]...```<br/>

---

#### Cgi: <b>[logged-in](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2653)</b>
Описание:
 Indicates whether a user is logged in or not<br/> Used to calculate on-demand delivery options upon requests to:<br/> - place=actual_delivery<br/> - place=delivery_route<br/>https://st.yandex-team.ru/MARKETOUT-36093<br/><b>Возвращаемое значение</b>: value of CGI parameter "&logged-in"<br/>
Пример использования:
```example: &logged-in=[SOME_VALUE]...```<br/><b>[..."logged-in=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_deferred_courier_delivery.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L156)</b><br><b>[..."logged-in=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_deferred_courier_delivery.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L166)</b><br><b>[..."logged-in=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_flat_courier_options.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L81)</b><br>

---

#### Cgi: <b>[madv-incut-ids](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2929)</b>
Описание:
<b>Возвращаемое значение</b>: media adv incut ids in SaaS<br/>https://st.yandex-team.ru/MEDIAADV-199<br/>
Пример использования:
```example: &madv-incut-ids=[SOME_VALUE]...```<br/>

---

#### Cgi: <b>[manufacturer_warranty](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L989)</b>
Описание:
 Filter out all offers except having warranty<br/><b>Возвращаемое значение</b>: CGI-value &manufacturer_warranty<br/>
Пример использования:
```example: &manufacturer_warranty=[SOME_VALUE]...```<br/><b>[..."manufacturer_warranty=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_geo.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L42)</b><br><b>[..."manufacturer_warranty=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_geo.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1232)</b><br><b>[..."manufacturer_warranty=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_productoffers_filters.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L33)</b><br>

---

#### Cgi: <b>[market-force-buisiness-id](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2639)</b>
Описание:
<b>Возвращаемое значение</b>: value of CGI-parameter &market-force-buisiness-id<br/>
Пример использования:
```example: &market-force-buisiness-id=[SOME_VALUE]...```<br/>

---

#### Cgi: <b>[market-req-id](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L614)</b>
Описание:
 (For TSUM request tracking) X-Market-Req-ID header value is taken from the CGI-parameter &market-req-id,<br/> if empty -- from the original request header X-Market-Req-ID<br/><b>Возвращаемое значение</b>: the optional header value<br/>
Пример использования:
```example: &market-req-id=[SOME_VALUE]...```<br/><b>[..."market-req-id="...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_personal_categories_blue.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L798)</b><br><b>[..."market-req-id="...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_personal_categories_blue.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L801)</b><br><b>[..."market-req-id="...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_reqwizard.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L175)</b><br>

---

#### Cgi: <b>[market-sku](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1522)</b>
Описание:
 Parameter is used to filter offers by SKU (Stock Keeping Unit).<br/>
Пример использования:
```example: &market-sku=[SOME_VALUE]...```<br/><b>[..."market-sku=2"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_alice.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L57)</b><br><b>[..."market-sku=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_blue_psku.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L167)</b><br><b>[..."market-sku=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_blue_psku.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L209)</b><br>

---

#### Cgi: <b>[market-turbo-requests](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2066)</b>
Описание:
<b>Возвращаемое значение</b>: value of CGI-parameter &market-turbo-requests<br/>https://st.yandex-team.ru/MARKETOUT-26812<br/>
Пример использования:
```example: &market-turbo-requests=[SOME_VALUE]...```<br/>

---

#### Cgi: <b>[market_delivery_offers_only, market-delivery-offers-only](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L419)</b>
Описание:
 Отображение только офферов с нашей доставкой (скрывает dropship-предложения)<br/>
Пример использования:
```example: &market_delivery_offers_only=[SOME_VALUE]...```<br/><b>[..."market_delivery_offers_only=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_blue_market.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L5141)</b><br>```example: &market-delivery-offers-only=[SOME_VALUE]...```<br/><b>[..."market-delivery-offers-only=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_blue_market.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L5141)</b><br>

---

#### Cgi: <b>[market_top_carousel](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2385)</b>
Описание:
https://st.yandex-team.ru/MARKETOUT-39571<br/>
Пример использования:
```example: &market_top_carousel=[SOME_VALUE]...```<br/><b>[..."market_top_carousel=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_wizards.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L13069)</b><br><b>[..."market_top_carousel="...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_wizards.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L13073)</b><br><b>[..."market_top_carousel="...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_wizards.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L13077)</b><br>

---

#### Cgi: <b>[market_wizhost](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1075)</b>
Описание:
 Explicitly set reqwizard host, enabled via rearr-factors=market_wizhost=some_host:123<br/> Not a normal cgi-param because we can pass only rearr-factors throught verstka<br/>https://st.yandex-team.ru/MARKETOUT-8541<br/>
Пример использования:
```example: &market_wizhost=[SOME_VALUE]...```<br/>

---

#### Cgi: <b>[max-outlets](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L716)</b>
Описание:
<b>Возвращаемое значение</b>: CGI @max-outlets<br/> Used for limiting number of outlels.<br/>https://st.yandex-team.ru/MARKETOUT-4407<br/>
Пример использования:
```example: &max-outlets=[SOME_VALUE]...```<br/><b>[..."max-outlets=100"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_geo_shopping_list.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L695)</b><br><b>[..."max-outlets=100"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_geo_shopping_list.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L707)</b><br><b>[..."max-outlets=100"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_geo_shopping_list.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1140)</b><br>

---

#### Cgi: <b>[max_pictures](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2733)</b>
Описание:
https://st.yandex-team.ru/MARKETOUT-40216<br/>
Пример использования:
```example: &max_pictures=[SOME_VALUE]...```<br/><b>[..."max_pictures=10"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_offerinfo.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L523)</b><br>

---

#### Cgi: <b>[mcpricefrom](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L184)</b>
Описание:

Пример использования:
```example: &mcpricefrom=[SOME_VALUE]...```<br/><b>[..."mcpricefrom=1000"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_filter_models.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L53)</b><br><b>[..."mcpricefrom=1000"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_filter_models.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L56)</b><br><b>[..."mcpricefrom=1030"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_glparams_values_sort_by_dimension.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L356)</b><br>

---

#### Cgi: <b>[mcpriceto](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L187)</b>
Описание:

Пример использования:
```example: &mcpriceto=[SOME_VALUE]...```<br/><b>[..."mcpriceto=10000"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_recipes.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1665)</b><br><b>[..."mcpriceto=1300"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_filter_models.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L53)</b><br><b>[..."mcpriceto=2000"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_filter_models.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L56)</b><br>

---

#### Cgi: <b>[mega-points](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L854)</b>
Описание:
 Geo mode for mega-points MARKETOUT-23222<br/><b>Возвращаемое значение</b>: value of CGI-parameter &mega-points<br/>
Пример использования:
```example: &mega-points=[SOME_VALUE]...```<br/><b>[..."mega-points=true"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_outlet_delivery.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L3837)</b><br><b>[..."mega-points=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_outlet_delivery.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L4172)</b><br><b>[..."mega-points=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_outlet_delivery.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L4185)</b><br>

---

#### Cgi: <b>[min-count-to-show](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2546)</b>
Описание:
https://st.yandex-team.ru/MARKETRECOM-2645<br/><b>Возвращаемое значение</b>: value of CGI parameter "&min-count-to-show"<br/>
Пример использования:
```example: &min-count-to-show=[SOME_VALUE]...```<br/><b>[..."min-count-to-show=4"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_complementary_product_groups_blue.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L378)</b><br><b>[..."min-count-to-show=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_complementary_product_groups_blue.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L436)</b><br><b>[..."min-count-to-show=4"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_complementary_product_groups.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L392)</b><br>

---

#### Cgi: <b>[min-delivery-priority](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1828)</b>
Описание:
<b>Возвращаемое значение</b>: value of CGI parameter &min-delivery-priority<br/>
Пример использования:
```example: &min-delivery-priority=[SOME_VALUE]...```<br/><b>[..."min-delivery-priority="...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_delivery.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1779)</b><br><b>[..."min-delivery-priority=country"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_delivery.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1803)</b><br><b>[..."min-delivery-priority=priority"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_delivery.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1823)</b><br>

---

#### Cgi: <b>[min-num-doc](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L463)</b>
Описание:
<b>Возвращаемое значение</b>: minimum number of accepted documents to form non empty output<br/> Минимальное количество документов для формирования не пустого ответа, изначально делалось для ручки cpa_shop_incut.<br/> Должно быть меньше или равно cgi: &numdoc=<br/> Не дружит с пейджером<br/>
Пример использования:
```example: &min-num-doc=[SOME_VALUE]...```<br/><b>[..."min-num-doc=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_advertising_carousel.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L276)</b><br><b>[..."min-num-doc=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_advertising_carousel.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L380)</b><br><b>[..."min-num-doc=0"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_advertising_carousel.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L470)</b><br>

---

#### Cgi: <b>[mini-tank](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L779)</b>
Описание:
 Request marked as from mini-tank<br/><b>Возвращаемое значение</b>: value of CGI-parameter &mini-tank, default -- false<br/>
Пример использования:
```example: &mini-tank=[SOME_VALUE]...```<br/><b>[..."mini-tank=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_error_log.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L112)</b><br>

---

#### Cgi: <b>[minify-outlets](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1773)</b>
Описание:
 минималистичный вывод в place=outlets<br/>
Пример использования:
```example: &minify-outlets=[SOME_VALUE]...```<br/><b>[..."minify-outlets=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_outlet_delivery.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L3337)</b><br><b>[..."minify-outlets=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_outlet_delivery.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L3339)</b><br><b>[..."minify-outlets=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_outlet_delivery.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L4282)</b><br>

---

#### Cgi: <b>[minimize-output](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2757)</b>
Описание:
https://st.yandex-team.ru/MARKETOUT-40803<br/>
Пример использования:
```example: &minimize-output=[SOME_VALUE]...```<br/><b>[..."minimize-output=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_filters_lists.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L438)</b><br><b>[..."minimize-output=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_filters_lists.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L445)</b><br><b>[..."minimize-output=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_glparams.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L4380)</b><br>

---

#### Cgi: <b>[model-matching](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1082)</b>
Описание:
 Filter documents by matching to model<br/> Used my a partner API calls<br/>https://st.yandex-team.ru/MARKETOUT-8447<br/><b>Возвращаемое значение</b>: CGI-value &model-matching={matched,notmatched}<br/>
Пример использования:
```example: &model-matching=[SOME_VALUE]...```<br/><b>[..."model-matching=matched"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_miprime.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L190)</b><br><b>[..."model-matching=notmatched"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_miprime.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L195)</b><br>

---

#### Cgi: <b>[model-rating](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1711)</b>
Описание:
<b>Возвращаемое значение</b>: value of CGI parameter &model-rating<br/> return models with rating greater or equal<br/>https://st.yandex-team.ru/MARKETOUT-16764<br/>
Пример использования:
```example: &model-rating=[SOME_VALUE]...```<br/><b>[..."model-rating=7"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_advertising_carousel.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L380)</b><br><b>[..."model-rating=3.75"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_review_hub.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L565)</b><br><b>[..."model-rating=3.75"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_review_hub.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L603)</b><br>

---

#### Cgi: <b>[modelid](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L136)</b>
Описание:
<b>Заметка</b> can not be negative<br/>
Пример использования:
```example: &modelid=[SOME_VALUE]...```<br/><b>[..."modelid=584110"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_model_wizard.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L355)</b><br><b>[..."modelid=584110"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_model_wizard.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L358)</b><br><b>[..."modelid=584110"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_model_wizard.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L384)</b><br>

---

#### Cgi: <b>[msku-only](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1850)</b>
Описание:
https://st.yandex-team.ru/MARKETOUT-18547<br/>
Пример использования:
```example: &msku-only=[SOME_VALUE]...```<br/><b>[..."msku-only=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_brand_products.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1409)</b><br><b>[..."msku-only=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_brand_products.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1551)</b><br><b>[..."msku-only=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_brand_products.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1564)</b><br>

---

#### Cgi: <b>[mskus-list](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1651)</b>
Описание:
<b>Возвращаемое значение</b>: &mskus-list value in the following format: <msku_1>:<count_1>[,<msku_1>:<count_2>, ...]<br/> Is used for place=geo<br/>
Пример использования:
```example: &mskus-list=[SOME_VALUE]...```<br/><b>[..."mskus-list="...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_geo_shopping_list.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L692)</b><br><b>[..."mskus-list="...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_geo_shopping_list.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L704)</b><br><b>[..."mskus-list="...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_geo_shopping_list.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1137)</b><br>

---

#### Cgi: <b>[nav_tree_id](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L657)</b>
Описание:
 TODO MARKETOUT-20919 Удалить старые навигационные деревья<br/><b>Устаревший параметр</b><br/> Identifier of navigation tree to be used<br/><b>Возвращаемое значение</b>: value of CGI-parameter nav_tree_id<br/>
Пример использования:
```example: &nav_tree_id=[SOME_VALUE]...```<br/>

---

#### Cgi: <b>[need_banner](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2713)</b>
Описание:
https://st.yandex-team.ru/MARKETOUT-38893<br/>
Пример использования:
```example: &need_banner=[SOME_VALUE]...```<br/><b>[..."need_banner=0"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_vendor_incut.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1921)</b><br><b>[..."need_banner=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_vendor_incut.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1950)</b><br><b>[..."need_banner=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_vendor_incut.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1978)</b><br>

---

#### Cgi: <b>[new-picture-format](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1814)</b>
Описание:
<b>Возвращаемое значение</b>: value of CGI parameter &new-picture-format<br/>
Пример использования:
```example: &new-picture-format=[SOME_VALUE]...```<br/><b>[..."new-picture-format=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_complementary_product_groups_blue.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L378)</b><br><b>[..."new-picture-format=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_complementary_product_groups_blue.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L436)</b><br><b>[..."new-picture-format=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_commonly_purchased.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L736)</b><br>

---

#### Cgi: <b>[nid](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L663)</b>
Описание:
 Identifiers of navigation nodes inside navigation tree<br/><b>Заметка</b>: also expected &nav_tree_id parameter<br/><b>Возвращаемое значение</b>: value of &nid CGI-parameter<br/>
Пример использования:
```example: &nid=[SOME_VALUE]...```<br/><b>[..."nid=19900"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_model_wizard.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L343)</b><br><b>[..."nid=19900"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_model_wizard.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L346)</b><br><b>[..."nid=19900"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_model_wizard.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L358)</b><br>

---

#### Cgi: <b>[no-delivery-discount](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2061)</b>
Описание:
<b>Возвращаемое значение</b>: value of CGI-parameter &no-delivery-discount<br/>https://st.yandex-team.ru/MARKETOUT-26613<br/>
Пример использования:
```example: &no-delivery-discount=[SOME_VALUE]...```<br/><b>[..."no-delivery-discount=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_delivery_interval.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L502)</b><br><b>[..."no-delivery-discount=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_delivery_modifier.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1025)</b><br><b>[..."no-delivery-discount=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_delivery_modifier.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1057)</b><br>

---

#### Cgi: <b>[no-incuts](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2475)</b>
Описание:
 Remove incuts from output (for place=blender)<br/>https://st.yandex-team.ru/MARKETSEARCH-335<br/><b>Возвращаемое значение</b>: value of CGI parameter "&no-incuts"<br/>
Пример использования:
```example: &no-incuts=[SOME_VALUE]...```<br/>

---

#### Cgi: <b>[no-intents](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2237)</b>
Описание:
<b>Возвращаемое значение</b>: value of CGI-parameter &no-intents<br/>
Пример использования:
```example: &no-intents=[SOME_VALUE]...```<br/><b>[..."no-intents=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_disabling_gl_filters.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L486)</b><br><b>[..."no-intents=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_disabling_gl_filters.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L493)</b><br><b>[..."no-intents=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_disabling_gl_filters.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L503)</b><br>

---

#### Cgi: <b>[no-random](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L558)</b>
Описание:
 Enables/disables randomized parts in output<br/><b>Возвращаемое значение</b>: value of CGI-parameter &no-random, default -- false<br/>
Пример использования:
```example: &no-random=[SOME_VALUE]...```<br/><b>[..."no-random=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_categories_and_models_by_history.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L416)</b><br><b>[..."no-random=0"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_categories_and_models_by_history.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L426)</b><br><b>[..."no-random=0"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_offerinfo.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1071)</b><br>

---

#### Cgi: <b>[no-search-filters](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2233)</b>
Описание:
<b>Возвращаемое значение</b>: value of CGI-parameter &no-search-filters<br/> Usefull for disabling "filters" section in prime results for accelerating<br/> Is used for blue turbo pages<br/>https://st.yandex-team.ru/MARKETOUT-29645<br/>
Пример использования:
```example: &no-search-filters=[SOME_VALUE]...```<br/><b>[..."no-search-filters=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_graceful_degradation.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L557)</b><br><b>[..."no-search-filters=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_graceful_degradation.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L562)</b><br><b>[..."no-search-filters=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_intents.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L4046)</b><br>

---

#### Cgi: <b>[no-vbid-filter](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2584)</b>
Описание:
<b>Возвращаемое значение</b>: value of CGI-parameter &no-vbid-filter (get all analog models with flag `&show-card-analogs`)<br/>https://st.yandex-team.ru/MARKETOUT-37797<br/>
Пример использования:
```example: &no-vbid-filter=[SOME_VALUE]...```<br/><b>[..."no-vbid-filter=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_productoffers_analogs_settings.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L157)</b><br><b>[..."no-vbid-filter=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_productoffers_analogs_settings.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L184)</b><br><b>[..."no-vbid-filter=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_productoffers_analogs_settings.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L203)</b><br>

---

#### Cgi: <b>[nocache](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L646)</b>
Описание:
<b>Возвращаемое значение</b>: value of CGI-parameter nocache<br/>
Пример использования:
```example: &nocache=[SOME_VALUE]...```<br/><b>[..."nocache=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_memcache.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L207)</b><br><b>[..."nocache=da"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_prime.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L3947)</b><br>

---

#### Cgi: <b>[non-dummy-redirects](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1197)</b>
Описание:
 Return redirects with params instead of url-only dummy redirects in prime<br/>https://st.yandex-team.ru/MARKETOUT-9486<br/><b>Возвращаемое значение</b>: CGI-value &non-dummy-redirects=<br/>
Пример использования:
```example: &non-dummy-redirects=[SOME_VALUE]...```<br/><b>[..."non-dummy-redirects=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_published_vendors.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L36)</b><br><b>[..."non-dummy-redirects=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_published_vendors.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L40)</b><br><b>[..."non-dummy-redirects=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_rerequests.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L501)</b><br>

---

#### Cgi: <b>[noreask](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L503)</b>
Описание:
 Не исправлять опечатку, даже если spellchecker уверен в себе<br/>https://st.yandex-team.ru/MARKETOUT-13352<br/><b>Возвращаемое значение</b>: value of &noreask= CGI-parameter<br/>
Пример использования:
```example: &noreask=[SOME_VALUE]...```<br/><b>[..."noreask=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_rerequests.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L652)</b><br><b>[..."noreask=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_prime_redirects.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1627)</b><br>

---

#### Cgi: <b>[nosearchresults](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2226)</b>
Описание:
 Removes results from output, only statistics will be in output.<br/><b>Возвращаемое значение</b>: CGI-value &nosearchresults<br/>
Пример использования:
```example: &nosearchresults=[SOME_VALUE]...```<br/><b>[..."nosearchresults=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_nosearchresult.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L25)</b><br><b>[..."nosearchresults=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_nosearchresult.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L30)</b><br><b>[..."nosearchresults=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_top_categories.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L818)</b><br>

---

#### Cgi: <b>[numdoc](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L456)</b>
Описание:
<b>Возвращаемое значение</b>: documents on page hard limit (cgi: &numdoc=)<br/> Этот лимит имеет приоритет и во всех выдачах использующих Pager будет выдано не более этого количества<br/>
Пример использования:
```example: &numdoc=[SOME_VALUE]...```<br/><b>[..."numdoc="...](https://a.yandex-team.ru/arc_vcs/market/report/lite/simple_testcase.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L190)</b><br><b>[..."numdoc="...](https://a.yandex-team.ru/arc_vcs/market/report/lite/simple_testcase.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L199)</b><br><b>[..."numdoc="...](https://a.yandex-team.ru/arc_vcs/market/report/lite/simple_testcase.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L208)</b><br>

---

#### Cgi: <b>[off-promo-disabling-experiment](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2599)</b>
Описание:
<b>Возвращаемое значение</b>: value of CGI-parameter &off-promo-disabling-experiment (disable flag PromoDisablingExperiment)<br/>https://st.yandex-team.ru/MARKETMONEY-527<br/>
Пример использования:
```example: &off-promo-disabling-experiment=[SOME_VALUE]...```<br/><b>[..."off-promo-disabling-experiment=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_blue_promo_blue_promocode.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L818)</b><br><b>[..."off-promo-disabling-experiment=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_blue_promo_blue_promocode.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L826)</b><br><b>[..."off-promo-disabling-experiment=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_cart_promo_disabling_exp.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L265)</b><br>

---

#### Cgi: <b>[offer-shipping](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L248)</b>
Описание:

Пример использования:
```example: &offer-shipping=[SOME_VALUE]...```<br/><b>[..."offer-shipping=delivery"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_model_wizard.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L893)</b><br><b>[..."offer-shipping=delivery"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_model_wizard.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L896)</b><br><b>[..."offer-shipping=pickup"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_model_wizard.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L902)</b><br>

---

#### Cgi: <b>[offer-sku](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1518)</b>
Описание:
 Parameter is used to filter offers by SKU (Stock Keeping Unit).<br/><b>Устаревший параметр</b>: Использовался в ФФ для поиска офера по магазинному СКУ. Сейчас логичнее использовать маркетное СКУ (MarketSKU)<br/>
Пример использования:
```example: &offer-sku=[SOME_VALUE]...```<br/><b>[..."offer-sku="...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_services.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L909)</b><br><b>[..."offer-sku="...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_services.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L981)</b><br><b>[..."offer-sku=90000000000"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_print_doc.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L421)</b><br>

---

#### Cgi: <b>[offer-url-hash](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1545)</b>
Описание:
 Parameter is used to filter offers by hash of canonized url offer.<br/>
Пример использования:
```example: &offer-url-hash=[SOME_VALUE]...```<br/><b>[..."offer-url-hash=test_offer_url_hash"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_print_doc.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L441)</b><br><b>[..."offer-url-hash=12345123452"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_prime.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2925)</b><br><b>[..."offer-url-hash=12345123451"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_prime.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2937)</b><br>

---

#### Cgi: <b>[offer-url](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1549)</b>
Описание:
 Parameter is used to filter offers by url.<br/>
Пример использования:
```example: &offer-url=[SOME_VALUE]...```<br/><b>[..."offer-url=supersite.com%2Fsuperoffer.html%3Fwombat%3D1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_prime.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2945)</b><br>

---

#### Cgi: <b>[offerid](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L132)</b>
Описание:
 For recommendations<br/>
Пример использования:
```example: &offerid=[SOME_VALUE]...```<br/><b>[..."offerid="...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_accessories.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L135)</b><br><b>[..."offerid=BH8EPLtKmdLQhLUasgaOnA"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_accessories_facets.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L64)</b><br><b>[..."offerid=bpQ3a9LXZAl_Kz34vaOpSg"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_accessories_facets.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L115)</b><br>

---

#### Cgi: <b>[offers-list](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1657)</b>
Описание:
<b>Возвращаемое значение</b>: &offers-list value in the following format: <waremd5_1>:<count_1>[,<waremd5_2>:<count_2>, ...]<br/> Is used for place=actual_delivery and means offers list with offers count<br/> Also used for place=credit_info and represents offers in user selected cart<br/>
Пример использования:
```example: &offers-list=[SOME_VALUE]...```<br/><b>[..."offers-list=Sku2Price55-iLVm1Goleg"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_actual_delivery_saashub.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L242)</b><br><b>[..."offers-list=SkuFb1Pri55-iLVm1Goleg"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_actual_delivery_saashub.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L269)</b><br><b>[..."offers-list=SkuFb2Pri56-iLVm1Goleg"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_actual_delivery_saashub.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L301)</b><br>

---

#### Cgi: <b>[offers-set](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1169)</b>
Описание:
 Modifier what to return at productoffers place<br/><b>Возвращаемое значение</b>: CGI-value &offers-set<br/><b>Заметка</b>: possible values "top", "list", "listCpa", "default", "defaultList", "all", "intents", "cehacIntents"<br/>
Пример использования:
```example: &offers-set=[SOME_VALUE]...```<br/><b>[..."offers-set=default"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_default_offer_experiments.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L47)</b><br><b>[..."offers-set=default"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_default_offer_experiments.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L53)</b><br><b>[..."offers-set=default"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_default_offer_experiments.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L103)</b><br>

---

#### Cgi: <b>[ogrn](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2259)</b>
Описание:
<b>Возвращаемое значение</b>: value of CGI-parameter &ogrn<br/>https://st.yandex-team.ru/MARKETOUT-30382<br/>
Пример использования:
```example: &ogrn=[SOME_VALUE]...```<br/><b>[..."ogrn=1235"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_place_supplier_info.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L21)</b><br><b>[..."ogrn=1235"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_place_supplier_info.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L38)</b><br>

---

#### Cgi: <b>[omm_place](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1867)</b>
Описание:
<b>Возвращаемое значение</b>: value of CGI parameter &omm_place<br/>https://st.yandex-team.ru/MARKETOUT-18941<br/>
Пример использования:
```example: &omm_place=[SOME_VALUE]...```<br/><b>[..."omm_place=yandexapp_vertical"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_omm.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L682)</b><br><b>[..."omm_place=yandexapp_vertical"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_omm.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L686)</b><br><b>[..."omm_place=omm_findings"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_test_place.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L161)</b><br>

---

#### Cgi: <b>[on-page, shows](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L468)</b>
Описание:
<b>Возвращаемое значение</b>: documents on page soft limit (cgi: &shows= or &on-page=)<br/> Для разных place= эффективное число выводимых документов может отличаться от запрошенного в этом cgi-параметре<br/>
Пример использования:
```example: &on-page=[SOME_VALUE]...```<br/><b>[..."on-page=5"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_dynamic_model_stats.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1257)</b><br><b>[..."on-page=5"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_dynamic_model_stats.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1272)</b><br><b>[..."on-page=5"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_dynamic_model_stats.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1513)</b><br>```example: &shows=[SOME_VALUE]...```<br/>

---

#### Cgi: <b>[only-cached](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L650)</b>
Описание:
 return: fast response (10ms) redirect (or answer) from cache if exist else empty response<br/>
Пример использования:
```example: &only-cached=[SOME_VALUE]...```<br/><b>[..."only-cached=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_memcache.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L215)</b><br><b>[..."only-cached=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_memcache.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L232)</b><br><b>[..."only-cached=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_memcache.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L235)</b><br>

---

#### Cgi: <b>[onstock-excludes-new](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2250)</b>
Описание:
<b>Возвращаемое значение</b>: value of CGI-parameter &onstock-excludes-new<br/> исключать товары-новинки без офферов при onstock<br/>https://st.yandex-team.ru/MARKETPROJECT-2963<br/> default false<br/>
Пример использования:
```example: &onstock-excludes-new=[SOME_VALUE]...```<br/><b>[..."onstock-excludes-new=0"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_onstock_new.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L93)</b><br><b>[..."onstock-excludes-new=0"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_onstock_new.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L218)</b><br>

---

#### Cgi: <b>[onstock](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1000)</b>
Описание:
 Filter out all offers except having on_stock flag and models without offers matched to other filters<br/><b>Возвращаемое значение</b>: CGI-value &onstock<br/>
Пример использования:
```example: &onstock=[SOME_VALUE]...```<br/><b>[..."onstock=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_model_modifications.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L412)</b><br><b>[..."onstock="...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_model_wizard.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L758)</b><br><b>[..."onstock=0"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_model_wizard.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L768)</b><br>

---

#### Cgi: <b>[ontile](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1092)</b>
Описание:
 Max outlet number on single tile in geo output<br/><b>Возвращаемое значение</b>: CGI-values &ontile<br/>
Пример использования:
```example: &ontile=[SOME_VALUE]...```<br/><b>[..."ontile=5"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_geo.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2765)</b><br><b>[..."ontile=3000"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_outlet_delivery_to_satellite_regions_saashub.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L467)</b><br><b>[..."ontile=500"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_blue_market.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L4588)</b><br>

---

#### Cgi: <b>[open-now](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1141)</b>
Описание:
 Show outlets which are open at the moment of request<br/> Supports only place=geo and book-now offers/outlets<br/><b>Возвращаемое значение</b>: CGI-value &open-now=<br/>
Пример использования:
```example: &open-now=[SOME_VALUE]...```<br/>

---

#### Cgi: <b>[outlet-around-the-clock](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1513)</b>
Описание:
 Parameter is used to filter outlets which work not 'around-the-clock'.<br/>
Пример использования:
```example: &outlet-around-the-clock=[SOME_VALUE]...```<br/><b>[..."outlet-around-the-clock=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_shop_info.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1084)</b><br><b>[..."outlet-around-the-clock=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_shop_info.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1095)</b><br><b>[..."outlet-around-the-clock=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_shop_info.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1107)</b><br>

---

#### Cgi: <b>[outlet-bool-props](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1505)</b>
Описание:
 Parameter is used to filter outlets by boolean properties.<br/>
Пример использования:
```example: &outlet-bool-props=[SOME_VALUE]...```<br/>

---

#### Cgi: <b>[outlet-daily](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1509)</b>
Описание:
 Parameter is used to filter outlets which work not daily.<br/>
Пример использования:
```example: &outlet-daily=[SOME_VALUE]...```<br/><b>[..."outlet-daily=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_shop_info.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1061)</b><br><b>[..."outlet-daily=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_shop_info.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1072)</b><br><b>[..."outlet-daily=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_shop_info.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1107)</b><br>

---

#### Cgi: <b>[owner](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1191)</b>
Описание:
<b>Возвращаемое значение</b>: value of &owner=... CGI-parameter<br/> Used by frontend to notify report, that its component was used<br/> for rendering page specified as owner. E.g.,<br/> place=geo&owner=offercard means that map will be used for offercard<br/>
Пример использования:
```example: &owner=[SOME_VALUE]...```<br/><b>[..."owner=offercard"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_geo.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1569)</b><br><b>[..."owner=offercard"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_geo.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1574)</b><br><b>[..."owner=offercard"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_geo.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1580)</b><br>

---

#### Cgi: <b>[page, n, page-no](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L446)</b>
Описание:
<b>Возвращаемое значение</b>: value of &n= or &page= or &page-no= CGI-parameter<br/> page will be clamped to (1, MAXIMUM_PAGES_COUNT)<br/>
Пример использования:
```example: &page=[SOME_VALUE]...```<br/><b>[..."page=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/simple_testcase.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L190)</b><br><b>[..."page=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/simple_testcase.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L199)</b><br><b>[..."page=2"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/simple_testcase.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L208)</b><br>```example: &n=[SOME_VALUE]...```<br/>```example: &page-no=[SOME_VALUE]...```<br/><b>[..."page-no=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_also_viewed.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1315)</b><br><b>[..."page-no=2"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_also_viewed.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1334)</b><br>

---

#### Cgi: <b>[parallel-dj-force-use-main](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2319)</b>
Описание:

Пример использования:
```example: &parallel-dj-force-use-main=[SOME_VALUE]...```<br/>

---

#### Cgi: <b>[parcels-list](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1663)</b>
Описание:
<b>Возвращаемое значение</b>: list of parcels<br/> Is used for place=actual_delivery:<br/>https://wiki.yandex-team.ru/users/vladankor/fast_actual_delivery_outlets/<br/>
Пример использования:
```example: &parcels-list=[SOME_VALUE]...```<br/><b>[..."parcels-list=tp"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_actual_delivery_grouped_outlets.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L625)</b><br><b>[..."parcels-list=tp"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_actual_delivery_grouped_outlets.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L640)</b><br><b>[..."parcels-list=tp"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_actual_delivery_grouped_outlets.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L654)</b><br>

---

#### Cgi: <b>[parentPromoId](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2172)</b>
Описание:
<b>Возвращаемое значение</b>: value of CGI-parameter &parentPromoId<br/>https://st.yandex-team.ru/MARKETOUT-42992<br/>
Пример использования:
```example: &parentPromoId=[SOME_VALUE]...```<br/><b>[..."parentPromoId="...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_blue_promo_filters.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1004)</b><br><b>[..."parentPromoId="...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_blue_promo_filters.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1330)</b><br><b>[..."parentPromoId=four"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_dj.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2592)</b><br>

---

#### Cgi: <b>[partial-delivery-enabled](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2609)</b>
Описание:
<b>Возвращаемое значение</b>: value of CGI-parameter &partial-delivery-enabled<br/>https://st.yandex-team.ru/MARKETOUT-44565<br/>
Пример использования:
```example: &partial-delivery-enabled=[SOME_VALUE]...```<br/><b>[..."partial-delivery-enabled="...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_actual_delivery_presets.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2365)</b><br><b>[..."partial-delivery-enabled="...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_delivery_route.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2938)</b><br>

---

#### Cgi: <b>[pass-text-to-dj](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2899)</b>
Описание:
<b>Возвращаемое значение</b>: value of CGI-parameter pass-text-to-dj<br/>https://st.yandex-team.ru/MARKETRECOM-4242<br/>
Пример использования:
```example: &pass-text-to-dj=[SOME_VALUE]...```<br/>

---

#### Cgi: <b>[payments](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L593)</b>
Описание:
 Filter offers by payment methods<br/><b>Возвращаемое значение</b>: value of CGI-parameter &payments=delivery_card,delivery_cash,prepayment_card<br/>
Пример использования:
```example: &payments=[SOME_VALUE]...```<br/><b>[..."payments=prepayment_card"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_dsbs_delivery.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1572)</b><br><b>[..."payments="...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_dsbs_delivery.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1589)</b><br><b>[..."payments="...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_dsbs_delivery.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1660)</b><br>

---

#### Cgi: <b>[perks](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1745)</b>
Описание:

Пример использования:
```example: &perks=[SOME_VALUE]...```<br/><b>[..."perks=yandex_cashback"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_multipromo_priority.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L315)</b><br><b>[..."perks=yandex_cashback"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_promo_self_intersection.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L77)</b><br><b>[..."perks=yandex_cashback"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_recom_promo_filter.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L129)</b><br>

---

#### Cgi: <b>[pessimize-offers-without-picture](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2773)</b>
Описание:
https://st.yandex-team.ru/ECOMSERP-109<br/>
Пример использования:
```example: &pessimize-offers-without-picture=[SOME_VALUE]...```<br/><b>[..."pessimize-offers-without-picture=0"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_prime_sorting.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L397)</b><br><b>[..."pessimize-offers-without-picture=0"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_prime_sorting.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L407)</b><br>

---

#### Cgi: <b>[pi-from](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1358)</b>
Описание:
 Partner interface part<br/>https://st.yandex-team.ru/MARKETPARTNER-3058<br/>
Пример использования:
```example: &pi-from=[SOME_VALUE]...```<br/><b>[..."pi-from=sandbox"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_hide_cpc_links.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L234)</b><br><b>[..."pi-from=sandbox"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_hide_cpc_links.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L239)</b><br><b>[..."pi-from=sandbo"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_cis.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L131)</b><br>

---

#### Cgi: <b>[pickup-options-extended-grouping](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1727)</b>
Описание:
<b>Возвращаемое значение</b>: &pickup-options-extended-grouping<br/> It allows to group pickup options also by payment types<br/>
Пример использования:
```example: &pickup-options-extended-grouping=[SOME_VALUE]...```<br/><b>[..."pickup-options-extended-grouping=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_deferred_courier_delivery.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L154)</b><br><b>[..."pickup-options-extended-grouping=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_flat_courier_options.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L79)</b><br><b>[..."pickup-options-extended-grouping=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_on_demand_delivery.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L278)</b><br>

---

#### Cgi: <b>[pickup-options](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L881)</b>
Описание:
 Return self-delivery methods (to outlets) with days and price (raw or aggregated)<br/><b>Возвращаемое значение</b>: value of CGI-parameter &pickup-options<br/>
Пример использования:
```example: &pickup-options=[SOME_VALUE]...```<br/><b>[..."pickup-options=raw"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_actual_delivery_saashub.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L269)</b><br><b>[..."pickup-options=raw"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_actual_delivery_saashub.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L301)</b><br><b>[..."pickup-options=raw"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_actual_delivery_unified_tariffs.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L367)</b><br>

---

#### Cgi: <b>[pickupincluded](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L829)</b>
Описание:
 Set if delivery price should be included in offer price<br/><b>Возвращаемое значение</b>: value of CGI-parameter &pickupincluded<br/>
Пример использования:
```example: &pickupincluded=[SOME_VALUE]...```<br/>

---

#### Cgi: <b>[place](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1899)</b>
Описание:

Пример использования:
```example: &place=[SOME_VALUE]...```<br/><b>[..."place=prime"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_bids_recommender_formulas.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L28)</b><br><b>[..."place=bids_recommender"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_bids_recommender_formulas.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L38)</b><br><b>[..."place="...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_long_requests_to_req_wizard.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L26)</b><br>

---

#### Cgi: <b>[place](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L437)</b>
Описание:
<b>Возвращаемое значение</b>: parsed value of &place=... CGI-parameter<br/>
Пример использования:
```example: &place=[SOME_VALUE]...```<br/><b>[..."place=prime"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_bids_recommender_formulas.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L28)</b><br><b>[..."place=bids_recommender"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_bids_recommender_formulas.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L38)</b><br><b>[..."place="...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_long_requests_to_req_wizard.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L26)</b><br>

---

#### Cgi: <b>[place](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L441)</b>
Описание:
<b>Возвращаемое значение</b>: value of &place=... CGI-parameter<br/>
Пример использования:
```example: &place=[SOME_VALUE]...```<br/><b>[..."place=prime"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_bids_recommender_formulas.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L28)</b><br><b>[..."place=bids_recommender"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_bids_recommender_formulas.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L38)</b><br><b>[..."place="...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_long_requests_to_req_wizard.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L26)</b><br>

---

#### Cgi: <b>[platform](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2151)</b>
Описание:
<b>Возвращаемое значение</b>: value of CGI parameter "&platform"+<br/>https://st.yandex-team.ru/MARKETOUT-29295<br/>
Пример использования:
```example: &platform=[SOME_VALUE]...```<br/><b>[..."platform=desktop"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_ugc.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L381)</b><br><b>[..."platform=desktop"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_blender_incuts_from_access.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L219)</b><br><b>[..."platform=desktop"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_blender_incuts_from_access.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L220)</b><br>

---

#### Cgi: <b>[pof](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L695)</b>
Описание:
<b>Возвращаемое значение</b>: CGI-parameter &pof<br/>
Пример использования:
```example: &pof=[SOME_VALUE]...```<br/><b>[..."pof=905"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_omm.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L690)</b><br><b>[..."pof=905"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_omm.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L715)</b><br><b>[..."pof="...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_turbo_place_sku.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L371)</b><br>

---

#### Cgi: <b>[point_id, outlets](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L291)</b>
Описание:

Пример использования:
```example: &point_id=[SOME_VALUE]...```<br/><b>[..."point_id=221"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_geo.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L623)</b><br><b>[..."point_id=221"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_geo.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L627)</b><br><b>[..."point_id=211"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_geo.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L825)</b><br>```example: &outlets=[SOME_VALUE]...```<br/><b>[..."outlets=2001"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_multi_service_pickup.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L423)</b><br><b>[..."outlets=11010"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_multi_service_pickup.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L603)</b><br><b>[..."outlets="...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_place_outlets.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L280)</b><br>

---

#### Cgi: <b>[popular-filters](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2334)</b>
Описание:
<b>Возвращаемое значение</b>: value of CGI-parameter &popular-filters<br/>https://st.yandex-team.ru/MARKETOUT-28631<br/>
Пример использования:
```example: &popular-filters=[SOME_VALUE]...```<br/>

---

#### Cgi: <b>[post-index](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1765)</b>
Описание:
 Почтовый индекс отделения<br/>
Пример использования:
```example: &post-index=[SOME_VALUE]...```<br/><b>[..."post-index="...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_actual_delivery_presets.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1718)</b><br><b>[..."post-index="...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_postpayment_price_thresholds.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L180)</b><br><b>[..."post-index=115203"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_actual_delivery_combinator.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1802)</b><br>

---

#### Cgi: <b>[pp-list](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L634)</b>
Описание:

Пример использования:
```example: &pp-list=[SOME_VALUE]...```<br/><b>[..."pp-list="...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_pp_list.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L43)</b><br>

---

#### Cgi: <b>[pp](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L631)</b>
Описание:
 Идентификатор места показа ответа Репорта. Каждое возможное значение pp<br/> уникально идентифицирует тип страницы, для которой был сделан запрос к Репорту.<br/> Используется для статистики, например: идентификатор цели.<br/> Чертовски важный параметр, поскольку при подсчёте статистики ошибка<br/> проставления значения этого параметра неотличима от потери денег.<br/>https://wiki.yandex-team.ru/market/development/placement/<br/>
Пример использования:
```example: &pp=[SOME_VALUE]...```<br/><b>[..."pp=143"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_accessories.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L135)</b><br><b>[..."pp=143"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_accessories_facets.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L64)</b><br><b>[..."pp=143"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_accessories_facets.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L115)</b><br>

---

#### Cgi: <b>[prefer-own-marketplace](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1933)</b>
Описание:
 prefer Blue offer in offer list<br/>https://st.yandex-team.ru/MARKETOUT-22555<br/>
Пример использования:
```example: &prefer-own-marketplace=[SOME_VALUE]...```<br/><b>[..."prefer-own-marketplace=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_blue_on_green.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L308)</b><br><b>[..."prefer-own-marketplace=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_blue_on_green.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L334)</b><br><b>[..."prefer-own-marketplace=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_blue_on_green.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L350)</b><br>

---

#### Cgi: <b>[preferable-courier-delivery-day](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1668)</b>
Описание:
<b>Возвращаемое значение</b>: &preferable-courier-delivery-day<br/> Is used for place=actual_delivery<br/>
Пример использования:
```example: &preferable-courier-delivery-day=[SOME_VALUE]...```<br/><b>[..."preferable-courier-delivery-day=8"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_adjust_shipment_by_supplier.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L219)</b><br><b>[..."preferable-courier-delivery-day="...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_lms_handling_info.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L488)</b><br><b>[..."preferable-courier-delivery-day="...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_sdd.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L338)</b><br>

---

#### Cgi: <b>[preferable-courier-delivery-service](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1673)</b>
Описание:
<b>Возвращаемое значение</b>: &preferable-courier-delivery-service<br/> Is used for place=actual_delivery<br/>
Пример использования:
```example: &preferable-courier-delivery-service=[SOME_VALUE]...```<br/><b>[..."preferable-courier-delivery-service=179"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_adjust_shipment_by_supplier.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L219)</b><br><b>[..."preferable-courier-delivery-service=258"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_lms.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2282)</b><br><b>[..."preferable-courier-delivery-service=257"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_lms.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2401)</b><br>

---

#### Cgi: <b>[premium-ads](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1059)</b>
Описание:
 Indicates that report should return block premium Ads<br/><b>Возвращаемое значение</b>: CGI-value &premium-ads, false if not set<br/> TODO: rename this cgi-param to &premium-ads<br/>
Пример использования:
```example: &premium-ads=[SOME_VALUE]...```<br/><b>[..."premium-ads=0"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_blender.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1756)</b><br><b>[..."premium-ads=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_premium_ads.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L180)</b><br><b>[..."premium-ads=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_premium_ads.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L216)</b><br>

---

#### Cgi: <b>[price](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L128)</b>
Описание:
 For recommendations<br/>
Пример использования:
```example: &price=[SOME_VALUE]...```<br/><b>[..."price=50"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_accessories.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L135)</b><br><b>[..."price=1000"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_accessories_facets.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L64)</b><br><b>[..."price=2000"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_accessories_facets.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L115)</b><br>

---

#### Cgi: <b>[prices-no-vat](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2856)</b>
Описание:
<b>Возвращаемое значение</b>: cgi: "prices-no-vat"<br/>https://st.yandex-team.ru/MARKETOUT-44489<br/>
Пример использования:
```example: &prices-no-vat=[SOME_VALUE]...```<br/><b>[..."prices-no-vat=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_market_for_business.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L669)</b><br><b>[..."prices-no-vat=0"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_market_for_business.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L732)</b><br>

---

#### Cgi: <b>[prime-output](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1541)</b>
Описание:
https://st.yandex-team.ru/MARKETOUT-13590<br/> Тестовый флажок для управления выдачей прайма (все, только фильтры, только результаты).<br/>
Пример использования:
```example: &prime-output=[SOME_VALUE]...```<br/>

---

#### Cgi: <b>[prime-prune-count](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1758)</b>
Описание:
https://st.yandex-team.ru/MARKETOUT-17821<br/> будет использоваться на требовательных к скорости местам, например на морде<br/> Позволяет выставить прюнинг (т.е. количество документов, которые будут обработаны)<br/>
Пример использования:
```example: &prime-prune-count=[SOME_VALUE]...```<br/><b>[..."prime-prune-count=80000"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_pruning_tbs_tpsz.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L562)</b><br><b>[..."prime-prune-count=75000"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_pruning_tbs_tpsz.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L567)</b><br><b>[..."prime-prune-count=80000"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_pruning_tbs_tpsz.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L576)</b><br>

---

#### Cgi: <b>[priority-models](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2131)</b>
Описание:
<b>Возвращаемое значение</b>: value of CGI-parameter &priority-models used in TPlaceBrandProducts place<br/>https://st.yandex-team.ru/MARKETOUT-46167<br/>
Пример использования:
```example: &priority-models=[SOME_VALUE]...```<br/><b>[..."priority-models=132"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_brand_products.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1841)</b><br><b>[..."priority-models=132"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_brand_products.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1890)</b><br>

---

#### Cgi: <b>[promo-bundle-id](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1375)</b>
Описание:

Пример использования:
```example: &promo-bundle-id=[SOME_VALUE]...```<br/><b>[..."promo-bundle-id=219650101-promo"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_promo_bundle.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L773)</b><br><b>[..."promo-bundle-id=promo21787011"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_promo_bundle.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L809)</b><br><b>[..."promo-bundle-id=219650101-promo"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_promo_bundle.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L824)</b><br>

---

#### Cgi: <b>[promo-bundle-id](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1379)</b>
Описание:
<b>Возвращаемое значение</b>: value of CGI parameter filter-nonverifiable-promos<br/>
Пример использования:
```example: &promo-bundle-id=[SOME_VALUE]...```<br/><b>[..."promo-bundle-id=219650101-promo"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_promo_bundle.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L773)</b><br><b>[..."promo-bundle-id=promo21787011"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_promo_bundle.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L809)</b><br><b>[..."promo-bundle-id=219650101-promo"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_promo_bundle.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L824)</b><br>

---

#### Cgi: <b>[promo-by-cart-enabled](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2391)</b>
Описание:
 Pricedrop is enabled in current page<br/>https://st.yandex-team.ru/MARKETOUT-31739<br/><b>Возвращаемое значение</b>: value of CGI parameter "&promo-by-cart-enabled"<br/>
Пример использования:
```example: &promo-by-cart-enabled=[SOME_VALUE]...```<br/><b>[..."promo-by-cart-enabled=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_promo_by_cart.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1219)</b><br><b>[..."promo-by-cart-enabled=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_promo_by_cart.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1275)</b><br><b>[..."promo-by-cart-enabled=0"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_promo_by_cart.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1694)</b><br>

---

#### Cgi: <b>[promo-by-cart-hash](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2397)</b>
Описание:
 Pricedrop is enabled in current page for the model hashed in the value of parameter<br/>https://st.yandex-team.ru/MARKETRECOM-4524<br/><b>Возвращаемое значение</b>: value of CGI parameter "&pdc"<br/>
Пример использования:
```example: &promo-by-cart-hash=[SOME_VALUE]...```<br/>

---

#### Cgi: <b>[promo-by-cart-in-special-places-only](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2403)</b>
Описание:
 PriceDrop in special places mode on<br/>https://st.yandex-team.ru/MARKETOUT-31739<br/><b>Возвращаемое значение</b>: value of CGI parameter "&promo-by-cart-in-special-places-only"<br/>
Пример использования:
```example: &promo-by-cart-in-special-places-only=[SOME_VALUE]...```<br/><b>[..."promo-by-cart-in-special-places-only=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_promo_by_cart.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1209)</b><br><b>[..."promo-by-cart-in-special-places-only="...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_promo_by_cart.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1248)</b><br><b>[..."promo-by-cart-in-special-places-only=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_promo_by_cart.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1694)</b><br>

---

#### Cgi: <b>[promo-by-cart-mskus](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2410)</b>
Описание:
 A list of mskus in cart added from special places with pricedrop discount<br/> For msku from a list pricedrop discount is shown everywhere<br/>https://st.yandex-team.ru/MARKETOUT-31739<br/><b>Возвращаемое значение</b>: value of CGI parameter "&promo-by-cart-mskus"<br/>
Пример использования:
```example: &promo-by-cart-mskus=[SOME_VALUE]...```<br/><b>[..."promo-by-cart-mskus=22"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_promo_by_cart.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1223)</b><br><b>[..."promo-by-cart-mskus=21"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_promo_by_cart.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1227)</b><br><b>[..."promo-by-cart-mskus=22"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_promo_by_cart.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1231)</b><br>

---

#### Cgi: <b>[promo-by-user-cart-hids](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2421)</b>
Описание:
 Parameter to enable/disable promo cart discount<br/>https://st.yandex-team.ru/MARKETRECOM-2440<br/><b>Возвращаемое значение</b>: value of CGI parameter "&promo-by-user-cart-hids"<br/>
Пример использования:
```example: &promo-by-user-cart-hids=[SOME_VALUE]...```<br/><b>[..."promo-by-user-cart-hids=0"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_promo_by_cart.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1166)</b><br><b>[..."promo-by-user-cart-hids=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_promo_by_cart.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1179)</b><br><b>[..."promo-by-user-cart-hids=0"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_promo_by_cart.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1191)</b><br>

---

#### Cgi: <b>[promo-check-min-price-n-offers](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L172)</b>
Описание:

Пример использования:
```example: &promo-check-min-price-n-offers=[SOME_VALUE]...```<br/><b>[..."promo-check-min-price-n-offers=3"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_promo_check_min_price.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L324)</b><br>

---

#### Cgi: <b>[promo-check-min-price](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L169)</b>
Описание:

Пример использования:
```example: &promo-check-min-price=[SOME_VALUE]...```<br/><b>[..."promo-check-min-price=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_recom_promo_filter.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L139)</b><br><b>[..."promo-check-min-price=0"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_recom_promo_filter.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L142)</b><br><b>[..."promo-check-min-price=5"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_promo_check_min_price.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L181)</b><br>

---

#### Cgi: <b>[promo-check-min-quality](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L175)</b>
Описание:

Пример использования:
```example: &promo-check-min-quality=[SOME_VALUE]...```<br/><b>[..."promo-check-min-quality=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_promo_check_min_quality.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L31)</b><br><b>[..."promo-check-min-quality=0"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_promo_check_min_quality.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L35)</b><br>

---

#### Cgi: <b>[promo-list-prune-count](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1389)</b>
Описание:
https://st.yandex-team.ru/MARKETOUT-24076<br/><b>Возвращаемое значение</b>: the value of CGI parameter "&promo-list-prune-count"<br/>
Пример использования:
```example: &promo-list-prune-count=[SOME_VALUE]...```<br/>

---

#### Cgi: <b>[promo-min-quality](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L166)</b>
Описание:

Пример использования:
```example: &promo-min-quality=[SOME_VALUE]...```<br/><b>[..."promo-min-quality=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_default_offer.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L493)</b><br>

---

#### Cgi: <b>[promo-models-best](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1284)</b>
Описание:
 Show only best promo models. Indexer calculates them for us<br/> Used in place promo_models<br/>https://st.yandex-team.ru/MARKETOUT-14728<br/><b>Возвращаемое значение</b>: value of CGI parameter "&promo-models-best"<br/>
Пример использования:
```example: &promo-models-best=[SOME_VALUE]...```<br/>

---

#### Cgi: <b>[promo-outlets](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L142)</b>
Описание:

Пример использования:
```example: &promo-outlets=[SOME_VALUE]...```<br/>

---

#### Cgi: <b>[promo-recipe-id](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L148)</b>
Описание:

Пример использования:
```example: &promo-recipe-id=[SOME_VALUE]...```<br/><b>[..."promo-recipe-id=101"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_promo_recipes.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L156)</b><br><b>[..."promo-recipe-id=102"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_promo_recipes.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L172)</b><br>

---

#### Cgi: <b>[promo-recipe-name](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L151)</b>
Описание:

Пример использования:
```example: &promo-recipe-name=[SOME_VALUE]...```<br/><b>[..."promo-recipe-name=shop"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_promo_recipes.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L195)</b><br>

---

#### Cgi: <b>[promo-recipe](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L145)</b>
Описание:

Пример использования:
```example: &promo-recipe=[SOME_VALUE]...```<br/><b>[..."promo-recipe=vendor-promo-code"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_promo_recipes.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L31)</b><br><b>[..."promo-recipe=vendor-promo-code"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_promo_recipes.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L47)</b><br><b>[..."promo-recipe=shop-promo-code"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_promo_recipes.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L70)</b><br>

---

#### Cgi: <b>[promo-redirect](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L429)</b>
Описание:

Пример использования:
```example: &promo-redirect=[SOME_VALUE]...```<br/><b>[..."promo-redirect=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_promo_recipes.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L242)</b><br><b>[..."promo-redirect=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_promo_recipes.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L247)</b><br><b>[..."promo-redirect=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_promo_recipes.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L251)</b><br>

---

#### Cgi: <b>[promo-top-categories-count](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1394)</b>
Описание:
https://st.yandex-team.ru/MARKETOUT-24315<br/><b>Возвращаемое значение</b>: the value of CGI parameter "&promo-top-categories-count"<br/>
Пример использования:
```example: &promo-top-categories-count=[SOME_VALUE]...```<br/><b>[..."promo-top-categories-count=%s"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_promo_top_categories.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L115)</b><br><b>[..."promo-top-categories-count=%s"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_promo_top_categories.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L144)</b><br><b>[..."promo-top-categories-count=2"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_promo_top_categories.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L176)</b><br>

---

#### Cgi: <b>[promo-type](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L139)</b>
Описание:

Пример использования:
```example: &promo-type=[SOME_VALUE]...```<br/><b>[..."promo-type=%s"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_promo_top_categories.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L115)</b><br><b>[..."promo-type=%s"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_promo_top_categories.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L144)</b><br><b>[..."promo-type=%s"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_promo_top_categories.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L173)</b><br>

---

#### Cgi: <b>[promoclicks-stats-type](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1913)</b>
Описание:

Пример использования:
```example: &promoclicks-stats-type=[SOME_VALUE]...```<br/><b>[..."promoclicks-stats-type=allpromo"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_shop_vendor_promo_clicks_stats.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L40)</b><br><b>[..."promoclicks-stats-type=promocode"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_shop_vendor_promo_clicks_stats.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L72)</b><br><b>[..."promoclicks-stats-type=allpromo"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_shop_vendor_promo_clicks_stats.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L94)</b><br>

---

#### Cgi: <b>[promoid](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1265)</b>
Описание:
 Promo ID (promoid)<br/>https://st.yandex-team.ru/MARKETOUT-10347<br/><b>Возвращаемое значение</b>: value of CGI parameter "&promoid"<br/>
Пример использования:
```example: &promoid=[SOME_VALUE]...```<br/><b>[..."promoid=promo1034701_01_key000"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_disabled_promo.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L38)</b><br><b>[..."promoid=promo1034701_01_key000"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_promo.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L37)</b><br><b>[..."promoid=promo1184204_01_key000"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_promo.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L147)</b><br>

---

#### Cgi: <b>[prun-count](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L792)</b>
Описание:
 Count of documents for pruning<br/><b>Заметка</b>: this value overrides same named from rearr-factors<br/><b>Возвращаемое значение</b>: CGI-parameter &prun-count<br/>
Пример использования:
```example: &prun-count=[SOME_VALUE]...```<br/><b>[..."prun-count=4"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_recipes.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L748)</b><br><b>[..."prun-count=10000"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_recom_banned_categories.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L321)</b><br><b>[..."prun-count=10000"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_recom_banned_categories.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L396)</b><br>

---

#### Cgi: <b>[puid](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L342)</b>
Описание:
<b>Возвращаемое значение</b>: value of &puid=... CGI-parameter(user id for web and mobile app)<br/>
Пример использования:
```example: &puid=[SOME_VALUE]...```<br/><b>[..."puid="...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_blue_psku.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1215)</b><br><b>[..."puid=173712710"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_offer_type_priority_ranging.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L235)</b><br><b>[..."puid=173712710"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_offer_type_priority_ranging.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L252)</b><br>

---

#### Cgi: <b>[qrfrom](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L984)</b>
Описание:
 Filter out all offers with quality rating lower then value<br/><b>Возвращаемое значение</b>: CGI-value &qrfrom<br/>
Пример использования:
```example: &qrfrom=[SOME_VALUE]...```<br/><b>[..."qrfrom=4"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_geo.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L42)</b><br><b>[..."qrfrom=4"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_geo.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1240)</b><br><b>[..."qrfrom=4"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_productoffers_filters.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L33)</b><br>

---

#### Cgi: <b>[qtree](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2998)</b>
Описание:
https://st.yandex-team.ru/MARKETOUT-47532<br/> Explicit qtree filter, used to fill docid cache<br/>
Пример использования:
```example: &qtree=[SOME_VALUE]...```<br/><b>[..."qtree=cHicnZRPaBNREMZn3m7bx2talsRoWQyGXLoKQh"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_bk.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L218)</b><br><b>[..."qtree="...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_docid_cache.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L98)</b><br>

---

#### Cgi: <b>[query-markup](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L305)</b>
Описание:

Пример использования:
```example: &query-markup=[SOME_VALUE]...```<br/><b>[..."query-markup=%7B%22Tokens%22%3A+%5B%7B%22EndChar%22%3A+6%2C+%22Text%22%3A"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_bk.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L220)</b><br>

---

#### Cgi: <b>[range](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2329)</b>
Описание:
<b>Возвращаемое значение</b>: value of CGI-parameter &range<br/>https://st.yandex-team.ru/MARKETRECOM-2839<br/>
Пример использования:
```example: &range=[SOME_VALUE]...```<br/><b>[..."range=range9"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_dj_pins.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L325)</b><br>

---

#### Cgi: <b>[ranking-mode](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2551)</b>
Описание:
https://st.yandex-team.ru/MARKETOUT-42180<br/><b>Возвращаемое значение</b>: value of CGI parameter "&ranking-mode"<br/>
Пример использования:
```example: &ranking-mode=[SOME_VALUE]...```<br/><b>[..."ranking-mode=mn"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_advertising_carousel.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L150)</b><br><b>[..."ranking-mode=mn"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_advertising_carousel.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L189)</b><br><b>[..."ranking-mode=mn"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_advertising_carousel.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L276)</b><br>

---

#### Cgi: <b>[raw_delivery_options](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L876)</b>
Описание:
 Enable delivery options output without applying order-before parameter<br/><b>Возвращаемое значение</b>: value of CGI-parameter &raw_delivery_options<br/>
Пример использования:
```example: &raw_delivery_options=[SOME_VALUE]...```<br/><b>[..."raw_delivery_options=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_delivery.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1297)</b><br><b>[..."raw_delivery_options=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_delivery_literal.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1259)</b><br><b>[..."raw_delivery_options=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_delivery_literal_exp.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1261)</b><br>

---

#### Cgi: <b>[rearr-factors](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L367)</b>
Описание:
<b>Возвращаемое значение</b>: &rearr-factors= is a catch-all parameter for passing assorted values from SERP to Market.<br/>.<br/>
Пример использования:
```example: &rearr-factors=[SOME_VALUE]...```<br/><b>[..."rearr-factors=split="...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_accessories.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L135)</b><br><b>[..."rearr-factors=split="...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_accessories_price_filter.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L244)</b><br><b>[..."rearr-factors=rty_delivery_cart=2"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_actual_delivery_saashub.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L269)</b><br>

---

#### Cgi: <b>[reask-modelids](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2678)</b>
Описание:
<b>Заметка</b> can not be negative<br/>
Пример использования:
```example: &reask-modelids=[SOME_VALUE]...```<br/><b>[..."reask-modelids=301"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_reask_gallery_wizard.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L539)</b><br><b>[..."reask-modelids=301"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_reask_gallery_wizard.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L552)</b><br><b>[..."reask-modelids=301"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_reask_gallery_wizard.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L556)</b><br>

---

#### Cgi: <b>[reask-wizard-state](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2685)</b>
Описание:

Пример использования:
```example: &reask-wizard-state=[SOME_VALUE]...```<br/><b>[..."reask-wizard-state=mcpriceto%3A200"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_reask_gallery_wizard.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L689)</b><br><b>[..."reask-wizard-state=mcpricefrom%3A200"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_reask_gallery_wizard.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L695)</b><br><b>[..."reask-wizard-state=mcpricefrom%3A700"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_reask_gallery_wizard.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L701)</b><br>

---

#### Cgi: <b>[recipe-id](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1978)</b>
Описание:
<b>Возвращаемое значение</b>: value of CGI-parameter &recipe-id<br/>https://st.yandex-team.ru/MARKETOUT-24332<br/>
Пример использования:
```example: &recipe-id=[SOME_VALUE]...```<br/><b>[..."recipe-id=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_search_recipes.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L147)</b><br><b>[..."recipe-id=2"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_search_recipes.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L159)</b><br><b>[..."recipe-id=3"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_search_recipes.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L171)</b><br>

---

#### Cgi: <b>[recipe-text](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L282)</b>
Описание:
<b>Возвращаемое значение</b>: value of &recipe-text=<br/>https://st.yandex-team.ru/MARKETSEO-139<br/>
Пример использования:
```example: &recipe-text=[SOME_VALUE]...```<br/><b>[..."recipe-text=Фумигаторы%20от%20блох"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_recipes.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L268)</b><br>

---

#### Cgi: <b>[recipe_resource](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1641)</b>
Описание:
<b>Возвращаемое значение</b>: value of CGI parameter &recipe_resource<br/>https://st.yandex-team.ru/MARKETOUT-15865<br/>
Пример использования:
```example: &recipe_resource=[SOME_VALUE]...```<br/>

---

#### Cgi: <b>[recom-context](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2644)</b>
Описание:
<b>Возвращаемое значение</b>: value of CGI-parameter &recom-context<br/>https://st.yandex-team.ru/MARKETOUT-36208<br/>
Пример использования:
```example: &recom-context=[SOME_VALUE]...```<br/><b>[..."recom-context=SuperContext"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_dj_place.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1540)</b><br>

---

#### Cgi: <b>[recom-place](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2689)</b>
Описание:
https://st.yandex-team.ru/MARKETOUT-36107<br/>
Пример использования:
```example: &recom-place=[SOME_VALUE]...```<br/><b>[..."recom-place=shop_goods"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_recom_universal.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L168)</b><br><b>[..."recom-place=shop_goods"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_recom_universal.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L190)</b><br><b>[..."recom-place=shop_goods_in_category"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_recom_universal.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L221)</b><br>

---

#### Cgi: <b>[recommendation-places](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1881)</b>
Описание:
<b>Возвращаемое значение</b>: value of CGI parameter &recommendation-places<br/>https://st.yandex-team.ru/MARKETOUT-18941<br/>
Пример использования:
```example: &recommendation-places=[SOME_VALUE]...```<br/><b>[..."recommendation-places=products_by_history"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_recommendations_meta.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L110)</b><br><b>[..."recommendation-places="...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_recom_banned_categories.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L519)</b><br>

---

#### Cgi: <b>[recommendations-count](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1553)</b>
Описание:
 Parameter is used to specify number of positions for recommendations.<br/>
Пример использования:
```example: &recommendations-count=[SOME_VALUE]...```<br/><b>[..."recommendations-count=50"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_bids_recommender.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L704)</b><br>

---

#### Cgi: <b>[reference-price](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1501)</b>
Описание:
 Parameter is used in 'productoffers' place. It is equivalent to &mcpriceto=(reference-price * 1.05).<br/> Parameter take precedence over &mcpriceto.<br/>
Пример использования:
```example: &reference-price=[SOME_VALUE]...```<br/><b>[..."reference-price=100"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_productoffers.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2629)</b><br>

---

#### Cgi: <b>[referer](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L608)</b>
Описание:
 Returns referer of request<br/><b>Возвращаемое значение</b>: value of CGI-parameter &referer, if empty -- request header Referer<br/>
Пример использования:
```example: &referer=[SOME_VALUE]...```<br/><b>[..."referer=https%3A%2F%2Fdefault.market-exp.pepelac2ft.yandex.ru%2Fproduct%2F10813494%2Fspec%3Fhid%3D90584"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_common_log.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L20)</b><br><b>[..."referer=https%3A%2F%2Fdefault.market-exp.pepelac2ft.yandex.ru%2Fproduct%2F10813494%2Fspec%3Fhid%3D90584"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_common_log.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L41)</b><br><b>[..."referer="...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_common_log.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L65)</b><br>

---

#### Cgi: <b>[regset](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L353)</b>
Описание:
<b>Возвращаемое значение</b>: value of &regset=... CGI-parameter<br/><b>Заметка</b>: if &rids is not set this parameter is ignored<br/><b>Заметка</b>: if &offer-shipping=[pickup,store,delivery,postomat] this parameter is ignored<br/><b>Заметка</b>: if set to 0 or 1, ignore some region filtering<br/>
Пример использования:
```example: &regset=[SOME_VALUE]...```<br/><b>[..."regset=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_actual_delivery_unified_tariffs.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L367)</b><br><b>[..."regset=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_actual_delivery_unified_tariffs.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L388)</b><br><b>[..."regset=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_actual_delivery_unified_tariffs.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L409)</b><br>

---

#### Cgi: <b>[relax-filters](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1418)</b>
Описание:
https://st.yandex-team.ru/MARKETOUT-12190<br/><b>Возвращаемое значение</b>: value of CGI parameter "&relax-filters"<br/>
Пример использования:
```example: &relax-filters=[SOME_VALUE]...```<br/><b>[..."relax-filters=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_geo.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2295)</b><br><b>[..."relax-filters="...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_geo.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2299)</b><br><b>[..."relax-filters=1%s"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_geo.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2304)</b><br>

---

#### Cgi: <b>[relax-relevance](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1424)</b>
Описание:
 Relax relevance threshold<br/>https://st.yandex-team.ru/MARKETOUT-21059<br/><b>Возвращаемое значение</b>: value of CGI parameter &relax-relevance<br/>
Пример использования:
```example: &relax-relevance=[SOME_VALUE]...```<br/><b>[..."relax-relevance="...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_filtering_by_relevance.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L413)</b><br><b>[..."relax-relevance=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_filtering_by_relevance.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L436)</b><br><b>[..."relax-relevance=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_filtering_by_relevance.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L452)</b><br>

---

#### Cgi: <b>[relev-factors](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L317)</b>
Описание:

Пример использования:
```example: &relev-factors=[SOME_VALUE]...```<br/><b>[..."relev-factors=bgfactors=FeXQkj-1AT0Klz_AAQGSCgUVPQoHQA"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_parallel.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L790)</b><br><b>[..."relev-factors=bgfactors=FeXQkj-1AT0Klz_AAQGSCgUVPQoHQA"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_parallel_products.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L795)</b><br><b>[..."relev-factors=Cpo%3D81"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_bk.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L219)</b><br>

---

#### Cgi: <b>[report-lockdown](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1454)</b>
Описание:
 Control report lockdown via place=report_status<br/>https://st.yandex-team.ru/MARKETOUT-17559<br/>
Пример использования:
```example: &report-lockdown=[SOME_VALUE]...```<br/><b>[..."report-lockdown=user"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_report_status.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L71)</b><br><b>[..."report-lockdown=0"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_report_status.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L82)</b><br><b>[..."report-lockdown=user"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_report_status.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L135)</b><br>

---

#### Cgi: <b>[report-status-action](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1449)</b>
Описание:
 Action to perform for place=report_status<br/>https://st.yandex-team.ru/MARKETOUT-13169<br/>
Пример использования:
```example: &report-status-action=[SOME_VALUE]...```<br/><b>[..."report-status-action=close"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_report_status.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L40)</b><br><b>[..."report-status-action=open"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_report_status.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L44)</b><br><b>[..."report-status-action=open"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_report_status.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L55)</b><br>

---

#### Cgi: <b>[req_attrs](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1613)</b>
Описание:
<b>Возвращаемое значение</b>: value of CGI parameter &req_attrs<br/> Show the values of these attributes in place=print_doc<br/>https://st.yandex-team.ru/MARKETOUT-6386<br/>
Пример использования:
```example: &req_attrs=[SOME_VALUE]...```<br/><b>[..."req_attrs=qdata"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_emergency_flags.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L63)</b><br><b>[..."req_attrs=qdata"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_emergency_flags.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L110)</b><br><b>[..."req_attrs=cbid"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_rty_qpipe.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L260)</b><br>

---

#### Cgi: <b>[reqid](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L493)</b>
Описание:
<b>Возвращаемое значение</b>: &reqid= parameter. CGI-parameter<br/>
Пример использования:
```example: &reqid=[SOME_VALUE]...```<br/><b>[..."reqid=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_new_blue_erf.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L84)</b><br><b>[..."reqid=2"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_new_blue_erf.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L103)</b><br><b>[..."reqid=3"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_new_blue_erf.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L122)</b><br>

---

#### Cgi: <b>[resale_goods](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2983)</b>
Описание:
<b>Возвращаемое значение</b>: is resale<br/>https://st.yandex-team.ru/MARKETOUT-47113 and https://st.yandex-team.ru/MARKETOUT-46787<br/>
Пример использования:
```example: &resale_goods=[SOME_VALUE]...```<br/><b>[..."resale_goods="...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_resale_goods.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L139)</b><br><b>[..."resale_goods=resale_resale"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_resale_goods.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L404)</b><br><b>[..."resale_goods=resale_resale"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_resale_goods.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L487)</b><br>

---

#### Cgi: <b>[resale_goods_condition](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2988)</b>
Описание:
<b>Возвращаемое значение</b>: Condition of resale<br/>https://st.yandex-team.ru/MARKETOUT-47114 and https://st.yandex-team.ru/MARKETOUT-46787<br/>
Пример использования:
```example: &resale_goods_condition=[SOME_VALUE]...```<br/><b>[..."resale_goods_condition="...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_resale_goods.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L141)</b><br>

---

#### Cgi: <b>[return-online-offers](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L839)</b>
Описание:
 Return online offers of shops from special list on productoffers<br/><b>Возвращаемое значение</b>: value of CGI-parameter &return-online-offers<br/>
Пример использования:
```example: &return-online-offers=[SOME_VALUE]...```<br/><b>[..."return-online-offers=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_productoffers.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L4338)</b><br><b>[..."return-online-offers=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_productoffers.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L4376)</b><br>

---

#### Cgi: <b>[review-grade](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1722)</b>
Описание:
<b>Возвращаемое значение</b>: value of CGI parameter &review-grade<br/> return models with reviews whose rating greater or equal<br/>https://st.yandex-team.ru/MARKETOUT-16764<br/>
Пример использования:
```example: &review-grade=[SOME_VALUE]...```<br/><b>[..."review-grade=4"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_review_hub.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L582)</b><br><b>[..."review-grade=4"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_review_hub.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L603)</b><br>

---

#### Cgi: <b>[reviews-with-comment](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1824)</b>
Описание:
<b>Возвращаемое значение</b>: value of CGI parameter &reviews-with-comment<br/>
Пример использования:
```example: &reviews-with-comment=[SOME_VALUE]...```<br/>

---

#### Cgi: <b>[rgb](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1646)</b>
Описание:
<b>Возвращаемое значение</b>: value of CGI parameter &rgb<br/> value=BLUE: Show only blue offers in search results in place=prime<br/>
Пример использования:
```example: &rgb=[SOME_VALUE]...```<br/><b>[..."rgb=blue"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_adjust_shipment_by_supplier.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L218)</b><br><b>[..."rgb=blue"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_alice.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L33)</b><br><b>[..."rgb=blue"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_alice.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L57)</b><br>

---

#### Cgi: <b>[rids](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L323)</b>
Описание:
<b>Возвращаемое значение</b>: value of &rids=... CGI-parameter<br/><b>Заметка</b>: any region assumed if not set<br/>s<br/>
Пример использования:
```example: &rids=[SOME_VALUE]...```<br/><b>[..."rids=213"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_actual_delivery_saashub.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L269)</b><br><b>[..."rids=213"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_actual_delivery_saashub.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L301)</b><br><b>[..."rids=213"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_actual_delivery_unified_tariffs.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L367)</b><br>

---

#### Cgi: <b>[rs](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1010)</b>
Описание:
<b>Возвращаемое значение</b>: value of CGI-parameter &rs<br/> Initially created for https://st.yandex-team.ru/MARKETOUT-7855, may be used for similar purposes elsewhere.<br/>
Пример использования:
```example: &rs=[SOME_VALUE]...```<br/><b>[..."rs="...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_model_wizard.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L741)</b><br><b>[..."rs="...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_model_wizard.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L747)</b><br><b>[..."rs=eJwzUvCS4xJLcspLLyjJDzZ29MzKrvCpCA1MLjEOlGBUYNBgAACpMAkq"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_model_wizard.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1008)</b><br>

---

#### Cgi: <b>[saas-ids-limit](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1984)</b>
Описание:
<b>Возвращаемое значение</b>: value of CGI-parameter &saas-ids-limit<br/> Max size of msku list in request to saas<br/>https://st.yandex-team.ru/MARKETOUT-24382<br/>
Пример использования:
```example: &saas-ids-limit=[SOME_VALUE]...```<br/>

---

#### Cgi: <b>[scale](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1968)</b>
Описание:
<b>Возвращаемое значение</b>: value of CGI-parameter &scale<br/> Initially created for https://st.yandex-team.ru/MARKETRECOM-1431 as a multiplier of items to request,<br/> may be used for similar purposes elsewhere.<br/>
Пример использования:
```example: &scale=[SOME_VALUE]...```<br/>

---

#### Cgi: <b>[search-in-clones](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2037)</b>
Описание:
<b>Возвращаемое значение</b>: value of CGI-parameter search-in-clones<br/>https://st.yandex-team.ru/MARKETOUT-25356<br/>
Пример использования:
```example: &search-in-clones=[SOME_VALUE]...```<br/><b>[..."search-in-clones=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_productoffers.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L4247)</b><br>

---

#### Cgi: <b>[search-only-in-leaves](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2141)</b>
Описание:
<b>Возвращаемое значение</b>: value of CGI-parameter &search-only-in-leaves<br/>https://st.yandex-team.ru/MARKETOUT-29177<br/>
Пример использования:
```example: &search-only-in-leaves=[SOME_VALUE]...```<br/>

---

#### Cgi: <b>[send-sale-data](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2589)</b>
Описание:
<b>Возвращаемое значение</b>: value of CGI-parameter &send-sale-data<br/>https://st.yandex-team.ru/MARKETOUT-44640<br/>
Пример использования:
```example: &send-sale-data=[SOME_VALUE]...```<br/><b>[..."send-sale-data=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_search_auction_cpa.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1130)</b><br><b>[..."send-sale-data=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_cpa_shop_incut.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1062)</b><br>

---

#### Cgi: <b>[session-page-view-unique-id](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2433)</b>
Описание:
 Parameter to define recommendations on page within a session<br/>https://st.yandex-team.ru/MARKETRECOM-5567<br/><b>Возвращаемое значение</b>: value of CGI parameter "&session-page-view-unique-id"<br/>
Пример использования:
```example: &session-page-view-unique-id=[SOME_VALUE]...```<br/><b>[..."session-page-view-unique-id=session_page_view_unique_id_1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_dj_place.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L562)</b><br>

---

#### Cgi: <b>[shcatid](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1732)</b>
Описание:
<b>Возвращаемое значение</b>: &shcatid<br/> for place=miprime MARKETOUT-17286<br/>
Пример использования:
```example: &shcatid=[SOME_VALUE]...```<br/><b>[..."shcatid="...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_miprime.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L178)</b><br>

---

#### Cgi: <b>[shop-delivery](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1563)</b>
Описание:
<b>Возвращаемое значение</b>: value of CGI parameter &shop-delivery<br/>https://st.yandex-team.ru/MARKETOUT-14059<br/>
Пример использования:
```example: &shop-delivery=[SOME_VALUE]...```<br/><b>[..."shop-delivery=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_new_pickup.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L304)</b><br><b>[..."shop-delivery=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_shop_info.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1303)</b><br><b>[..."shop-delivery=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_shop_info.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1371)</b><br>

---

#### Cgi: <b>[shop-in-shop-top-count](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2904)</b>
Описание:
<b>Возвращаемое значение</b>: shop-in-shop-top-count<br/>https://st.yandex-team.ru/MARKETOUT-44187 & https://st.yandex-team.ru/MARKETOUT-44610<br/>
Пример использования:
```example: &shop-in-shop-top-count=[SOME_VALUE]...```<br/>

---

#### Cgi: <b>[shop-offers-chunk](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L547)</b>
Описание:
<b>Возвращаемое значение</b>: &shop-offers-chunk= parameter. CGI-parameter<br/> shop-offers-chunk parameter is supposed to use only with place = shopoffers<br/>
Пример использования:
```example: &shop-offers-chunk=[SOME_VALUE]...```<br/><b>[..."shop-offers-chunk=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_shopoffers.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L47)</b><br><b>[..."shop-offers-chunk=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_shopoffers.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L64)</b><br><b>[..."shop-offers-chunk=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_shopoffers.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L87)</b><br>

---

#### Cgi: <b>[shop-promo-id](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2178)</b>
Описание:
<b>Возвращаемое значение</b>: value of CGI-parameter &shop-promo-id<br/>https://st.yandex-team.ru/MARKETOUT-30247<br/> !!! IMPORTANT CREATES OFFER ID FILTERS ON META<br/>
Пример использования:
```example: &shop-promo-id=[SOME_VALUE]...```<br/><b>[..."shop-promo-id="...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_blue_promo_blue_promocode.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1031)</b><br><b>[..."shop-promo-id="...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_blue_promo_filters.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L831)</b><br><b>[..."shop-promo-id="...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_blue_promo_filters.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1114)</b><br>

---

#### Cgi: <b>[shop-sku](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1526)</b>
Описание:
 Parameter is used to filter offers by SKU (Stock Keeping Unit).<br/>
Пример использования:
```example: &shop-sku=[SOME_VALUE]...```<br/><b>[..."shop-sku=9991"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_supplier_high_prices.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L408)</b><br><b>[..."shop-sku=9992"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_supplier_high_prices.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L410)</b><br><b>[..."shop-sku=9992"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_supplier_high_prices.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L413)</b><br>

---

#### Cgi: <b>[shopping-list](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1232)</b>
Описание:
 offer/model/cluster IDs<br/><b>Заметка</b>: value example (offerid, modelid, modelid, offerid):<br/><b>Заметка</b>:     o:09lEaAKkQll1XTaaaaaaaQ:1,m:3501:2,m:3502:1,o:2b0-iAnHLZST2Ekoq4xElr:5<br/>
Пример использования:
```example: &shopping-list=[SOME_VALUE]...```<br/><b>[..."shopping-list=m"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_alt_same_shop.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L970)</b><br><b>[..."shopping-list=m"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_alt_same_shop.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1003)</b><br><b>[..."shopping-list=m"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_alt_same_shop.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1070)</b><br>

---

#### Cgi: <b>[shops-per-business](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2886)</b>
Описание:
<b>Возвращаемое значение</b>: shops per business in place=shop_info, 0 for all<br/>https://st.yandex-team.ru/MARKETOUT-45207<br/>
Пример использования:
```example: &shops-per-business=[SOME_VALUE]...```<br/><b>[..."shops-per-business=0"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_shop_info.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2671)</b><br><b>[..."shops-per-business=2"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_shop_info.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2672)</b><br><b>[..."shops-per-business=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_shop_info.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2698)</b><br>

---

#### Cgi: <b>[short-params-list](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2682)</b>
Описание:
 For place compare_products<br/>
Пример использования:
```example: &short-params-list=[SOME_VALUE]...```<br/><b>[..."short-params-list=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_compare_products.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1568)</b><br><b>[..."short-params-list=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_compare_products.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1599)</b><br><b>[..."short-params-list=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_compare_products.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1609)</b><br>

---

#### Cgi: <b>[short_sorts_names](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2823)</b>
Описание:
<b>Возвращаемое значение</b>: value of short_sorts_names CGI-parameter<br/>https://st.yandex-team.ru/MARKETOUT-43588<br/>
Пример использования:
```example: &short_sorts_names=[SOME_VALUE]...```<br/><b>[..."short_sorts_names=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_blue_market.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L3459)</b><br><b>[..."short_sorts_names=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_blue_market.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L3507)</b><br>

---

#### Cgi: <b>[show-alcohol](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2056)</b>
Описание:
<b>Возвращаемое значение</b>: value of CGI-parameter &show-alcohol<br/>https://st.yandex-team.ru/MARKETOUT-26436<br/>
Пример использования:
```example: &show-alcohol=[SOME_VALUE]...```<br/><b>[..."show-alcohol=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_actual_delivery_presets.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1856)</b><br><b>[..."show-alcohol=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_actual_delivery_presets.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1889)</b><br><b>[..."show-alcohol=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_actual_delivery_presets.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1919)</b><br>

---

#### Cgi: <b>[show-all-complementary-products](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2788)</b>
Описание:
<b>Возвращаемое значение</b>: value of CGI parameter show-all-complementary-products<br/>https://st.yandex-team.ru/MARKETRECOM-3895<br/>
Пример использования:
```example: &show-all-complementary-products=[SOME_VALUE]...```<br/><b>[..."show-all-complementary-products="...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_complementary_product_groups.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L430)</b><br><b>[..."show-all-complementary-products="...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_complementary_product_groups.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L452)</b><br><b>[..."show-all-complementary-products=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_complementary_product_groups.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L488)</b><br>

---

#### Cgi: <b>[show-book-now-only](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L963)</b>
Описание:
 Filter out all offers except eligible for booking (in user region)?<br/><b>Возвращаемое значение</b>: CGI-value &show-book-now-only<br/>
Пример использования:
```example: &show-book-now-only=[SOME_VALUE]...```<br/><b>[..."show-book-now-only=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_geo.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L42)</b><br><b>[..."show-book-now-only=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_geo.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L825)</b><br><b>[..."show-book-now-only=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_geo.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L865)</b><br>

---

#### Cgi: <b>[show-booking-outlets](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1048)</b>
Описание:
 Indicates that report should return a list of outlets in the user region<br/><b>Возвращаемое значение</b>: CGI-value &show-booking-outlets, false if not set<br/>
Пример использования:
```example: &show-booking-outlets=[SOME_VALUE]...```<br/><b>[..."show-booking-outlets=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_book_now.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L859)</b><br><b>[..."show-booking-outlets=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_book_now.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L877)</b><br><b>[..."show-booking-outlets=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_book_now.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L910)</b><br>

---

#### Cgi: <b>[show-card-analogs](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2574)</b>
Описание:
<b>Возвращаемое значение</b>: value of CGI-parameter &show-card-analogs<br/>https://st.yandex-team.ru/MARKETOUT-37797<br/>
Пример использования:
```example: &show-card-analogs=[SOME_VALUE]...```<br/><b>[..."show-card-analogs=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_productoffers_analogs_settings.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L157)</b><br><b>[..."show-card-analogs=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_productoffers_analogs_settings.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L184)</b><br><b>[..."show-card-analogs=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_productoffers_analogs_settings.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L203)</b><br>

---

#### Cgi: <b>[show-credits](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2537)</b>
Описание:
 Enable calculating offer credit info upon requests to:<br/> - place=prime<br/> - place=sku_offers<br/> - place=credit_info<br/> Overridden by rearr-factor 'market_show_credits' if the latter is present<br/>https://st.yandex-team.ru/MARKETOUT-34232<br/><b>Возвращаемое значение</b>: value of CGI parameter "&show-credits"<br/>
Пример использования:
```example: &show-credits=[SOME_VALUE]...```<br/><b>[..."show-credits="...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_place_credit_info.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L211)</b><br><b>[..."show-credits=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_place_credit_info.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L314)</b><br><b>[..."show-credits=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_place_credit_info.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L399)</b><br>

---

#### Cgi: <b>[show-cutprice](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1632)</b>
Описание:
<b>Возвращаемое значение</b>: value of CGI parameter &show-cutprice<br/>
Пример использования:
```example: &show-cutprice=[SOME_VALUE]...```<br/><b>[..."show-cutprice=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_productoffers_pp.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L105)</b><br><b>[..."show-cutprice=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_productoffers_pp.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L111)</b><br><b>[..."show-cutprice=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_productoffers_premium.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L367)</b><br>

---

#### Cgi: <b>[show-extended-info](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2111)</b>
Описание:
<b>Возвращаемое значение</b>: value of CGI-parameter &show-extended-info<br/>https://st.yandex-team.ru/MARKETOUT-28351<br/>
Пример использования:
```example: &show-extended-info=[SOME_VALUE]...```<br/>

---

#### Cgi: <b>[show-filter](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1536)</b>
Описание:
<b>Возвращаемое значение</b>: value of CGI parameter &show-filter<br/>https://st.yandex-team.ru/MARKETOUT-13851<br/>
Пример использования:
```example: &show-filter=[SOME_VALUE]...```<br/><b>[..."show-filter=vendor"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_disabling_gl_filters.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L448)</b><br><b>[..."show-filter=vendor"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_disabling_gl_filters.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L486)</b><br><b>[..."show-filter=vendor"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_disabling_gl_filters.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L493)</b><br>

---

#### Cgi: <b>[show-filtered-buckets-and-carriers](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2086)</b>
Описание:
<b>Возвращаемое значение</b>: value of CGI-parameter &show-filtered-buckets-and-carriers<br/>https://st.yandex-team.ru/MARKETOUT-27263<br/>
Пример использования:
```example: &show-filtered-buckets-and-carriers=[SOME_VALUE]...```<br/><b>[..."show-filtered-buckets-and-carriers=true"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_actual_delivery.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L5075)</b><br>

---

#### Cgi: <b>[show-free-offers](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2569)</b>
Описание:
<b>Возвращаемое значение</b>: value of CGI-parameter &show-free-offers<br/>https://st.yandex-team.ru/MARKETPROJECT-4208<br/>
Пример использования:
```example: &show-free-offers=[SOME_VALUE]...```<br/>

---

#### Cgi: <b>[show-geo-cpa](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1174)</b>
Описание:
<b>Возвращаемое значение</b>: enables CPA on geo places<br/>https://st.yandex-team.ru/MARKETOUT-9177<br/>
Пример использования:
```example: &show-geo-cpa=[SOME_VALUE]...```<br/><b>[..."show-geo-cpa=da"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_cpa_category_geo.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L169)</b><br><b>[..."show-geo-cpa=da"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_cpa_category_geo.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L205)</b><br><b>[..."show-geo-cpa=da"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_cpa_category_geo.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L248)</b><br>

---

#### Cgi: <b>[show-installments](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2541)</b>
Описание:
https://st.yandex-team.ru/MARKETOUT-43129<br/>
Пример использования:
```example: &show-installments=[SOME_VALUE]...```<br/><b>[..."show-installments="...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_installment_info.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L197)</b><br>

---

#### Cgi: <b>[show-min-quantity](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1337)</b>
Описание:
 Show min quantity parameters for offers<br/>https://st.yandex-team.ru/MARKETOUT-11791<br/><b>Возвращаемое значение</b>: value of CGI parameter "&show-min-quantity"<br/><b>Заметка</b>: possible values (no(default),yes,cpa-to-cpc)<br/>
Пример использования:
```example: &show-min-quantity=[SOME_VALUE]...```<br/><b>[..."show-min-quantity=no"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_min_quantity.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L241)</b><br><b>[..."show-min-quantity=yes"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_min_quantity.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L244)</b><br><b>[..."show-min-quantity=cpa-to-cpc"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_min_quantity.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L247)</b><br>

---

#### Cgi: <b>[show-model-card-params](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1568)</b>
Описание:
<b>Возвращаемое значение</b>: value of CGI parameter &show-model-card-params<br/>https://st.yandex-team.ru/MARKETOUT-15054<br/>
Пример использования:
```example: &show-model-card-params=[SOME_VALUE]...```<br/><b>[..."show-model-card-params=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_glparams.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1873)</b><br><b>[..."show-model-card-params=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_glparams.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1878)</b><br><b>[..."show-model-card-params=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_glparams.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L3130)</b><br>

---

#### Cgi: <b>[show-models-specs](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1343)</b>
Описание:
 List of requested model description template types<br/>https://st.yandex-team.ru/MARKETOUT-11078<br/><b>Возвращаемое значение</b>: value of CGI parameter "&show-models-specs"<br/>
Пример использования:
```example: &show-models-specs=[SOME_VALUE]...```<br/><b>[..."show-models-specs=msku-full"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_blue_psku.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L209)</b><br><b>[..."show-models-specs=full"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_blue_psku.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L230)</b><br><b>[..."show-models-specs=full"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_modelinfo_sku.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L668)</b><br>

---

#### Cgi: <b>[show-models](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1033)</b>
Описание:
 Indicates that report should return models or only offers.<br/><b>Возвращаемое значение</b>: CGI-value &show-models, false if not set<br/>
Пример использования:
```example: &show-models=[SOME_VALUE]...```<br/><b>[..."show-models=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_blue_psku.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L209)</b><br><b>[..."show-models=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_blue_psku.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L945)</b><br><b>[..."show-models=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_blue_psku.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L995)</b><br>

---

#### Cgi: <b>[show-msku](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1846)</b>
Описание:
https://st.yandex-team.ru/MARKETOUT-18547<br/>
Пример использования:
```example: &show-msku=[SOME_VALUE]...```<br/><b>[..."show-msku=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_brand_products.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L725)</b><br><b>[..."show-msku=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_brand_products.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1240)</b><br><b>[..."show-msku=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_brand_products.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1488)</b><br>

---

#### Cgi: <b>[show-multi-service-intervals](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1876)</b>
Описание:
 show multi-service time intervals in place=actual_delviery<br/>https://st.yandex-team.ru/MARKETOUT-17858<br/>
Пример использования:
```example: &show-multi-service-intervals=[SOME_VALUE]...```<br/><b>[..."show-multi-service-intervals="...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_multi_service_time_intervals.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L442)</b><br><b>[..."show-multi-service-intervals=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_multi_service_time_intervals.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L445)</b><br><b>[..."show-multi-service-intervals=0"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_multi_service_time_intervals.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L446)</b><br>

---

#### Cgi: <b>[show-nearest-region](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2009)</b>
Описание:
<b>Возвращаемое значение</b>: value of CGI-parameter &show-nearest-region<br/> Actually replace rids with nearest region<br/><b>Заметка</b>: bool, default false<br/>https://st.yandex-team.ru/MARKETOUT-24880<br/>
Пример использования:
```example: &show-nearest-region=[SOME_VALUE]...```<br/><b>[..."show-nearest-region=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_nearest_city.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L73)</b><br>

---

#### Cgi: <b>[show-only-new-products](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1742)</b>
Описание:
https://st.yandex-team.ru/MARKETOUT-17383<br/> фильтр по новинкам<br/>
Пример использования:
```example: &show-only-new-products=[SOME_VALUE]...```<br/><b>[..."show-only-new-products=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_vendor_offers_models.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L318)</b><br>

---

#### Cgi: <b>[show-outlet-entities](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2254)</b>
Описание:
<b>Возвращаемое значение</b>: value of CGI parameter &show-outlet-entities<br/>
Пример использования:
```example: &show-outlet-entities=[SOME_VALUE]...```<br/><b>[..."show-outlet-entities=true"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_geo.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2899)</b><br>

---

#### Cgi: <b>[show-outlet](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1107)</b>
Описание:
 Types of geo output<br/><b>Возвращаемое значение</b>: value of CGI-parameter &show-outlet<br/>
Пример использования:
```example: &show-outlet=[SOME_VALUE]...```<br/><b>[..."show-outlet=offers"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_geo.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L639)</b><br><b>[..."show-outlet=tiles"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_geo.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L644)</b><br><b>[..."show-outlet=tiles"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_geo.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L776)</b><br>

---

#### Cgi: <b>[show-partner-documents](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1842)</b>
Описание:
https://st.yandex-team.ru/MARKETOUT-25195<br/>
Пример использования:
```example: &show-partner-documents=[SOME_VALUE]...```<br/><b>[..."show-partner-documents="...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_blue_psku.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L419)</b><br><b>[..."show-partner-documents="...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_blue_psku.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L432)</b><br><b>[..."show-partner-documents=true"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_blue_psku.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L895)</b><br>

---

#### Cgi: <b>[show-personal](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1596)</b>
Описание:
<b>Возвращаемое значение</b>: value of CGI parameter &show-personal<br/> Show model reviews in personal categories<br/> Only on place=multi_category and place=deals<br/>https://st.yandex-team.ru/MARKETOUT-16852<br/>
Пример использования:
```example: &show-personal=[SOME_VALUE]...```<br/><b>[..."show-personal=0"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_recom_banned_categories.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L414)</b><br><b>[..."show-personal=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_recom_for_women.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L174)</b><br><b>[..."show-personal=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_recom_for_women.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L190)</b><br>

---

#### Cgi: <b>[show-preorder](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1859)</b>
Описание:
https://st.yandex-team.ru/MARKETOUT-18858<br/>
Пример использования:
```example: &show-preorder=[SOME_VALUE]...```<br/><b>[..."show-preorder=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_on_demand_delivery.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1308)</b><br><b>[..."show-preorder=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_rty_qpipe.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L781)</b><br><b>[..."show-preorder=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_rty_qpipe.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L793)</b><br>

---

#### Cgi: <b>[show-real-delivery-for-preorder](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1862)</b>
Описание:

Пример использования:
```example: &show-real-delivery-for-preorder=[SOME_VALUE]...```<br/><b>[..."show-real-delivery-for-preorder=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_actual_delivery.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L4137)</b><br><b>[..."show-real-delivery-for-preorder=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_actual_delivery.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L4138)</b><br><b>[..."show-real-delivery-for-preorder="...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_actual_delivery.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L4393)</b><br>

---

#### Cgi: <b>[show-reviews](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1589)</b>
Описание:
<b>Возвращаемое значение</b>: value of CGI parameter &show-reviews<br/> Number of reviews to be shown with search results in place=prime<br/>https://st.yandex-team.ru/MARKETOUT-14808<br/>
Пример использования:
```example: &show-reviews=[SOME_VALUE]...```<br/><b>[..."show-reviews=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_recipes.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L253)</b><br><b>[..."show-reviews=0"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_recipes.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L261)</b><br><b>[..."show-reviews=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_recipes.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L797)</b><br>

---

#### Cgi: <b>[show-shops](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L744)</b>
Описание:
<b>Возвращаемое значение</b>: value of CGI parameter &show-shops<br/>https://st.yandex-team.ru/MARKETOUT-9824<br/>
Пример использования:
```example: &show-shops=[SOME_VALUE]...```<br/><b>[..."show-shops=all"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_top_glfilter_values.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L818)</b><br><b>[..."show-shops=top"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_top_glfilter_values.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L822)</b><br><b>[..."show-shops=all"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_top_glfilter_values.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L888)</b><br>

---

#### Cgi: <b>[show-stats](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2818)</b>
Описание:
<b>Возвращаемое значение</b>: value of CGI parameter &show-stats<br/>https://st.yandex-team.ru/MARKETOUT-43456<br/><b>Заметка</b>: if set to "yes", will return resource usage of this request. If set ot "only_stats", will return only resource usage<br/>
Пример использования:
```example: &show-stats=[SOME_VALUE]...```<br/><b>[..."show-stats=yes"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_stats.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L45)</b><br><b>[..."show-stats=only_stats"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_stats.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L48)</b><br>

---

#### Cgi: <b>[show-top-queries](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1439)</b>
Описание:
 Show bids recommendations by top offer queries<br/>https://st.yandex-team.ru/MARKETOUT-12568<br/>
Пример использования:
```example: &show-top-queries=[SOME_VALUE]...```<br/><b>[..."show-top-queries=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_bids_recommender.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L522)</b><br><b>[..."show-top-queries=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_bids_recommender.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1417)</b><br><b>[..."show-top-queries=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_bids_recommender.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1613)</b><br>

---

#### Cgi: <b>[show-urls](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1005)</b>
Описание:
 URL types, requested here will be shown and logged<br/><b>Возвращаемое значение</b>: CGI-value &show-urls<br/>
Пример использования:
```example: &show-urls=[SOME_VALUE]...```<br/><b>[..."show-urls=external%2Ccpa"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_cpa_only_parallel.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L46)</b><br><b>[..."show-urls=direct"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_filter_shops.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L243)</b><br><b>[..."show-urls=direct"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_filter_shops.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L256)</b><br>

---

#### Cgi: <b>[show-used-goods](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2914)</b>
Описание:
<b>Возвращаемое значение</b>: Use used goods (second hand) offers<br/>https://st.yandex-team.ru/MARKETOUT-45799<br/>
Пример использования:
```example: &show-used-goods=[SOME_VALUE]...```<br/><b>[..."show-used-goods="...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_used_goods.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L105)</b><br><b>[..."show-used-goods="...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_used_goods.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L134)</b><br><b>[..."show-used-goods="...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_used_goods.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L360)</b><br>

---

#### Cgi: <b>[showVendors](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L749)</b>
Описание:
<b>Возвращаемое значение</b>: value of CGI parameter &showVendors<br/>https://st.yandex-team.ru/MARKETOUT-7904<br/>
Пример использования:
```example: &showVendors=[SOME_VALUE]...```<br/><b>[..."showVendors=top"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_top_glfilter_values.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L687)</b><br><b>[..."showVendors=all"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_top_glfilter_values.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L688)</b><br><b>[..."showVendors=top"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_top_glfilter_values.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L748)</b><br>

---

#### Cgi: <b>[show_explicit_content](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1023)</b>
Описание:
 Allows restricted categories to be shown in output<br/><b>Возвращаемое значение</b>: CGI-value &show_explicit_content<br/>
Пример использования:
```example: &show_explicit_content=[SOME_VALUE]...```<br/><b>[..."show_explicit_content=medicine"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_wizards_medicine_restriction.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L227)</b><br><b>[..."show_explicit_content=all"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_wizards_medicine_restriction.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L271)</b><br><b>[..."show_explicit_content=medicine"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_wizards_medicine_restriction.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L291)</b><br>

---

#### Cgi: <b>[show_promo_features](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1918)</b>
Описание:
 Show feature params for offer which used in promo<br/>https://st.yandex-team.ru/MARKETOUT-21866<br/>
Пример использования:
```example: &show_promo_features=[SOME_VALUE]...```<br/><b>[..."show_promo_features="...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_cms_promo.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L125)</b><br>

---

#### Cgi: <b>[show_subscription_goods](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2828)</b>
Описание:
<b>Возвращаемое значение</b>: value of show_subscription_goods CGI-parameter<br/>https://st.yandex-team.ru/MARKETOUT-43116<br/>
Пример использования:
```example: &show_subscription_goods=[SOME_VALUE]...```<br/>

---

#### Cgi: <b>[skip-empty-request-check](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2091)</b>
Описание:
<b>Возвращаемое значение</b>: value of CGI-parameter &skip-empty-request-check<br/>https://st.yandex-team.ru/MARKETOUT-27941<br/>
Пример использования:
```example: &skip-empty-request-check=[SOME_VALUE]...```<br/>

---

#### Cgi: <b>[skip-group-model-offers](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1871)</b>
Описание:
https://st.yandex-team.ru/MARKETINDEXER-15795<br/>
Пример использования:
```example: &skip-group-model-offers=[SOME_VALUE]...```<br/><b>[..."skip-group-model-offers=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_discount.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L353)</b><br><b>[..."skip-group-model-offers=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_promo_type_filter.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L786)</b><br>

---

#### Cgi: <b>[skip-post-options-calc](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1990)</b>
Описание:
<b>Возвращаемое значение</b>: &skip-post-options-calc<br/> This flag allows to turn on/off post options calculation<br/>https://st.yandex-team.ru/MARKETOUT-23406<br/>
Пример использования:
```example: &skip-post-options-calc=[SOME_VALUE]...```<br/><b>[..."skip-post-options-calc="...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_actual_delivery.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L3496)</b><br>

---

#### Cgi: <b>[skip](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L480)</b>
Описание:
<b>Возвращаемое значение</b>: documents to be skipped from the start in addition to paging (cgi: &skip=)<br/>
Пример использования:
```example: &skip=[SOME_VALUE]...```<br/><b>[..."skip=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_personal_offers.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L203)</b><br><b>[..."skip=2"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_bestdeals_personal.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L135)</b><br><b>[..."skip=8"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_prime.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1026)</b><br>

---

#### Cgi: <b>[sku-all](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2622)</b>
Описание:
<b>Возвращаемое значение</b>: value of CGI-parameter &sku-all<br/><b>Заметка</b>: if set, report will set the sku field for white offers too<br/>
Пример использования:
```example: &sku-all=[SOME_VALUE]...```<br/><b>[..."sku-all=0"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_sku_white_prime.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L217)</b><br>

---

#### Cgi: <b>[sku-jmp-table](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2613)</b>
Описание:
<b>Возвращаемое значение</b>: value of CGI-parameter &sku-jmp-table<br/>
Пример использования:
```example: &sku-jmp-table=[SOME_VALUE]...```<br/><b>[..."sku-jmp-table=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_table_of_sizes.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2268)</b><br>

---

#### Cgi: <b>[sku-required](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2705)</b>
Описание:
https://st.yandex-team.ru/MARKETOUT-38624<br/>
Пример использования:
```example: &sku-required=[SOME_VALUE]...```<br/><b>[..."sku-required=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_cpa_shop_incut.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1305)</b><br><b>[..."sku-required=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_vendor_incut.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2157)</b><br>

---

#### Cgi: <b>[slider-rearr](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2564)</b>
Описание:
<b>Возвращаемое значение</b>: value of CGI parameter "&slider-rearr"<br/>
Пример использования:
```example: &slider-rearr=[SOME_VALUE]...```<br/>

---

#### Cgi: <b>[slider_ignore_doc](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2377)</b>
Описание:
https://st.yandex-team.ru/MARKETOUT-31681<br/>
Пример использования:
```example: &slider_ignore_doc=[SOME_VALUE]...```<br/>

---

#### Cgi: <b>[slider_type](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2373)</b>
Описание:
<b>Возвращаемое значение</b>: &slider_type= parameter<br/>https://st.yandex-team.ru/MARKETOUT-31681<br/>
Пример использования:
```example: &slider_type=[SOME_VALUE]...```<br/>

---

#### Cgi: <b>[source_base](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1069)</b>
Описание:
 Returns domain from source_base field<br/>https://st.yandex-team.ru/MARKETOUT-22276<br/>
Пример использования:
```example: &source_base=[SOME_VALUE]...```<br/><b>[..."source_base=avito.ru"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_click_log.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L189)</b><br><b>[..."source_base=avito.ru"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_goods_logs.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L180)</b><br><b>[..."source_base=avito.ru"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_show_log.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L542)</b><br>

---

#### Cgi: <b>[space-between-entity](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1962)</b>
Описание:
<b>Возвращаемое значение</b>: value of CGI-paramenet &space-between-entity<br/>https://st.yandex-team.ru/MARKETOUT-23856<br/>
Пример использования:
```example: &space-between-entity=[SOME_VALUE]...```<br/>

---

#### Cgi: <b>[split-strategy](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2264)</b>
Описание:
<b>Возвращаемое значение</b>: value of string view of strategy<br/>https://st.yandex-team.ru/MARKETOUT-30433<br/>
Пример использования:
```example: &split-strategy=[SOME_VALUE]...```<br/><b>[..."split-strategy=split-medicine"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_combine_medicine_split.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L419)</b><br><b>[..."split-strategy=split-medicine"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_combine_medicine_split.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L461)</b><br><b>[..."split-strategy=split-medicine"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_combine_medicine_split.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L503)</b><br>

---

#### Cgi: <b>[sponsored-place](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1064)</b>
Описание:
 Indicates place to show sponsored ads for place=sponsored_products<br/><b>Возвращаемое значение</b>: CGI-value &sponsored-place<br/>
Пример использования:
```example: &sponsored-place=[SOME_VALUE]...```<br/><b>[..."sponsored-place=block-on-search"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_sponsored_products.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L283)</b><br><b>[..."sponsored-place=block-on-search"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_sponsored_products.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L383)</b><br><b>[..."sponsored-place=mimic-on-search"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_sponsored_products.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L400)</b><br>

---

#### Cgi: <b>[src_pof](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2783)</b>
Описание:
<b>Возвращаемое значение</b>: value of CGI parameter &src_pof<br/>https://st.yandex-team.ru/MARKETOUT-17784<br/>
Пример использования:
```example: &src_pof=[SOME_VALUE]...```<br/><b>[..."src_pof=971"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_parallel.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2241)</b><br><b>[..."src_pof=971"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_parallel.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2276)</b><br><b>[..."src_pof=971"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_parallel_products.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2255)</b><br>

---

#### Cgi: <b>[stat-block-id](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L618)</b>
Описание:
<b>Возвращаемое значение</b>: value of CGI-parameter &stat-block-id<br/>
Пример использования:
```example: &stat-block-id=[SOME_VALUE]...```<br/><b>[..."stat-block-id=test"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_tskv_access_log.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L27)</b><br><b>[..."stat-block-id=2000000000020160101000000"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_show_log.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L737)</b><br><b>[..."stat-block-id=2000000000020160101000000"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_show_log.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L827)</b><br>

---

#### Cgi: <b>[strict-json-parser](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2368)</b>
Описание:
<b>Возвращаемое значение</b>: value of CGI-parameter &strict-json-parser<br/> Use strict json parser on parallel<br/>https://st.yandex-team.ru/MARKETOUT-31632<br/>
Пример использования:
```example: &strict-json-parser=[SOME_VALUE]...```<br/>

---

#### Cgi: <b>[strip_query_language](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L930)</b>
Описание:
 Strip query language operators before sending the request to basesearches.<br/>https://yandex.ru/support/search/query-language/qlanguage.xml<br/>https://st.yandex-team.ru/MARKETOUT-6992<br/>
Пример использования:
```example: &strip_query_language=[SOME_VALUE]...```<br/>

---

#### Cgi: <b>[subreqid](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L691)</b>
Описание:
<b>Возвращаемое значение</b>: CGI &subreqid=<br/> Используется для различения в логах разных подзапросов. Например, верстка может задавать один и тот же запрос:<br/> а) просто б) с опечаточником в) с кворумом г) еще как-то; и использован будет только один из а, б, в или г.<br/> Потому, чтобы в access-логах верстки можно было понять, результат какого из запросов к репорту был использовал, в лог пишется этот subreqid.<br/>
Пример использования:
```example: &subreqid=[SOME_VALUE]...```<br/><b>[..."subreqid=ololo"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_wizards.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L6161)</b><br><b>[..."subreqid=ololo"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_wizards.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L6236)</b><br><b>[..."subreqid="...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_wizards.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L6465)</b><br>

---

#### Cgi: <b>[suggest, suggest_text, suggest_type, suggest_reqid](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L583)</b>
Описание:
 Map of suggest parameters<br/><b>Возвращаемое значение</b>: map of keys and values of CGI-parameters &suggest, &suggest_text, &suggest_type, &suggest_reqid<br/>
Пример использования:
```example: &suggest=[SOME_VALUE]...```<br/><b>[..."suggest=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_rerequests.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L88)</b><br><b>[..."suggest=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_rerequests.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L102)</b><br><b>[..."suggest=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_rerequests.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L436)</b><br>```example: &suggest_text=[SOME_VALUE]...```<br/><b>[..."suggest_text="...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_rerequests.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L436)</b><br><b>[..."suggest_text="...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_rerequests.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L477)</b><br><b>[..."suggest_text=scissors"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_rerequests.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L522)</b><br>```example: &suggest_type=[SOME_VALUE]...```<br/><b>[..."suggest_type=category"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_redirects.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L543)</b><br><b>[..."suggest_type=type"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_redirects.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L770)</b><br><b>[..."suggest_type=recipe"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_redirects.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2492)</b><br>```example: &suggest_reqid=[SOME_VALUE]...```<br/><b>[..."suggest_reqid=reqid1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_redirects.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L770)</b><br>

---

#### Cgi: <b>[suggest](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L578)</b>
Описание:
 Type of redirect from suggest<br/><b>Возвращаемое значение</b>: value of CGI-parameter &suggest<br/>
Пример использования:
```example: &suggest=[SOME_VALUE]...```<br/><b>[..."suggest=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_rerequests.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L88)</b><br><b>[..."suggest=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_rerequests.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L102)</b><br><b>[..."suggest=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_rerequests.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L436)</b><br>

---

#### Cgi: <b>[suggest_text](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L277)</b>
Описание:

Пример использования:
```example: &suggest_text=[SOME_VALUE]...```<br/><b>[..."suggest_text="...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_rerequests.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L436)</b><br><b>[..."suggest_text="...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_rerequests.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L477)</b><br><b>[..."suggest_text=scissors"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_rerequests.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L522)</b><br>

---

#### Cgi: <b>[supplier-id](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1788)</b>
Описание:
<b>Возвращаемое значение</b>: value of CGI parameter supplier-id<br/>https://st.yandex-team.ru/MARKETOUT-17826<br/> Use supplier-id as filter on prime<br/> in order to show Bringly shops with<br/> offers from storage<br/>
Пример использования:
```example: &supplier-id=[SOME_VALUE]...```<br/><b>[..."supplier-id=225"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_demand_prediction.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L225)</b><br><b>[..."supplier-id=223"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_demand_prediction.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L250)</b><br><b>[..."supplier-id=225"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_demand_prediction.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L267)</b><br>

---

#### Cgi: <b>[supplier_type](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L426)</b>
Описание:
 supplier_type выставляется в 1 для поиска только p1 офферов<br/> или оставляем пустым чтобы показать все предложения<br/> Остальные значения не поддерживаются<br/> WARNING! Влияет на выбор байбокса в мскушке, т.к фильтрует с помощью литерала<br/>
Пример использования:
```example: &supplier_type=[SOME_VALUE]...```<br/><b>[..."supplier_type="...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_stat_numbers.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L968)</b><br><b>[..."supplier_type=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_stat_numbers.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L979)</b><br><b>[..."supplier_type=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_stat_numbers.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L980)</b><br>

---

#### Cgi: <b>[supported-incuts](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2798)</b>
Описание:
<b>Возвращаемое значение</b>: value of &supported-incuts CGI-parameter<br/>
Пример использования:
```example: &supported-incuts=[SOME_VALUE]...```<br/><b>[..."supported-incuts="...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_blender_bundles_catalog_quiz.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L135)</b><br><b>[..."supported-incuts="...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_blender_bundles_catalog_quiz.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L196)</b><br><b>[..."supported-incuts="...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_blender_incuts_from_access.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L180)</b><br>

---

#### Cgi: <b>[test-buckets](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L433)</b>
Описание:
<b>Возвращаемое значение</b>: value of &test-buckets CGI-parameter<br/>
Пример использования:
```example: &test-buckets=[SOME_VALUE]...```<br/><b>[..."test-buckets=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_wizards.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L6162)</b><br><b>[..."test-buckets=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_wizards.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L6236)</b><br><b>[..."test-buckets=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_bk.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L166)</b><br>

---

#### Cgi: <b>[test_bits](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1111)</b>
Описание:
<b>Возвращаемое значение</b>: value of &test_bits=... CGI-parameter<br/>
Пример использования:
```example: &test_bits=[SOME_VALUE]...```<br/><b>[..."test_bits=101010"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_bk.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L166)</b><br><b>[..."test_bits=101010"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_click_log.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L240)</b><br><b>[..."test_bits=101010"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_click_log.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L255)</b><br>

---

#### Cgi: <b>[test_tag](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1115)</b>
Описание:
<b>Возвращаемое значение</b>: value of &test_tag=... CGI-parameter<br/>
Пример использования:
```example: &test_tag=[SOME_VALUE]...```<br/><b>[..."test_tag=test_123"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_bk.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L166)</b><br><b>[..."test_tag=test_123"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_click_log.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L255)</b><br><b>[..."test_tag=cool"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_click_log.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1257)</b><br>

---

#### Cgi: <b>[text2](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L901)</b>
Описание:
 Offer exact title for bids recommender<br/><b>Возвращаемое значение</b>: value of CGI-parameter &text2<br/>
Пример использования:
```example: &text2=[SOME_VALUE]...```<br/><b>[..."text2=item"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_bids_recommender_non_local.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L82)</b><br><b>[..."text2=item"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_bids_recommender_non_local.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L112)</b><br><b>[..."text2=ball"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_used_goods.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L358)</b><br>

---

#### Cgi: <b>[text](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L274)</b>
Описание:

Пример использования:
```example: &text=[SOME_VALUE]...```<br/><b>[..."text=The+offer+title"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_bids_recommender_formulas.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L28)</b><br><b>[..."text=The+offer+title"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_bids_recommender_formulas.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L38)</b><br><b>[..."text=оффер"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_boost_express_offers.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L344)</b><br>

---

#### Cgi: <b>[tile](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1097)</b>
Описание:
 Tiles to find outlets on them<br/><b>Возвращаемое значение</b>: CGI-values &tile<br/>
Пример использования:
```example: &tile=[SOME_VALUE]...```<br/><b>[..."tile=617"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_multi_service_pickup.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L309)</b><br><b>[..."tile=619"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_geo.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L635)</b><br><b>[..."tile=619"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_geo.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L644)</b><br>

---

#### Cgi: <b>[title](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2051)</b>
Описание:
<b>Возвращаемое значение</b>: value of CGI-parameter &title<br/>https://st.yandex-team.ru/MARKETOUT-21270<br/>
Пример использования:
```example: &title=[SOME_VALUE]...```<br/><b>[..."title=Search"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_bids_recommender.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1257)</b><br>

---

#### Cgi: <b>[tl](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2721)</b>
Описание:
https://st.yandex-team.ru/MARKETRECOM-3556<br/>
Пример использования:
```example: &tl=[SOME_VALUE]...```<br/><b>[..."tl=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_dj_thematic_nid_response.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L117)</b><br><b>[..."tl=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_dj_pins.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L173)</b><br><b>[..."tl=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_dj_pins.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L209)</b><br>

---

#### Cgi: <b>[tld](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1368)</b>
Описание:
 Force TLD for request<br/>https://st.yandex-team.ru/MARKETOUT-11996<br/><b>Возвращаемое значение</b>: string with market top level domain for user<br/>
Пример использования:
```example: &tld=[SOME_VALUE]...```<br/>

---

#### Cgi: <b>[topic](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2324)</b>
Описание:
<b>Возвращаемое значение</b>: value of CGI-parameter &topic<br/>https://st.yandex-team.ru/MARKETRECOM-2839<br/>
Пример использования:
```example: &topic=[SOME_VALUE]...```<br/><b>[..."topic=topic9"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_dj_pins.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L325)</b><br>

---

#### Cgi: <b>[total-price](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2002)</b>
Описание:
<b>Возвращаемое значение</b>: value of CGI-parameter &total-price<br/> Total cart price including delivery and discount<br/><b>Заметка</b> Mandatory<br/>https://st.yandex-team.ru/MARKETOUT-24933<br/>
Пример использования:
```example: &total-price=[SOME_VALUE]...```<br/><b>[..."total-price="...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_actual_delivery_unified_tariffs.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L358)</b><br><b>[..."total-price="...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_actual_delivery_unified_tariffs.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L497)</b><br><b>[..."total-price="...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_actual_delivery_unified_tariffs.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L556)</b><br>

---

#### Cgi: <b>[touch](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L668)</b>
Описание:
<b>Возвращаемое значение</b>: value of CGI-parameter touch<br/> indicating wether request came from pad/phone or desktop<br/>
Пример использования:
```example: &touch=[SOME_VALUE]...```<br/><b>[..."touch=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_model_wizard.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L665)</b><br><b>[..."touch=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_model_wizard.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L958)</b><br><b>[..."touch=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_ugc.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L763)</b><br>

---

#### Cgi: <b>[trace-factor](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L98)</b>
Описание:
https://st.yandex-team.ru/MARKETOUT-25239<br/> Список факторов, значения которых нужно вернуть<br/>
Пример использования:
```example: &trace-factor=[SOME_VALUE]...```<br/><b>[..."trace-factor=FACTOR_XXX"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_factors_for_formula.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L484)</b><br><b>[..."trace-factor=SHOP_OPINION_COUNT"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_factors_for_formula.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L488)</b><br><b>[..."trace-factor=SHOP_OPINION_COUNT"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_factors_for_formula.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L512)</b><br>

---

#### Cgi: <b>[track-last-page](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L451)</b>
Описание:
https://st.yandex-team.ru/MARKETOUT-17101<br/><b>Возвращаемое значение</b>: value of &track-last-page=... CGI-parameter<br/>
Пример использования:
```example: &track-last-page=[SOME_VALUE]...```<br/><b>[..."track-last-page=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_prime.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L901)</b><br><b>[..."track-last-page=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_prime.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L907)</b><br><b>[..."track-last-page=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_prime.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L914)</b><br>

---

#### Cgi: <b>[treat-as-cpc-pessimization-category](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1163)</b>
Описание:
 TEMPORARY FLAG!!!<br/>
Пример использования:
```example: &treat-as-cpc-pessimization-category=[SOME_VALUE]...```<br/><b>[..."treat-as-cpc-pessimization-category=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_show_log.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L598)</b><br>

---

#### Cgi: <b>[trim-thumbs](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1705)</b>
Описание:
<b>Возвращаемое значение</b>: value of CGI parameter &trim-thumbs<br/> return trimmed thumbnails in pictures<br/>https://st.yandex-team.ru/MARKETOUT-16741<br/>
Пример использования:
```example: &trim-thumbs=[SOME_VALUE]...```<br/><b>[..."trim-thumbs=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_personal_categories.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1081)</b><br><b>[..."trim-thumbs=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_personal_categories.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1165)</b><br><b>[..."trim-thumbs=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_picture_filtering.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L206)</b><br>

---

#### Cgi: <b>[trying-available](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L211)</b>
Описание:
 Нужен для включения фильтрации офферов по признаку наличия примерки<br/> при trying-available=1 отображаются только офферы с примеркой<br/> при trying-available=0 отображаются все офферы вне зависимости от примерки<br/>https://st.yandex-team.ru/MARKETOUT-45489<br/><b>Возвращаемое значение</b>: value of CGI parameter "&trying-available"<br/><b>Заметка</b>: possible values (0(default),1)<br/>
Пример использования:
```example: &trying-available=[SOME_VALUE]...```<br/><b>[..."trying-available=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_trying_filter.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L291)</b><br><b>[..."trying-available=0"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_trying_filter.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L332)</b><br><b>[..."trying-available=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_trying_filter.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L359)</b><br>

---

#### Cgi: <b>[type](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1184)</b>
Описание:
 Returns type of requested bids recomendations.<br/><b>Возвращаемое значение</b>: CGI-value &type=<br/>
Пример использования:
```example: &type=[SOME_VALUE]...```<br/><b>[..."type=market_search"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_bids_recommender_formulas.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L38)</b><br><b>[..."type=card"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_bids_recommender_cpa_uncollapse.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L293)</b><br><b>[..."type=card"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_bids_recommender_cpa_uncollapse.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L363)</b><br>

---

#### Cgi: <b>[uid-type](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2101)</b>
Описание:
<b>Возвращаемое значение</b>: value of CGI-parameter &uid-type<br/>https://st.yandex-team.ru/MARKETOUT-26840<br/>
Пример использования:
```example: &uid-type=[SOME_VALUE]...```<br/><b>[..."uid-type=yandexuid"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_consolidate_log.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L329)</b><br>

---

#### Cgi: <b>[uid](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2106)</b>
Описание:
<b>Возвращаемое значение</b>: value of CGI-parameter &uid<br/>https://st.yandex-team.ru/MARKETOUT-26840<br/>
Пример использования:
```example: &uid=[SOME_VALUE]...```<br/><b>[..."uid=123456789"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_consolidate_log.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L329)</b><br>

---

#### Cgi: <b>[use-best-top](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1478)</b>
Описание:
 Render only top values for glfilter<br/>https://st.yandex-team.ru/MARKETOUT-13076<br/><b>Возвращаемое значение</b>: value of CGI parameter "&use-best-top"<br/>
Пример использования:
```example: &use-best-top=[SOME_VALUE]...```<br/><b>[..."use-best-top=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_top_glfilter_values.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L737)</b><br>

---

#### Cgi: <b>[use-blue-shard](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L407)</b>
Описание:
<b>Возвращаемое значение</b>: value of &use-blue-shard=... CGI parameter<br/> used in place=print_doc (default value: true if rgb=blue else false)<br/> debug parameter<br/>
Пример использования:
```example: &use-blue-shard=[SOME_VALUE]...```<br/>

---

#### Cgi: <b>[use-default-offers](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1618)</b>
Описание:
<b>Возвращаемое значение</b>: value of CGI parameter &use-default-offers<br/> Если выставлен, то в моделях будут дефолтные офферы<br/>
Пример использования:
```example: &use-default-offers=[SOME_VALUE]...```<br/><b>[..."use-default-offers=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_modelinfo_sku.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L103)</b><br><b>[..."use-default-offers=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_modelinfo_sku.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L181)</b><br><b>[..."use-default-offers=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_modelinfo_sku.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L405)</b><br>

---

#### Cgi: <b>[use-nid-for-search](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2745)</b>
Описание:
https://st.yandex-team.ru/MARKETOUT-40485<br/>
Пример использования:
```example: &use-nid-for-search=[SOME_VALUE]...```<br/><b>[..."use-nid-for-search=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_intents.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2800)</b><br><b>[..."use-nid-for-search=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_intents.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2848)</b><br><b>[..."use-nid-for-search=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_pruning_tbs_tpsz.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L643)</b><br>

---

#### Cgi: <b>[use-optimized-prime-prune-count](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1761)</b>
Описание:

Пример использования:
```example: &use-optimized-prime-prune-count=[SOME_VALUE]...```<br/>

---

#### Cgi: <b>[use-premium-offers](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1622)</b>
Описание:
<b>Возвращаемое значение</b>: value of CGI parameter &use-premium-offers<br/>
Пример использования:
```example: &use-premium-offers=[SOME_VALUE]...```<br/><b>[..."use-premium-offers=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_also_viewed.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L545)</b><br><b>[..."use-premium-offers=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_also_viewed.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L670)</b><br>

---

#### Cgi: <b>[use-relevance-in-bestsellers](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2344)</b>
Описание:
<b>Возвращаемое значение</b>: value of CGI-parameter &use-relevance-in-bestsellers<br/>https://st.yandex-team.ru/MARKETOUT-31666<br/>
Пример использования:
```example: &use-relevance-in-bestsellers=[SOME_VALUE]...```<br/><b>[..."use-relevance-in-bestsellers=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_prime_sorting.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1264)</b><br>

---

#### Cgi: <b>[use-rids-location](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L271)</b>
Описание:

Пример использования:
```example: &use-rids-location=[SOME_VALUE]...```<br/><b>[..."use-rids-location=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_pickup_modifiers.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L303)</b><br><b>[..."use-rids-location=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_pickup_modifiers.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L316)</b><br><b>[..."use-rids-location=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_pickup_modifiers.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L346)</b><br>

---

#### Cgi: <b>[use-simple-better-price](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1737)</b>
Описание:
<b>Возвращаемое значение</b>: use-simple-better-price<br/> for place=better_price<br/>
Пример использования:
```example: &use-simple-better-price=[SOME_VALUE]...```<br/><b>[..."use-simple-better-price="...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_better_price.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L278)</b><br>

---

#### Cgi: <b>[use-skus-in-jump-table](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L3008)</b>
Описание:
<b>Возвращаемое значение</b>: List of skus to add to jump-table<br/>https://st.yandex-team.ru/MARKETOUT-47598<br/>
Пример использования:
```example: &use-skus-in-jump-table=[SOME_VALUE]...```<br/><b>[..."use-skus-in-jump-table=2006"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_productoffers_sku.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L684)</b><br>

---

#### Cgi: <b>[use-text-search-factors](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2594)</b>
Описание:
<b>Возвращаемое значение</b>: value of CGI-parameter &use-text-search-factors<br/>https://st.yandex-team.ru/MARKETOUT-46557<br/>
Пример использования:
```example: &use-text-search-factors=[SOME_VALUE]...```<br/><b>[..."use-text-search-factors="...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_bert_service.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L177)</b><br><b>[..."use-text-search-factors=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_bert_service.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L183)</b><br>

---

#### Cgi: <b>[use_multiple_hyperid](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2081)</b>
Описание:
<b>Возвращаемое значение</b>: value of CGI-parameter &use_multiple_hyperid<br/>https://st.yandex-team.ru/MARKETOUT-27103<br/>
Пример использования:
```example: &use_multiple_hyperid=[SOME_VALUE]...```<br/><b>[..."use_multiple_hyperid=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_model_transitions.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L118)</b><br><b>[..."use_multiple_hyperid=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_model_transitions.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L125)</b><br><b>[..."use_multiple_hyperid=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_productoffers_multiple_hyperid.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L140)</b><br>

---

#### Cgi: <b>[user_type](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L489)</b>
Описание:
<b>Возвращаемое значение</b>: &user_type= parameter.<br/> Used for ABT. MARKETOUT-3772<br/>
Пример использования:
```example: &user_type=[SOME_VALUE]...```<br/><b>[..."user_type=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_show_log.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L917)</b><br><b>[..."user_type=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_show_log.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1005)</b><br><b>[..."user_type=moron"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_show_log.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1094)</b><br>

---

#### Cgi: <b>[utm_campaign](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1135)</b>
Описание:
<b>Возвращаемое значение</b>: value of &utm_campaign=... CGI-parameter<br/>
Пример использования:
```example: &utm_campaign=[SOME_VALUE]...```<br/><b>[..."utm_campaign=c"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_wizards.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L3489)</b><br><b>[..."utm_campaign=c"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_wizards.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L3493)</b><br><b>[..."utm_campaign=c"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_wizards.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L3497)</b><br>

---

#### Cgi: <b>[utm_medium](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1127)</b>
Описание:
<b>Возвращаемое значение</b>: value of &utm_medium=... CGI-parameter<br/>
Пример использования:
```example: &utm_medium=[SOME_VALUE]...```<br/><b>[..."utm_medium=cpc"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_model_wizard.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L741)</b><br><b>[..."utm_medium=cpc"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_model_wizard.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L747)</b><br><b>[..."utm_medium=cpc"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_model_offers_wizard.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L121)</b><br>

---

#### Cgi: <b>[utm_source](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1119)</b>
Описание:
<b>Возвращаемое значение</b>: value of &utm_source=... CGI-parameter<br/>
Пример использования:
```example: &utm_source=[SOME_VALUE]...```<br/><b>[..."utm_source=50"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_show_log.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1096)</b><br><b>[..."utm_source=54"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_show_log.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1259)</b><br><b>[..."utm_source=123\t456"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_show_log.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1418)</b><br>

---

#### Cgi: <b>[utm_source_service](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1123)</b>
Описание:
<b>Возвращаемое значение</b>: value of &utm_source_service=... CGI-parameter<br/>
Пример использования:
```example: &utm_source_service=[SOME_VALUE]...```<br/><b>[..."utm_source_service=img"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_place_images.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1320)</b><br><b>[..."utm_source_service=img"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_place_images.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1330)</b><br><b>[..."utm_source_service=web"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_click_log.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1546)</b><br>

---

#### Cgi: <b>[utm_term](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1131)</b>
Описание:
<b>Возвращаемое значение</b>: value of &utm_term=... CGI-parameter<br/>
Пример использования:
```example: &utm_term=[SOME_VALUE]...```<br/><b>[..."utm_term=term"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_wizards.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L3489)</b><br><b>[..."utm_term=term"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_wizards.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L3493)</b><br><b>[..."utm_term=term"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_wizards.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L3497)</b><br>

---

#### Cgi: <b>[uuid](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L346)</b>
Описание:
<b>Возвращаемое значение</b>: value of &uuid=... CGI-parameter(user id for mobile app)<br/>
Пример использования:
```example: &uuid=[SOME_VALUE]...```<br/><b>[..."uuid=10101"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_products_by_history.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L136)</b><br><b>[..."uuid=10101"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_products_by_history.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L138)</b><br><b>[..."uuid=10101"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_recommender.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L124)</b><br>

---

#### Cgi: <b>[validate-bundle](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1941)</b>
Описание:
https://st.yandex-team.ru/MARKETOUT-23686<br/>
Пример использования:
```example: &validate-bundle=[SOME_VALUE]...```<br/><b>[..."validate-bundle=0"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_promo_bundle.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L793)</b><br><b>[..."validate-bundle="...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_promo_secret_sale.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L415)</b><br>

---

#### Cgi: <b>[vbid-from](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1429)</b>
Описание:
 Filtering by vendor bid<br/>https://st.yandex-team.ru/MARKETOUT-11769<br/>
Пример использования:
```example: &vbid-from=[SOME_VALUE]...```<br/><b>[..."vbid-from=200"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_brand_products.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1240)</b><br><b>[..."vbid-from=0"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_brand_products.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1255)</b><br>

---

#### Cgi: <b>[vbid-to](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1434)</b>
Описание:
 Filtering by vendor bid<br/>https://st.yandex-team.ru/MARKETOUT-11769<br/>
Пример использования:
```example: &vbid-to=[SOME_VALUE]...```<br/><b>[..."vbid-to=210"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_brand_products.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1240)</b><br>

---

#### Cgi: <b>[vendor-max-values](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L739)</b>
Описание:
<b>Возвращаемое значение</b>: value of CGI-parameter &vendor-max-values if present or 10 if place=visual<br/>
Пример использования:
```example: &vendor-max-values=[SOME_VALUE]...```<br/><b>[..."vendor-max-values="...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_glparams_values.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L180)</b><br>

---

#### Cgi: <b>[vendor_id](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L735)</b>
Описание:
 Vendor identifier<br/><b>Заметка</b>: CGI-parameter vendor_id contains comma-separated vendor ID values<br/><b>Возвращаемое значение</b>: value of CGI-parameter &vendor_id<br/>
Пример использования:
```example: &vendor_id=[SOME_VALUE]...```<br/><b>[..."vendor_id=4"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_shop_vendor_promo_clicks_stats.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L94)</b><br><b>[..."vendor_id=5"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_shop_vendor_promo_clicks_stats.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L116)</b><br><b>[..."vendor_id=999"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_shop_vendor_promo_clicks_stats.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L155)</b><br>

---

#### Cgi: <b>[view-unique-id](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2427)</b>
Описание:
 Parameter to define recommendation block within a session<br/>https://st.yandex-team.ru/BLUEMARKET-11980<br/><b>Возвращаемое значение</b>: value of CGI parameter "&view-unique-id"<br/>
Пример использования:
```example: &view-unique-id=[SOME_VALUE]...```<br/><b>[..."view-unique-id=unique_id"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_dj_place.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L478)</b><br><b>[..."view-unique-id=view_unique_id_1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_dj_place.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L564)</b><br><b>[..."view-unique-id=view_unique_id_2"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_dj_place.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L565)</b><br>

---

#### Cgi: <b>[viewtype](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L722)</b>
Описание:
 Main search SERP type (grid/list), used for training ranking formulas.<br/>https://st.yandex-team.ru/MARKETVERSTKA-11151<br/>https://st.yandex-team.ru/MARKETOUT-5646<br/>
Пример использования:
```example: &viewtype=[SOME_VALUE]...```<br/><b>[..."viewtype=grid"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_ugc.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L377)</b><br><b>[..."viewtype=grid"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_ugc.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L812)</b><br><b>[..."viewtype=grid"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_ugc.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L848)</b><br>

---

#### Cgi: <b>[virt-shop](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1628)</b>
Описание:
<b>Возвращаемое значение</b>: value of CGI parameter &virt-shop<br/> to show supplier instead beru (for checkouter)<br/> default value: true<br/>
Пример использования:
```example: &virt-shop=[SOME_VALUE]...```<br/>

---

#### Cgi: <b>[visual-analogue-mix](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2955)</b>
Описание:
<b>Возвращаемое значение</b>: Add visual similar models to analogue place (place=also_viewed)<br/>https://st.yandex-team.ru/MARKETYA-737 and https://st.yandex-team.ru/MARKETSEARCH-810<br/>
Пример использования:
```example: &visual-analogue-mix=[SOME_VALUE]...```<br/><b>[..."visual-analogue-mix=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_also_viewed.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1222)</b><br><b>[..."visual-analogue-mix=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_also_viewed.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1257)</b><br><b>[..."visual-analogue-mix=0"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_also_viewed.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1286)</b><br>

---

#### Cgi: <b>[visual-similar-count](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2960)</b>
Описание:
<b>Возвращаемое значение</b>: Set up how many visual similar models will place=visual_search return<br/>https://st.yandex-team.ru/MARKETOUT-45337<br/>
Пример использования:
```example: &visual-similar-count=[SOME_VALUE]...```<br/><b>[..."visual-similar-count=4"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_dj.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2634)</b><br><b>[..."visual-similar-count=%d"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_visual_search.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L159)</b><br><b>[..."visual-similar-count=%d"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_visual_search.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L185)</b><br>

---

#### Cgi: <b>[wait-for-production-requests-to-stop](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2469)</b>
Описание:
 Wait for production requests to stop after closing report<br/><b>Возвращаемое значение</b>: value of CGI-parameter &wait-for-production-requests-to-stop<br/>
Пример использования:
```example: &wait-for-production-requests-to-stop=[SOME_VALUE]...```<br/><b>[..."wait-for-production-requests-to-stop=0"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_report_status.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L97)</b><br>

---

#### Cgi: <b>[waitall](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L945)</b>
Описание:
 Disables all known timeouts<br/><b>Возвращаемое значение</b>: CGI-value &waitall<br/>
Пример использования:
```example: &waitall=[SOME_VALUE]...```<br/><b>[..."waitall=da"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_merch_data_in_vendor_clicks.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L427)</b><br><b>[..."waitall=da"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_search_auction_mixed.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L93)</b><br><b>[..."waitall=da"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_search_auction_mixed.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L282)</b><br>

---

#### Cgi: <b>[warehouse_id](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1905)</b>
Описание:
 Switch to filter offers by warehouse<br/>https://st.yandex-team.ru/MARKETOUT-20875<br/>
Пример использования:
```example: &warehouse_id=[SOME_VALUE]...```<br/><b>[..."warehouse_id=147"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_dj.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2616)</b><br><b>[..."warehouse_id=2222"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_lms.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1827)</b><br>

---

#### Cgi: <b>[warehouses-per-business](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2894)</b>
Описание:
<b>Возвращаемое значение</b>: limit of warehouses per business for place parse_wh_compressed<br/>
Пример использования:
```example: &warehouses-per-business=[SOME_VALUE]...```<br/><b>[..."warehouses-per-business=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_get_eats_warehouses.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L205)</b><br><b>[..."warehouses-per-business=2"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_get_eats_warehouses.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L223)</b><br><b>[..."warehouses-per-business=0"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_get_eats_warehouses.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L242)</b><br>

---

#### Cgi: <b>[where](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L311)</b>
Описание:
<b>Возвращаемое значение</b>: &where cgi parameter<br/><b>Заметка</b>: to pass to ichwill<br/> https://st.yandex-team.ru/MARKETOUT-11899<br/>
Пример использования:
```example: &where=[SOME_VALUE]...```<br/>

---

#### Cgi: <b>[with-cpa-offers-first](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2126)</b>
Описание:
<b>Возвращаемое значение</b>: value of CGI-parameter &with_cpa_offers_first used in TPlaceBrandProducts place<br/>https://st.yandex-team.ru/MARKETOUT-37212<br/>
Пример использования:
```example: &with-cpa-offers-first=[SOME_VALUE]...```<br/><b>[..."with-cpa-offers-first=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_brand_products.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1890)</b><br><b>[..."with-cpa-offers-first=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_brand_products.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2227)</b><br><b>[..."with-cpa-offers-first=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_brand_products.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2364)</b><br>

---

#### Cgi: <b>[with-installments](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L223)</b>
Описание:

Пример использования:
```example: &with-installments=[SOME_VALUE]...```<br/>

---

#### Cgi: <b>[with-rebuilt-model](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L979)</b>
Описание:
https://st.yandex-team.ru/MARKETOUT-7705<br/> Enables successor clusters on visual and visualcard places<br/><b>Возвращаемое значение</b>: CGI-value &with-rebuilt-model<br/>
Пример использования:
```example: &with-rebuilt-model=[SOME_VALUE]...```<br/><b>[..."with-rebuilt-model=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_compare_products.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1171)</b><br><b>[..."with-rebuilt-model=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_compare_products.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1200)</b><br><b>[..."with-rebuilt-model=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_compare_products.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1204)</b><br>

---

#### Cgi: <b>[with-services](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2794)</b>
Описание:
<b>Возвращаемое значение</b>: value of CGI parameter &with-services<br/> Disable/enable filter by order services<br/>https://st.yandex-team.ru/MARKETOUT-40717<br/>
Пример использования:
```example: &with-services=[SOME_VALUE]...```<br/><b>[..."with-services="...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_services.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L860)</b><br><b>[..."with-services="...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_services.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L882)</b><br><b>[..."with-services="...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_services.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L895)</b><br>

---

#### Cgi: <b>[with-yandex-delivery](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L214)</b>
Описание:

Пример использования:
```example: &with-yandex-delivery=[SOME_VALUE]...```<br/><b>[..."with-yandex-delivery=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_prime.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L7185)</b><br>

---

#### Cgi: <b>[without-clones](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L603)</b>
Описание:
 Return shops without clones (for place=shops_list)<br/><b>Возвращаемое значение</b>: value of CGI-parameter &without-clones<br/>
Пример использования:
```example: &without-clones=[SOME_VALUE]...```<br/><b>[..."without-clones=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_shops_list.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L176)</b><br>

---

#### Cgi: <b>[wizard-rules](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L314)</b>
Описание:

Пример использования:
```example: &wizard-rules=[SOME_VALUE]...```<br/><b>[..."wizard-rules="...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_model_wizard.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L699)</b><br><b>[..."wizard-rules="...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_offers_wizard.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L965)</b><br><b>[..."wizard-rules="...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_parallel.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L117)</b><br>

---

#### Cgi: <b>[wprid](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L642)</b>
Описание:
<b>Возвращаемое значение</b>: value of CGI-parameter wprid<br/>
Пример использования:
```example: &wprid=[SOME_VALUE]...```<br/><b>[..."wprid=1123456789"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_parallel.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1974)</b><br><b>[..."wprid=cb8f7a995444ab4dc3215cad33fcd6bb"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_parallel.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2241)</b><br><b>[..."wprid=cb8f7a995444ab4dc3215cad33fcd6bb"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_parallel.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2276)</b><br>

---

#### Cgi: <b>[x-yandex-encrypted-icookie](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1583)</b>
Описание:
<b>Возвращаемое значение</b>: value of CGI parameter &x-yandex-encrypted-icookie<br/>https://st.yandex-team.ru/MARKETOUT-40773<br/>
Пример использования:
```example: &x-yandex-encrypted-icookie=[SOME_VALUE]...```<br/><b>[..."x-yandex-encrypted-icookie=1123456"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_parallel.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2241)</b><br><b>[..."x-yandex-encrypted-icookie=1123456"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_parallel.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2276)</b><br><b>[..."x-yandex-encrypted-icookie=1123456"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_parallel_products.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2255)</b><br>

---

#### Cgi: <b>[x-yandex-icookie](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1573)</b>
Описание:
<b>Возвращаемое значение</b>: value of CGI parameter &x-yandex-icookie<br/>https://st.yandex-team.ru/MARKETOUT-16248<br/>
Пример использования:
```example: &x-yandex-icookie=[SOME_VALUE]...```<br/><b>[..."x-yandex-icookie=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_promo_personalization.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L82)</b><br><b>[..."x-yandex-icookie=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_promo_personalization.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L83)</b><br><b>[..."x-yandex-icookie=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_promo_personalization.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L97)</b><br>

---

#### Cgi: <b>[x-yandex-src-icookie](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1578)</b>
Описание:
<b>Возвращаемое значение</b>: value of CGI parameter &x-yandex-src-icookie<br/>https://st.yandex-team.ru/MARKETFRONT-35776<br/>
Пример использования:
```example: &x-yandex-src-icookie=[SOME_VALUE]...```<br/><b>[..."x-yandex-src-icookie=7111647341623827291"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_click_log.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1546)</b><br><b>[..."x-yandex-src-icookie=7111647341623827291"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_show_log.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1737)</b><br>

---

#### Cgi: <b>[ya-card-max-cashback](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2213)</b>
Описание:
 Max amount for Yandex Card cashback<br/>https://st.yandex-team.ru/MARKETOUT-46822<br/>
Пример использования:
```example: &ya-card-max-cashback=[SOME_VALUE]...```<br/><b>[..."ya-card-max-cashback=100"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_blue_promo_blue_cashback.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L3757)</b><br><b>[..."ya-card-max-cashback=100"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_blue_promo_blue_cashback.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L3807)</b><br>

---

#### Cgi: <b>[ya-card-max-offer-price](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2221)</b>
Описание:
 Max price for offer to have Yandex Card cashback<br/>
Пример использования:
```example: &ya-card-max-offer-price=[SOME_VALUE]...```<br/><b>[..."ya-card-max-offer-price=4001"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_blue_promo_blue_cashback.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L3810)</b><br><b>[..."ya-card-max-offer-price=3999"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_blue_promo_blue_cashback.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L3815)</b><br>

---

#### Cgi: <b>[ya-card-promo-id](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2217)</b>
Описание:
 Promo Id for Yandex Card cashback<br/>
Пример использования:
```example: &ya-card-promo-id=[SOME_VALUE]...```<br/><b>[..."ya-card-promo-id="...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_blue_promo_blue_cashback.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L3757)</b><br><b>[..."ya-card-promo-id="...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_blue_promo_blue_cashback.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L3807)</b><br><b>[..."ya-card-promo-id="...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_blue_promo_blue_cashback.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L3808)</b><br>

---

#### Cgi: <b>[ya-card-share](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2208)</b>
Описание:
 Share of Yandex Card cashback<br/>https://st.yandex-team.ru/MARKETOUT-46822<br/>
Пример использования:
```example: &ya-card-share=[SOME_VALUE]...```<br/><b>[..."ya-card-share=0.5"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_blue_promo_blue_cashback.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L3757)</b><br><b>[..."ya-card-share=0.5"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_blue_promo_blue_cashback.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L3807)</b><br><b>[..."ya-card-share=0.5"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_blue_promo_blue_cashback.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L3808)</b><br>

---

#### Cgi: <b>[yaca, cat2marketbind](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L705)</b>
Описание:
 Describes path in catalog<br/><b>Возвращаемое значение</b>: CGI-parameter &yaca or &cat2marketbind<br/>
Пример использования:
```example: &yaca=[SOME_VALUE]...```<br/>```example: &cat2marketbind=[SOME_VALUE]...```<br/>

---

#### Cgi: <b>[yamarec-place-id](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2965)</b>
Описание:
<b>Возвращаемое значение</b>: Name of section in yamarec.conf (right now used for place=also-viewed)<br/>https://st.yandex-team.ru/MARKETRECOM-4975<br/>
Пример использования:
```example: &yamarec-place-id=[SOME_VALUE]...```<br/><b>[..."yamarec-place-id=also-viewed-express"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_express_delivery.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L4687)</b><br><b>[..."yamarec-place-id="...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_also_viewed.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1393)</b><br><b>[..."yamarec-place-id=also-viewed-express"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_also_viewed.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1418)</b><br>

---

#### Cgi: <b>[yandexgid](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2356)</b>
Описание:
<b>Возвращаемое значение</b>: value of CGI-parameter &yandexgid<br/> It is region id set in yandex_gid cookie<br/>https://wiki.yandex-team.ru/geolocation/cookies<br/>
Пример использования:
```example: &yandexgid=[SOME_VALUE]...```<br/><b>[..."yandexgid=2"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_click_n_collect.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L700)</b><br>

---

#### Cgi: <b>[yandexuid](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L338)</b>
Описание:
<b>Возвращаемое значение</b>: value of &yandexuid=... CGI-parameter (user id for web)<br/>
Пример использования:
```example: &yandexuid=[SOME_VALUE]...```<br/><b>[..."yandexuid=001"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_analogs_with_also_viewed.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L49)</b><br><b>[..."yandexuid=1"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_articles.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L120)</b><br><b>[..."yandexuid=2"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_articles.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L139)</b><br>

---

#### Cgi: <b>[yp](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2362)</b>
Описание:
<b>Возвращаемое значение</b>: value of CGI-parameter &yp<br/> It is yp cookie value<br/>https://wiki.yandex-team.ru/Cookies/Y<br/>
Пример использования:
```example: &yp=[SOME_VALUE]...```<br/><b>[..."yp=iamyp"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_click_n_collect.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L700)</b><br>

---

#### Cgi: <b>[zoom](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L1087)</b>
Описание:
 Parameter for point coordinates adjusting in geo output<br/><b>Возвращаемое значение</b>: CGI-values &zoom<br/>
Пример использования:
```example: &zoom=[SOME_VALUE]...```<br/><b>[..."zoom=10"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_multi_service_pickup.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L309)</b><br><b>[..."zoom=10"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_cpa_category_geo.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L169)</b><br><b>[..."zoom=10"...](https://a.yandex-team.ru/arc_vcs/market/report/lite/test_cpa_category_geo.py?rev=20450873c10bb360c6907a893e6bd65badbdb721#L205)</b><br>

---

#### Cgi: <b>[сategory-mix-saturation](https://a.yandex-team.ru/arc_vcs/market/report/library/cgi/params.h?rev=20450873c10bb360c6907a893e6bd65badbdb721#L2717)</b>
Описание:
https://st.yandex-team.ru/MARKETYA-12<br/>
Пример использования:
```example: &сategory-mix-saturation=[SOME_VALUE]...```<br/>

---

