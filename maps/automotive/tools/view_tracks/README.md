# Просмотр треков

Скрипт собирает треки для указанной машины за выбранный день и выводит их в stdout в виде tsv для easyview.
* исходные данные `//home/maps/automotive/crossmatch/daily/telematics_matched_path`
* исходные данные `//home/maps/automotive/crossmatch/daily/not_matched_telematics`
* исходные данные `//home/maps/automotive/crossmatch/daily/not_matched_jams`
* на stdout выдаёт tsv для easyview

## Параметры

* ```--build-not-matched``` - optional - включает режим расчёта для несматченных пар машина-гу. Для работы необходимо указать ```--imei``` машины и ```--head-id``` головного устройства.
* ```--car-id``` - optional - id машины, для которой готовятся треки
* ```--imei``` - optional - imei машины, для которой готовятся треки (используется вместе с ```--build-not-matched```)
* ```--head-id``` - optional - id ГУ, для которой готовятся треки (используется вместе с ```--build-not-matched```)
* ```--date```  - optional (default: вчера) - дата, за которую готовим треки
* ```--source-path``` -  optional (default: //home/maps/automotive/crossmatch/daily) - кастомный путь до табличек telematics_matched_path

## How to use?

1) Надо получить YQL_TOKEN [тут](http://yql.yandex-team.ru/?settings_mode=token) и добавить его в env ```export YQL_TOKEN=<token>```
2) Собрать easyview: ```cd maps/tools/easyview/bin && ya make``` (пути для корня аркадии).
Можно сразу сделать алиас, чтобы было удобней запускать: ```echo alias easyview=\"~/arcadia/maps/tools/easyview/bin/easyview\" >> ~/.bashrc```
3) Собрать и запустить сам view_tracks

## Примеры

* ```./automotive-crossmatch-view-tracks --car-id 91c30149-e870-1533-42ec-7393c24afdc9 --date 2019-12-11 > В820ХТ75020191211.tsv``` -
собрать треки для car_id 91c30149-e870-1533-42ec-7393c24afdc9 и положить их в файл ```В820ХТ75020191211.tsv```.
Потом файл можно отправить в easyview: ```cat В820ХТ75020191211.tsv | easyview```
* ```automotive-crossmatch-view-tracks --car-id f469884b-7310-43a6-b38c-f7a59434fa91 | easyview``` -
собрать треки для car_id f469884b-7310-43a6-b38c-f7a59434fa91 за предыдущий день и отобразить их в easyview
* ```automotive-crossmatch-view-tracks --build-not-matched --date 2020-05-27 --head-id fcc2de063ac6 --imei 867962043848822  | easyview``` -
собрать треки для imei 867962043848822 и head_id fcc2de063ac6 за 2020-05-27 и отобразить их в easyview
