Redux-middleware для работы с метрикой и зонами
==

Пример использования
==

```javascript
// @flow

import type {GenericAction} from '@yandex-market/apiary/common/actions';
import launch from '@yandex-market/mandrel/launchClient';
import {applyMiddleware} from 'redux';
import '@/widgets/core/Root';
import {createZoneMiddleware, metrikaEmitter, reachGoalFactory} from '@yandex-market/cia';

const COUNTER_ID = '47628343';
const SERVICE_ID = 'market_front_blue_desktop';

const state = window.state;

const reachGoal = reachGoalFactory(COUNTER_ID);
const emitMetrika = (action: GenericAction) =>  metrikaEmitter(reachGoal, action);
const zoneMiddleware = createZoneMiddleware(emitMetrika);

launch({
    enhancer: applyMiddleware(zoneMiddleware),
    sk: state.user.sk,
    counterId: COUNTER_ID,
    serviceId: SERVICE_ID,
    pageId: state.pageId,
    requestId: state.requestId,
    requestStart: state.requestStart,
    expFlags: state.expFlags,
});
```
