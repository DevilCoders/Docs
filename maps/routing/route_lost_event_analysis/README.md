В этом каталоге содержатся инструменты для классификации и визуализации ситуаций, когда пользователи Навигатора съезжали с маршрута. Для работы с инструментами необходим YT token.

Посчитать статистику и собрать примеры маршрутов для визуализации можно приблизительно так:

    ./classifier/bin/classifier/classifier \
        --cluster hahn \
        --date 2019-07-01 \
        --graph-version 2019-07-01-0 \
        --summary-table //home/maps/users/"$USER"/route-lost-summary \
        --sample-table //home/maps/users/"$USER"/route-lost-samples

После этого можно запустить визуализацию:

    YCR_MODE=http:8088 ./visualize_data/visualize_data \
        --summary-table //home/maps/users/"$USER"/route-lost-summary \
        --sample-table //home/maps/users/"$USER"/route-lost-samples \
        --graph /var/spool/yandex/maps/graph/19.07.01-0/road_graph.fb \
        --rtree /var/spool/yandex/maps/graph/19.07.01-0/rtree.fb

На машинке на указанном порту будет запущен HTTP-сервер, возвращающий страницу view.html по соответствующему URL-у. На странице показываются места, в которых происходит достаточное количество сходов. Для каждого места выводится информация о том, сколько сходов произошло за день и сколько в среднем теряют/выигрывают времени люди, сойдя с маршрута. По каждому месту можно посмотреть примеры конкретных случаев сходов. В примерах синим цветом обозначены маршруты, с которых происходит сход, красным — траектории движения пользователей, тёмно-серым — маршруты, предложенные пользователям после схода.

Результаты регулярной классификации можно посмотреть на [этом dashboard-е](https://datalens.yandex-team.ru/dashboards/qib8jq30j2com-route-lost-event-classification).
