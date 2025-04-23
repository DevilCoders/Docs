Это папка с исполняемыми в огородных модулях скриптах с целью варки данных:

<code>

- [add_lines_uri][1] - Патчит текстовый файл "routes" из masstransit_data_rasp, добавляя туда *uri маршрутов* ОТ из masstransit_data
- [build_pedestrian_transfers][2] - Строит пересадки между остановками одной компоненты из flatbuffer в tsv
- [build-stops-binding][3] - Привязывает остановки к пешеходному графу.
- [tsv_to_fb][4] - Переваривает данные из сырого вида во FlatBuffer (для ускорения запуска роутеров)
- [validate-mtdata][5] - Инициализирует Masstransit. Проверяет, что конструктор не падает
- [validate-pedestran-graph][6] - Проверка PedestrianGraph. Проверяет, что конструктор не падает.


[1]: ./add_lines_uri                    ""
[2]: ./build_pedestrian_transfers       ""
[3]: ./build-stops-binding              ""
[4]: ./tsv_to_fb                        ""
[5]: ./validate-mtdata                  ""
[6]: ./validate-pedestrian-graph        ""


</code>
