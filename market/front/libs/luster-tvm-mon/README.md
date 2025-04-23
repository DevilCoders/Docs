# Luster TVM monitoring
Мониторинг времени жизни тикетов TVM'а.

Расширение слушает RPC событие 'tvm ticket update' через которое воркер извещает об обновлении тикета:
```javascript
var luster = require('luster');
if (luster.config.extensions['luster-tvm-mon']) {
    luster.remoteCall('tvm ticket update', ticket);
}
````
Далее находится воркер с наиболее старым тикетом, и проверяется что время его получение не старше updateThreshold.

После проверки статус записывается в файл statFile в формате ```<CODE>;<MESSAGE>```.

Возможные коды:
* OK - если все тикеты прошли проверку
* NOK – если хотя бы один тикет не прошел. В message будут подробности вида: ```ticket is stale, wid: <worker id>, update time: 2016-11-15T16:46:53+03:00```

# Пример конфига ластера
```javascript
module.exports = {
    app: '../../app/start.js',

    extensions: {
        'luster-tvm-mon': {
            statFile: process.cwd() + '/tvm-state',
            updateThreshold: [10, 'minute'] // в формате moment.js
        }
    }
};
```
