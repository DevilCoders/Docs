# @yandex-int/abt

Library to work with [`UserSplit As A Service (USaaS) aka YA3`](https://wiki.yandex-team.ru/jandekspoisk/kachestvopoiska/abt/uaas/).
A typical ABT thing.

<!-- toc -->
- [@yandex-int/abt](#yandex-intabt)
  - [Intro](#intro)
  - [Usage](#usage)
    - [Подключение к Я.Метрике](#подключение-к-яметрике)
  - [Usage grpc](#usage-grpc)
<!-- tocstop -->

## Intro
<!-- intro -->
Начинать внедрение на сервисе лучше со встречи с [командой разработки экспериментов](https://staff.yandex-team.ru/departments/yandex_search_tech_quality_rank_userdata_experiment/).

Узнать общую информацию можно из [статьи про abt на wiki](https://wiki.yandex-team.ru/jandekspoisk/kachestvopoiska/abt/uaas/)
и [Гайда на сайте документации](https://doc.yandex-team.ru/analytics/experiments-guide/).

[Инструкции](https://doc.yandex-team.ru/analytics-experiments-instr/index.html).

Чек лист:
- Заказать доступы из своих подсетей и abc-сервиса до [uaas.search.yandex.net:80](https://puncher.yandex-team.ru/?destination=uaas.search.yandex.net&protocol=tcp&ports=80&rules=exclude_rejected&values=all&sort=destination);
- Завести заявку на добавление очереди из трекера [в админку AB](https://doc.yandex-team.ru/analytics-experiments-instr/rm/99testing/index.html#step3);
- Встретиться с ребятами из [команды экспериментов](https://staff.yandex-team.ru/departments/yandex_search_tech_quality_rank_userdata_experiment/) и заявить о желании подключиться;
- Начать поставлять [данные в метрику](https://wiki.yandex-team.ru/jandekspoisk/kachestvopoiska/abt/metrika/#x-yandex-expboxes-crypted);
- Дождаться раскатки конфига и получать удовольствие.
<!-- introstop -->

## Usage
<!-- usage -->
```ts
import { Server } from 'http';
import { ABTSplitter, ABTInfo } from '@yandex-int/abt';

// Обычно достаточно одного экземпляра ABT на каждый сервис
const abt = new ABTSplitter({ service: 'forms', handler: 'FORMS' });

const server = new Server(async (req, res) => {
  // …
  // Схема L7-USaaS: Если есть L7 балансер и включен USaaS макрос:
  const info: ABTInfo = abt.parseInfo(req.headers, { set_this_flag: 'my-darling' });

  // Схема AnyService-USaaS: В любом другом случае ходим напрямую в uaas.search.yandex.net:
  const info: ABTInfo = await abt.askForInfo(req.headers);

  // …
});
```
<!-- usagestop -->

### Подключение к Я.Метрике
<!-- metrika -->
В поле `info.experiments` содержится подготовленная зашифрованная строчка с `X-Yandex-ExpBoxes`, которую надо передать в конструктор Метрики.

- [Подробнее про подключение по Метрике](https://wiki.yandex-team.ru/jandekspoisk/kachestvopoiska/abt/metrika/)
- [Проращивание экспериментов в RUM](https://wiki.yandex-team.ru/velocity/abt/)

```js
w.yaCounter<counter_id> = new Ya.Metrika({
  id: metrika.counterId,
  params: metrika.params,
  experiments: info.experiments,
  // ...
});
```
<!-- metrikastop -->

## Usage grpc
<!-- usagegrpc -->
Если сервис работает через Apphost, то UaaS лучше подключать как вершину графа и пользоваться `abt/grpc` – частью пакета, которая работает с gRPC форматом и помогает с протобафами.

С gRPC форматом необходимо, сначала, подготовить запрос в вершину UaaS-а, затем, сходить в эту самую вершину (вне данного пакета), потом получить результаты от UaaS-а и вытащить флаги.

0. Пометка

*apphostNativeContext – входной параметр в main функции вершины графа – вершину нужно заводить самостоятельно, а посмотреть пример такой вершины можно в сервисе [jobs](https://a.yandex-team.ru/arc/trunk/arcadia/frontend/services/jobs), вершина называется [INIT_UAAS](https://a.yandex-team.ru/arc/trunk/arcadia/frontend/services/jobs/src/entries/server/init-usersplit.ts)*

1. Подготовка запроса:
```ts
import { ApphostContext } from '@yandex-int/frontend-apphost-context';
import { ABTGrpcSplitter, UaasRestrictions, UaasSplitIds } from '@yandex-int/abt/build/grpc';

const apphostContext = new ApphostContext(apphostNativeContext);

// Определяет сервис, для которого нужны эксперименты.
const restrictions: UaasRestrictions = {
  Service: 'jobs',
};
// Добавляет Icookie как способ разбиения трафика (нужно для UaaS-а).
const splitIds: UaasSplitIds = {
  Icookie: 'someIcookie',
};

const reqProtobuf = ABTGrpcSplitter.getUaasRequest(restrictions, splitIds);

// Добавление запроса для UaaS-а в аппхостовый контекст. Ждёт Buffer, но по факту использует Uint8Array.
apphostContext.addProtobufItem('uaas_input', reqProtobuf as Buffer);
```

2. Получение флагов:
```ts
import { ApphostContext } from '@yandex-int/frontend-apphost-context';
import { ABTGrpcSplitter, ABTInfo, UaasResponse } from '@yandex-int/abt/build/grpc';

const apphostContext = new ApphostContext(apphostNativeContext);

// Извлечение из контекста результатов работы вершины UaaS-а.
const uaasResponse: UaasResponse = ABTGrpcSplitter.getUaasResponse(apphostContext, 'jobs');

// Парсинг результатов UaaS-а.
const info: ABTInfo = new ABTGrpcSplitter({ service: 'jobs', handler: 'JOBS' }).parseInfo(uaasResponse);

// Дальше, можно использовать info как угодно)
```
<!-- usagegrpcstop -->
