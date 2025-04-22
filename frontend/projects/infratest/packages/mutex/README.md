# Mutex
## Использование

```js
import Mutex from '@yandex-int/mutex';

const mutex = new Mutex({ name: 'mutex', warnQueueSize: 4 })
const start1 = () => console.log("start1");
const stop1 = () => console.log("stop1");
const start2 = () => console.log("start2");

const firstCall = (async () => {
    const stop = await mutex.lock();
    start1();
    await delay(0);
    stop1();
    stop();
})();

const secondCall = (async () => {
    await mutex.lock();
    start2();
})();

await Promise.all([firstCall, secondCall]);

// start1 -> stop1 -> star2
```

