# `maps-logger`

Package for logging. It uses TSKV format and extends from `winston`.

```ts
import {createLogger} from '@yandex-int/maps-logger';

const logger = createLogger({
    tskvFormat: 'service-log'
});

logger.info('Message');
// tskv	tskv_format=service-log	group=unknown	timestamp=29/10/2019:10:48:26	hostname=sigorilla-osx	unixtime=1572335306	message=Message
logger.info('Message', {group: 'module-a'});
// tskv	tskv_format=service-log	group=module-a	timestamp=29/10/2019:10:48:26	hostname=sigorilla-osx	unixtime=1572335306	message=Message
```

More example see in `./example` folder.
