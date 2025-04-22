## Построение оффлайн базы для RsyaSimilarBanners

* запустить https://yql.yandex-team.ru/Operations/XKUD6Z3udoXsaYCDd9E2-Mm6Soi2j_6dLmO6TZwYVxQ=

* скачать dssm модели
    * для кластеризации (два баннера, кликнутых в одном поисковом хите, граф обучения https://nirvana.yandex-team.ru/flow/26e131f6-f021-4232-bb00-21ed5d4f64d6/d5cfc8ec-1a0f-4bfa-80db-dbf2930f9d81/graph/FlowchartBlockOperation/799a1a8b-9ca8-4828-9481-b01a7ab49099):
        * `bannerVSbanner.dssm` - https://proxy.sandbox.yandex-team.ru/901192336
        * `bannerVSbanner.appl` - https://proxy.sandbox.yandex-team.ru/901194611
    * для предсказания похожего на кликнутый в РСЯ (граф обучения https://nirvana.yandex-team.ru/flow/8bc13ede-df59-49d4-92f6-a397ee1c0720/4202bcd6-c5ab-413a-80b8-6e8569d022da/graph/FlowchartBlockOperation/aea34145-95d5-42c7-8483-b6aae5fddec2):
        * `nextBannerRelevance.dssm` - https://sandbox.yandex-team.ru/resource/901175211/view

* Построить кластеры: \
`` 
multiclusters train --proxy hahn 
--input //home/bs/users/jruziev/rsya_similar_banners/auction/1show 
--embed_model_path bannerVSbanner.dssm 
--output_model_path bannerVSbanner.kmeans 
--num_iters 100,100 --memory_limits 51,51 --num_clusters 1000,1000 
--min_cluster_weight 100,10 --num_threads 10,1 
--max_data_size_for_learning 2000000,2000000 
--working_dir //home/bs/users/jruziev/rsya_similar_banners/auction/cluster_build.work 
--input_columns CleanBannerTitle,CleanBannerText,StrippedGoodURL,GoodURLUta 
--dssm_fields banner_title_1,banner_text_1,stripped_goodurl_1,goodurl_uta_1 
--state_path state 
--weight_column SqrtShows
 ``

* Разметить другую таблицу кластерами: \
``
multiclusters assign 
--proxy hahn 
--input //home/bs/users/jruziev/rsya_similar_banners/auction/1show 
--embed_model_path bannerVSbanner.dssm 
--cluster_model_path bannerVSbanner.kmeans 
--output_table //home/bs/users/jruziev/rsya_similar_banners/auction/1show.clustered
--input_columns CleanBannerTitle,CleanBannerText,StrippedGoodURL,GoodURLUta 
--dssm_fields banner_title_1,banner_text_1,stripped_goodurl_1,goodurl_uta_1 
--assign_stage 2
``

* Оставляем в каждом кластере по одному представителю: \
``
takeN.py 
--src //home/bs/users/jruziev/rsya_similar_banners/auction/1show.clustered 
--dst //home/bs/users/jruziev/rsya_similar_banners/auction/1show.clustered.take1 
--group-keys ClusterID 
-n 1
``

* Скачиваем кластеры: \
``
ytread 
--noloop -i //home/bs/users/jruziev/rsya_similar_banners/auction/1show.clustered.take1 
-c ClusterID,CleanBannerTitle,CleanBannerText,StrippedGoodURL,GoodURLUta > clusters.tsv
``

* Скачиваем баннеры, которые будут участвовать в аукционе: \
``
ytread 
--noloop -c BannerID,NumShows,DomainID,CleanBannerTitle,CleanBannerText,StrippedGoodURL,GoodURLUta,LogMoney,RegionPattern 
-i //home/bs/users/jruziev/rsya_similar_banners/auction/1show > banners.tsv
``

* Проводим двойной аукцион: \
``
cat clusters | 
fastrank2 --conf auction.conf 
--num_inputs `wc -l clusters | awk -F ' ' '{print $1}'` > offline_auction.tsv
``

* Опционально можно записать табличку на YT \
``
cat offline_auction.tsv | 
yt write 
--table //home/bs/users/jruziev/rsya_similar_banners/auction/offline_auction
--format '<columns=["score";"ClusterID";"BannerID";"RegionPattern";"BannerTitle"];enable_type_conversion=%true>schemaful_dsv'
``

* по порогу отсечь оффлайн базу (текущий порог >2)

* собрать в сендбокс ресурс типа RSYA_SIMILAR_BANNERS_BASES файлы:
    * geodata6.bin
    * bannerVSbanner.appl
    * bannerVSbanner.kmeans
    * offline_auction.tsv

    В зависимости от released=testing/stable база раскатится в тестовый или продакшн контур rsya_similar_banners
