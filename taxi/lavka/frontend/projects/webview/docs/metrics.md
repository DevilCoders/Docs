## Отправка метрик в Solomon

[Что такое Solomon](https://docs.yandex-team.ru/solomon/)

[Как работает в Такси](https://wiki.yandex-team.ru/taxi-ito/solomonappmetrics/)

Для отправки произвольных метрик используется пакет [@lavka-js-toolbox/metric](https://a.yandex-team.ru/arcadia/taxi/lavka/js-toolbox/packages/metric).

При локальной разработке метрики только пишутся в консоль, но не отправляются.

1) Чтобы начать отправлять новую метрику, необходимо добавить новый сенсор в [список](https://a.yandex-team.ru/arc_vcs/taxi/lavka/frontend/projects/webview/src/endpoint/server/lib/metric/sensors.ts):
```typescript
type TestSensorAttributes = {
  country: string
  city: string
}
export const testSensor = create<TestSensorAttributes>('test_sensor')
```

2) Затем в нужно месте вызвать с атрибутами:
```typescript
import {metric, testSensor} from '../lib/metric'

metric.push(
  testSensor({
    country: 'Russia',
    city: 'Moscow',
  })
)
```

3) Построить график в интерфейсе [Monitoring UI](https://monitoring.yandex-team.ru/projects/taxi/explorer/queries?q.0.s=%7Bproject%3D"taxi"%7D) или [Solomon](https://solomon.yandex-team.ru/?project=taxi) (не рекомендуется). Для этого указать атрибуты:
   * project = taxi
   * cluster = production | testing | unstable
   * service = app
   * application = lavka-{имя сервиса из админки}
   * sensor = {имя сенсора}, `test_sensor` из примера выше
   * {any_other_attr} - любой атрибут, например `country` из примера выше

[![monitoring example](https://jing.yandex-team.ru/files/rifler/2022-05-25_15-45-16.png "monitoring example")](https://monitoring.yandex-team.ru/projects/taxi/explorer/queries?q.0.s=alias%28series_sum%28%22value%22%2C%20drop_below%28diff%28%7Bproject%3D%22taxi%22%2C%20cluster%3D%22production%22%2C%20service%3D%22app%22%2C%20application%3D%22lavka-grocery-frontend-standalone%22%2C%20sensor%3D%22Order%22%7D%29%2C%200%29%29%2C%20%22Заказы%22%29&from=now-1w&to=now&refresh=60000&normz=off&colors=auto&type=auto&interpolation=linear&dsp_method=auto&dsp_aggr=default&dsp_fill=default&vis_labels=off&vis_aggr=avg)
