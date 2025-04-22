## Метрики
#### Dimensions
* fielddate - дата
* source - источник метрики (sdk/ssp/sspid_[SSPID]/app/identity/...)
* key - флаг подсчета
    * key=soup - метрика считается относительно тех связок, которые попали в суп
    * key=total - метрика считается относительно всех накопленных связок
* snap - интервал подсчета (total/daily/new)
* cnt_type - тип метрик [возможные варианты: pairs / ids]
    * cnt_type=pairs означает, что метрика считалась относительно связок
    * cnt_type=ids - относительно идентификаторов, т.е. связался ли идентификатор хоть с чем-то правильным
* with_idfa - срез на котором считалась метрика [возможные варианты: with/without/all]
#### Measures
* fp - количество связанных фингерпринтами связок (если cnt_type=pairs) / идентификаторов (cnt_type=ids)
* with_cid - количество пар/идентификаторов, где был известен cryptaId
* true_cid - количество пар/идентификаторов, в которых cryptaId совпал
* cid_rate - true_cid/with_cid
* coverage - покрытие фингерпринтом (среди тех записей, где конкретный фингерпринт возможен)
* total_coverage - покрытие фингерпринтом на всем логе

Далее идут метрики, которые считаются только на срезе с with_idfa=with (проверка правильности fp-связок идет по idfa)
* true_idfa - количество правильных пар/идентификаторов
* real - реальное количество пар/идентификаторов, на которых ВОЗМОЖНО посчитать фингерпринт
* total - реальное количество пар/идентификаторов
* data_rate - доля данных на которых фингерпринт возможен = real / total
* precision - точность = true_idfa/fp
* recall - полнота = true_idfa/real
* total_recall - полнота относительно всего = true_idfa / total

### Визуализация
- Таблица в статфэйсе: [Crypta/Graph/FingerprintBase](https://stat.yandex-team.ru/Crypta/Graph/FingerprintBase)
- Основой дашборд: [datalens](https://datalens.yandex-team.ru/uj0m556sqfoir-unifiedcryptastats?tab=QyZ) 
  * директория с chart editors к дашборду: [crypta/fingerprint](https://datalens.yandex-team.ru/navigation/ys0qjprvvvhqt-fingerprint)

### Ежедневный запуск в сандбокс
- Настройка шедулера: [spine](https://a.yandex-team.ru/arc/trunk/arcadia/crypta/graph/spine/__init__.py?rev=r8112027#L591).
- Шедулер: [fingerprint metrics](https://sandbox.yandex-team.ru/scheduler/43414/view).
### Релиз
Через общую релизную машину [ЦУМ](https://tsum.yandex-team.ru/pipe/projects/crypta/delivery-dashboard/crypta_graph_fingerprint) для фингерпринта или выкаткой сандбокс ресурса [CRYPTA_BINARY_FINGERPRINT_BUNDLE](https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/projects/crypta/run_binary/bundles.py?rev=r7677371#L4).

### Запуск локально
Сохраняет результаты в [stat-beta](https://stat-beta.yandex-team.ru/Crypta/Graph/FingerprintBase).

Пример
```bash
./crypta-graph-fingerprint-metrics --date 2021-04-25
```
