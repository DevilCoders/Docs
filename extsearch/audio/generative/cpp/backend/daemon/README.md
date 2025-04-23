### Что это
Демон бэкэнда генеративной музыки. Умеет генерировать генеративный HLS поток по заданным жанру и температуре.

### Что нужно сделать перед тем, как запустить 

Единственный системный пререквезит для локального запуска генеративного демона - установленный redis.
Пойдёт с дефолтными настройками

Ещё нужно подготовить файлы с данными лупов и предгенерированных трэков.
Для этого надо собрать extsearch/audio/generative/cpp/backend/tools/loops_exporter
и extsearch/audio/generative/cpp/backend/tools/pregen_exporter.
Запустить из директории демона:

    ya make ../extsearch/audio/generative/cpp/backend/tools/loops_exporter
    ya make ../extsearch/audio/generative/cpp/backend/tools/pregen_exporter
    ../tools/loops_exporter/loops_exporter data/loopsinfo.pb
    ../tools/pregen_exporter/pregen_exporter data/pregeninfo.pb

### Как запустить
 
В целом всё почти готово для запуска. Нужно попросить меня дать доступ к секрету и понеслась:  

    export GENERATIVE_S3_LOOPS_SECRET=`ya vault get version -o loops_s3_secret ver-01eg8mrgsyfsgf6w6x3ar1t0jh`
    ./generative_daemon generative_daemon_local.json  

### Как получить HLS ссылку

Для этого есть ручка /generative/get_stream в которую нужно запостить json параметрами запрашиваемого стрима.
Например так:

    json='{"params":{"genre":"rock", "temperature":3, "adaptive":true, "manual":true}, "version":"1.0"}'
    hlsUrl=`curl -X POST http://localhost:8080/generative/get_stream -d "$json" | jq -r .stream.url` 

Если нет jq или подобной утилитки, то прийдётся написать на любимом скриптовом языке небольшой helper.

Полученный url можно например запустить через gstreamer:

    gst-launch-1.0 souphttpsrc is-live=true do-timestamp=true "location=$hlsUrl" ! hlsdemux ! decodebin ! audioconvert ! pulsesink

### Что-то воспроизведение заикается

Лупы загружаются с тестового s3, он может тормозить. Пока кэш более-менее не заполнится, будет иногда притормаживать, увы.


### Обновление data/project_tags.json 

Скрипт лежит в extsearch/audio/generative/py/tools/check_and_export_tags.py инструкция внутри
