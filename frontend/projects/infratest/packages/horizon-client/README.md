# Horizon GRPC client

> Horizon – сервис, отвечающий за доставку файлов графов и источников до инстансов AppHost'а, их валидацию, предоставление информации о статусе выкатки файлов и возможности для отладки графов, а также отображение перечисленного в удобном для пользователя UI.
[Подробности](https://wiki.yandex-team.ru/horizon/)

### Пример: Nora API
```js
const {Client, GraphModel: {Filter}} = require('@yandex-int/horizon-client');

const client = new Client({host: 'horizon.z.yandex-team.ru', token: '***TOKEN***'});

const filter = new Filter();
filter.setName('graph_name');
filter.setVertical('graph_vertical');
filter.setFromUi(true);

const graph = await client.model.getGraph(filter);
...
```
