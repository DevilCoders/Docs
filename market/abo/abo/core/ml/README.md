## МЛ в або

###  Подготовка данных
подправить папку куда сохранять и запустить запрос
```
ya yql -i train.yql hahn
```

### Notebook

```
#ya tool yt read //home/market/production/abo/ml/imelnikov/2021-04-09 --format tsv
catboost fit -f <file> --cd train.cd --has-header --cv "Classical:0;5" --cv-no-shuffle

# feature importance
catboost fstr -m model.bin -o importance.txt
```

### Статус

#### 2021-05-12 - currency rate day, week, month
`999:	learn: 0.3051664	test: 0.3578306	best: 0.3551460 (182)	total: 12.2s	remaining: 0us`

**Importance**
```angular2html
4:  4.190204939	currency_rate_week
5:  3.987252199	currency_rate_day
13: 2.952284144	currency_rate_month
```
#### 2021-04-30 - currency rate diff
`999:	learn: 0.2804124	test: 0.3821715	best: 0.3766722 (141)	total: 9.34s	remaining: 0us`

**Importance**
```2.807563638	currency_rate_diff```

#### 2021-04-20 - shop params
`999:	learn: 0.2734633	test: 0.3736166	best: 0.3689422 (169)	total: 7.27s	remaining: 0us`

**Importance**
New features are zero. Maybe there is a bug in stored data

#### 2021-04-12 - weekday
`999:	learn: 0.2613921	test: 0.3719702	best: 0.3643901 (130)	total: 6.24s	remaining: 0us`

**Importance**
```angular2html
7.824534476	clicks_shop
5.549249503	model_shops
5.4461266	age
4.620752387	model_cat_shops
4.195380995	cat_models
4.054703708	model_clicks_model
3.751397641	critical_tickets
3.417945531	model_clicks_shop
3.401395757	model_offers
3.134688696	title
3.078951462	price
2.956095974	price_to_median
2.953403867	critical
2.935736813	cat_min_price
2.877225222	cat_vendors
2.867056464	model_median_price
2.806334145	cat_avg_price
2.743685886	cat_shops
2.726385949	clicks_shop_category
2.574074687	price_to_average
2.551277629	clicks_model
2.47189027	model_cat_offers
2.431381929	model_click_shop_model
2.277196734	model_click_category
2.224019353	week_day
2.199694921	tickets
2.150066499	cat_offers
2.130263952	model_min_price
1.940031416	description
1.91455395	clicks_category
1.416551402	model_avg_price
0.90506344	resolved_tickets
0.7702814962	resolved
0.7026012467	clicks_shop_model
0	cat_avg_fee
```

#### 2021-04-11 - rm week features
`999:	learn: 0.2571284	test: 0.3728486	best: 0.3629333 (46)	total: 3.61s	remaining: 0us`

**Importance**
```angular2html
10.2598202	clicks_shop
8.940208311	critical_tickets
8.551969612	model_shops
5.890834009	model_offers
4.878410368	tickets
4.865155798	critical
4.210604183	price_to_median
4.063604546	age
4.044702742	model_cat_shops
3.249376024	cat_models
2.923194201	model_clicks_model
2.751143942	clicks_shop_category
2.576737379	cat_avg_price
2.574186611	model_click_category
2.566560861	title
2.462199723	model_click_shop_model
2.387857053	clicks_category
2.277640672	cat_vendors
2.240875612	cat_offers
2.233487605	model_clicks_shop
2.193563299	cat_shops
2.103722431	model_cat_offers
1.929213854	model_min_price
1.602076599	resolved_tickets
1.461899058	clicks_model
1.205985128	model_avg_price
1.106018593	price_to_average
0.9431586816	model_median_price
0.8708149033	clicks_shop_model
0.8462004544	cat_min_price
0.8309109719	description
0.6602791265	resolved
0.2975874452	price
0	cat_avg_fee
```


#### 2021-04-11 - 100 days + no-shuffle
`999:	learn: 0.2602756	test: 0.3653074	best: 0.3573533 (164)	total: 3.61s	remaining: 0us`

**Importance**
```angular2html
5.967515318	age
5.634969303	clicks_shop
4.689132814	model_offers
4.379876793	critical
4.124875165	model_cat_shops
4.01828797	cat_avg_price
3.980874767	cat_vendors
3.907085933	model_shops
3.566387105	price_to_median
3.549269478	critical_tickets
3.454421582	cat_models
3.38801938	model_cat_offers
3.355986192	clicks_shop_category
3.271605974	cat_shops
3.227545974	tickets
3.113786998	title
3.070803116	model_clicks_shop
3.006700255	price_to_average
2.954959197	model_click_category
2.952257404	clicks_model
2.951513498	cat_offers
2.624554283	price
2.355576957	model_click_shop_model
2.302744292	model_clicks_model
2.174115064	model_median_price
1.821545409	model_avg_price
1.573569281	clicks_category
1.564627212	description
1.539829202	resolved
1.495013074	model_min_price
1.379117087	resolved_tickets
1.303934066	cat_min_price
1.220933755	clicks_shop_model
0.07856609989	ping_enabled
0	own_region
0	cat_avg_fee
```

#### 2021-04-10 - is_offer_blue=false
**Ошибка**
`999:	learn: 0.3058920	test: 0.3577871	best: 0.3552179 (108)	total: 5.95s	remaining: 0us`

**Importance**
```
5.921659826	age
5.369410273	clicks_shop
5.107676389	description
4.938732145	title
4.933053643	price_to_average
4.119952994	price_to_median
4.041152485	model_min_price
3.911086909	cat_avg_price
3.708469329	clicks_model
3.462960037	model_cat_offers
3.386786158	model_cat_shops
3.177028578	model_click_category
3.092772601	cat_avg_fee
3.059607158	model_clicks_shop
2.896408052	price
2.79971438	cat_vendors
2.772596775	cat_shops
2.66595721	model_shops
2.609736689	tickets
2.608362359	clicks_category
2.583849168	model_avg_price
2.488354893	cat_offers
2.429484735	cat_models
2.426873555	model_offers
2.318890102	critical_tickets
1.976997233	model_median_price
1.884458591	clicks_shop_category
1.848215346	model_clicks_model
1.600495446	model_click_shop_model
1.541440878	cat_min_price
1.155917477	resolved
1.113857965	clicks_shop_model
0.8921924109	critical
0.854208941	resolved_tickets
0.3016392666	ping_enabled
0	own_region
```

#### 2021-04-09 - initial
**Ошибка**
  `999:	learn: 0.3075753	test: 0.3575176	best: 0.3541102 (167)	total: 5.09s	remaining: 0us`

**Importance**
```angular2html
5.921659826	age
5.369410273	clicks_shop
5.107676389	description
4.938732145	title
4.933053643	price_to_average
4.119952994	price_to_median
4.041152485	model_min_price
3.911086909	cat_avg_price
3.708469329	clicks_model
3.462960037	model_cat_offers
3.386786158	model_cat_shops
3.177028578	model_click_category
3.092772601	cat_avg_fee
3.059607158	model_clicks_shop
2.896408052	price
2.79971438	cat_vendors
2.772596775	cat_shops
2.66595721	model_shops
2.609736689	tickets
2.608362359	clicks_category
2.583849168	model_avg_price
2.488354893	cat_offers
2.429484735	cat_models
2.426873555	model_offers
2.318890102	critical_tickets
1.976997233	model_median_price
1.884458591	clicks_shop_category
1.848215346	model_clicks_model
1.600495446	model_click_shop_model
1.541440878	cat_min_price
1.155917477	resolved
1.113857965	clicks_shop_model
0.8921924109	critical
0.854208941	resolved_tickets
0.3016392666	ping_enabled
0	own_region
```


### Идеи
- распределение цен в категориях, моделях, магазинах
    avg, min, max
    median, 10percentile, 90percentile
- биды из оферов
    какие виды ставок есть
- курс валюты, погода, пробки за день
- цена офера к модели в диапазоне `(price - min_price)/(median_price - min_price)`
- ✅ только 3 мес - !!качество не просело!!
- категории высокого уровня, а не листовые
- ✅ убрать слабые фичи (own_region, ping_enabled)
- обновить ml_shop_data
- ✅ день недели, день месяца, час дня


### Почитать
- https://yt.yandex-team.ru/docs/quickstart
- https://catboost.ai/docs/concepts/cli-reference_train-model.html
- https://github.yandex-team.ru/imelnikov/genboost
- https://wiki.yandex-team.ru/users/imelnikov/ml/

