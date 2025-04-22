## YT


### Репликация данных с Hahn на Arnold

[Тикет](https://st.yandex-team.ru/GEOANALYTICS-1810)

[Скрипт](https://a.yandex-team.ru/arc_vcs/maps/analytics/tools/yt/replicator)

[Реактор](https://reactor.yandex-team.ru/browse/resolve?path=%2Fmaps%2Fanalytics%2Ftools%2Fyt%2Freplicate%2Fdaily)

Бывают таблички с очень большим кол-вом чанков. В итоге они очень очень долго копируются. Надо для таких табличек схлопывать чанки.
Можно через YT утилиту, например, для `//home/maps/analytics/data/metro-jams/data_rates_log` запустить:
```
yt merge 
  --src //home/maps/analytics/data/metro-jams/data_rates_log
  --dst //home/maps/analytics/data/metro-jams/data_rates_log 
  --spec '{combine_chunks=true;mode=ordered;pool=maps-analytics}' 
  --proxy hahn
```

При даунтайме Хана нужно: 
- отключить репликацию (остановить реакцию)
- заменить наши 2 подключения ([раз](https://github.com/RD1878/frontend-testing-react-project-lvl1/runs/5623908346?check_suite_focus=true), [два](https://datalens.yandex-team.ru/connections/ym4xf2m7ma4yr-maps-analytics-chyt-no-cache))
    - Заменяем кластер на Arnold
    - Заменяем клику на общую, например `*ch_datalens`


### Закончилась квота на ноды 
- Попросите почисчитить ненужные папки в `tmp`, `users`, `st`
- Запросите через `ABC` дополнительные ноды, они бесплатные.

### Автоматическое удаление пустых папок

Нужно выставить атрибут `yt set //home/maps/analytics/@prune_empty_map_nodes "%true" --proxy {cluster}` на папке в которой нужно чистить пустые папки. 
