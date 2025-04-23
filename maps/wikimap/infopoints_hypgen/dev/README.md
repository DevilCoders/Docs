# HOWTO

Черновик сервиса, извлекающего полезный сигнал из инфоточек.
На wiki читать https://wiki.yandex-team.ru/Users/pkostikov/infopoints_analyzer/

## Получение исходных данных

Тулза restore_infopoints из пакета yandex-maps-infopoint-statistic

e.g.
/usr/lib/yandex/maps/infopoint/restore_infopoints/maps/infopoint/statistic/bin/restore_infopoints/restore_infopoints --format=table --begin 20171201T000000 --end 20171202T000000 > 20171201.20171202.raw.tsv

С этого формата начинается работа текущего прототипа

## Что дальше можно делать

migrations - схема БД, в которую пишутся события и гипотезы

dispatcher - на вход получает исходные данные, пробегает по ним и заполняет базу событиями и гипотезами
e.g.
time ./dispatcher ~/tmp/20171201.20171202.raw.tsv [output_for_feedback_import.tsv]

viewer - yacare сервис, который дает доступ к содержимому базы
e.g.
YCR_MODE=http:8080 ./viewer
curl -X GET -vs 'http://localhost:8080/event/55161'
curl -X GET -vs 'http://localhost:8080/hypothesis/1'

easyview_dumper - выгружает содержимое базы в формате, понятном easyview
e.g.
./easyview_dumper easyview.tsv


# TODO

## По функциональности
- достичь качества гипотез, сравнимого с предыдущей версией (? как померить)
- разбить на 2 потока: шлагбаумы и все остальное
- реализовать доставку до НЯК
- регулярная выгрузка

## По коду
- фильтр интересных инфоточек по тексту через boost::regex
- логирование правильное
- уйти от зависисмости от библиотек wikimap
- сохранять всю информацию об инфоточке в базе, чтобы можно было добавлять факторы легко
- сделать конфиг, сейчас не до конца, конфиги сразу ресурсами
- перейти на sql chemistry

## Фичи
- трек как-то выгребать - можно и потом
- учет регионов
- +1 бинарник: по базе сделать датасет, дальше надо как-то учить

