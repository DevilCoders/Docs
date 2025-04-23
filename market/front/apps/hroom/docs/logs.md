# Работа с логами
Для логов необходимо использовать модуль ```lib/logger```. Например, так будет выглядеть работа метода log:
```javascript
import {log} from 'lib/logger';

log('hello');
// index.js:3   hello
```
Как видно, метод лог выводит путь к файлу, в которм он был вызван и номер строки.
Данный метод необходим, главным образом, для разработки.

По дефолту модуль logger экспортирует объект logger.
```javascript
import logger from 'lib/logger';

const user = await User.findOne({email: req.body.email});
user.email = req.body.newEmail;
const [err] = await to(user.save());
if (err) {
    logger.error('user update error', {
        error: err
        newEmail: req.body.newEmail,
        email: req.body.email,
    });
    return;
}

logger.info('user update success', {
    username,
    newEmail: req.body.newEmail,
    email: req.body.email,
});
```
Данный метод необходим, главным образом, в production-режиме, а также в процессе выполнения тасков (exec-команд).
Как видно из примера, объект logger имеет два метода: info и error, каждый пришется в свой файл в виде json-а.
Все поля, которые передаются в объекте во втором параметре приводятся к строке, объекты - сериализуются через util.inspect.
В дальнейшем по этим данным можно собирать статистику ошибок и строить метрики.
