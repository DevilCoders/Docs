# @yandex-ing/nock-log

Модуль позволяет исключить ручное написание проверок параметров запроса при использовании `nock`. 
Вместо этого модуль запоминает запросы и ответы в наборе инстансов `nock.Scope`, чтобы затем сравнить их с эталонным значением.

## Установка

Для установки пакета следует выполнить в корне репозитория:
```bash
npx lerna add @yandex-int/nock-log --scope=<package-name>
```
где `<package-name>` - название пакета, куда нужно установить `nock-log`.

## Использование

Пример использования с jest snapshots:

```ts
import nock from 'nock';
import { nockLog, NockLog } from '@yandex-int/nock-log';

let requestsLog: NockLog;
beforeEach(() => {
    requestsLog = nockLog();
});

it('should request something', () => {
    const scope = nock('http://some-api')
        .post('/v0/detect')
        .reply(200);
    
    // Либо создаем scope через const scope = requestsLog.nock('...')
    requestsLog.addScope(scope);

    // do some testing

    expect(requestsLog.getLog()).toMatchSnapshot();
});
```
