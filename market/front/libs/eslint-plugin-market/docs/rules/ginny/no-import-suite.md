# ginny/no-import-suite

Запрещает использовать importSuite. Вместо этого стоит использовать [prepareSuite](https://github.yandex-team.ru/market/hermione-suite-manager#preparesuite--options).

## Примеры

Примеры **неправильного** кода:

```js
import {importSuite} from 'ginny';

importSuite('b-button', {...});
```

```js
const {importSuite} = require('ginny');

importSuite('b-button', {...});
```

Примеры **правильного** кода:

```js
import {prepareSuite} from 'ginny';
import ButtonSuite from '@/spec/hermione/test-suites/blocks/b-button';

prepareSuite(ButtonSuite, {...});
```

```js
const {prepareSuite} = require('ginny');
const ButtonSuite = require('@/spec/hermione/test-suites/blocks/b-button');

prepareSuite(ButtonSuite, {...});
```
