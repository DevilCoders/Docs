
## Тестирвование контролеров

Если хочется отдельно протестирвать логику контроллера, то это можно сделать следующим образом:

```js
import {makeMirrorDesktop} from '@self/root/src/helpers/testament/mirror'; // для тача makeMirrorTouch

/** @type {Mirror} */
let mirror;
/** @type {MandrelLayer} */
let mandrelLayer;

beforeAll(async () => {
    mirror = await makeMirrorDesktop({
        jest: {
            testFilename: __filename,
            jestObject: jest,
        },
        kadavr: {
            skipLayer: true,
        },
    });
    mandrelLayer = mirror.getLayer('mandrel');
    await mandrelLayer.initContext();
});

afterAll(() => {
    mirror.destroy();
});

it('должен генерировать верные данные, коллекции и слоты', async () => {
    await expect(() => jestLayer.runCode(() => {
        const expect = require('expect');
        const controller = require('../controller');
        const inputOptions = {}; // опции контроллера
        const ctx = getBackend('mandrel')?.getContext(); // получаем контекст
        const schema = controller(ctx, inputOptions);
        expect(schema.data).toMatchSnapshot();
        expect(schema.collections).toMatchSnapshot();
        expect(schema.slots.foo.name).toBe('@marketfront/Foo');
        expect(schema.slots.bar.name).toBe('@marketfront/Bar');
    }, [])).resolves.not.toThrow();
});
```
