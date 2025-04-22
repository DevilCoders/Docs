# Fork nodules/yandex-mycookie
## Cookie "my" parsing

```javascript
var my = require('yandex-mycookie');

console.dir(my.parse('YyMCAwUrAgKAsSwBAS4BATYBAQA='));
```

result:

```
{
    '35': [ 3, 5 ],
    '43': [ 2, 177 ],
    '44': [ 1 ],
    '46': [ 1 ],
    '54': [ 1 ]
}
```

## Blocks to cookie value serialization

```javascript
var my = require('yandex-mycookie'),
    blocks = my.parse('YyMCAwUrAgKAsSwBAS4BATYBAQA=');

blocks['46'] ? blocks['46'][0] = 0 : blocks['46'] = [ 0 ];
blocks['99'] = [ 42, 0, 42 ];

console.log('Cookie value: ', my.serialize(blocks));
```
