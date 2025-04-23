## Быстрый старт

В данном разделе документации рассмотрим как собрать, запустить и создать ответ сценария в Гудвине.

### Установка зависимостей

1. В корне монорепозитория необходимо установить общие, между проектами зависимости `npm ci`
2. В корне проекта, нужно также установить зависимости `npm ci`
3. Запустить сборку с помощью команды `npm run build`

### Старт проекта

Запустить проект можно с помощью команды `npm run start`. После этого локальный сервер будет доступен по адресу `http://<instance-name>.<location>.yp-c.yandex.net:3333`, например, `http://lezin-dev.sas.yp-c.yandex.net:3333`

### Новый сценарий

Чтобы добавить новый сценарий в Гудвин, нужно реализовать адаптер, который будет формировать ответ данного сценария.

1. Код адаптера должен находиться в директории [src/features/](src/features/), например, `src/features/TestFeature/TestFeature.server.ts`
2. Написать базовую реализацию адаптера

```js
import { ISnippet } from '@yandex-int/taburet/lib/adapters';

import { Adapter } from 'vendors/taburet/Adapter';
import { IAliceDocResponse } from 'typings/goodwin';

interface ITestFeatureSnippet extends ISnippet {
    type: 'test_feature';
}

export class AdapterTestFeature extends Adapter<ITestFeatureSnippet> {
    public transform(): IAliceDocResponse {
       // Здесь формирование ответа сценария Алисы
    }
}
```

3. Сформировать ответ сценария через базовый класс `AliceDocResponse` в методе `transform`

```js
public transform(): IAliceDocResponse {
    const response = new AliceDocResponse(
        this.snippet.type,
        'Ответ голосом',
        'Ответ текстом или карточками'
    );

    return response.serialize();
}
```
