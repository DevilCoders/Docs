nodules-blackbox
================

Обертка над API [Черного ящика](http://doc.yandex-team.ru/blackbox/concepts/about.xml) для Node.js.

## Использование

~~~js
var blackbox = require('nodules-blackbox'),
    bbClient = blackbox({ host : 'blackbox.yandex-team.ru', path : '/blackbox' });
~~~

### `Blackbox#sessionId()`

http://doc.yandex-team.ru/blackbox/reference/MethodSessionID.xml

~~~js
var BB_STATUS = blackbox.STATUS;

bbClient.sessionId({
    sessionid : sessionId,
    host : host,
    userip : userip,
    dbfields : dbFields
})
.then(function(bbResp) {
    if ( ! bbResp) {
        return;
    }

    var status = bbResp.status.id;
    if (status <= BB_STATUS.NEED_RESET) {
        if (status === bbStatus.VALID) {
            return bbResp;
        }

        var newSession = bbResp['new-session'];
        if (newSession) {
            // ...
        }
    }
})
~~~

### `Blackbox#oauth()`

http://doc.yandex-team.ru/blackbox/reference/method-oauth.xml

~~~js
bbClient.oauth({
    token : oauthToken,
    userip : userip
})
.then(function(bbResp) {
    // ...
})
~~~

### `Blackbox#runMethod()`

Вызвать произвольный метод ЧЯ.

На примере [Метода userinfo](http://doc.yandex-team.ru/blackbox/reference/MethodUserInfo.xml)

~~~js
bbClient.runMethod('userinfo', ({
    uid : [uids],
    userip : userip
})
.then(function(bbResp) {
    // ...
})
~~~
