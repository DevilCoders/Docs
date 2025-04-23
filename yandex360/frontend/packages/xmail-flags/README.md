### Example

```javascript

const { check, Variable } = require('@ps-int/xmail-flags');

const settings = {
    "attach-tab_promo": "on",
    "browser_notify_message": false,
    "chat-state": "%7B%22fid1-tid168040561096267945%22%3Atrue%2C%22fid1-tid168040561096267948%22%3Atrue%2C%22fid1-tid167477611142846007%22%3Atrue%2C%22fid1-tid168603511049689749%22%3Atrue%2C%22fid1-tid168603511049689917%22%3Atrue%7D",
    "done_shown_counter": "49",
    "tb_mail_mailbox": [
        {
            "id": "archive",
            "settings": {}
        }
    ],
    "reply_to": [
        "foo@example.com",
        "bar@example.com"
    ],
    "exp-1234": "on",
    "theme": "grass"
};
const settingsMap = new Map(Object.entries(settings).map(([k, v]) => [k, v.toString()]));

const values = new Map([
    [ 'locale', Variable.string('ru') ],
    [ 'isPDD', Variable.boolean(false) ],
    [ 'isWS', Variable.boolean(false) ],
    [ 'isCorp', Variable.boolean(false) ],
    [ 'isFriend', Variable.boolean(true) ],
    [ 'sids', Variable.array(['1','2','669']) ],
    [ 'settings', Variable.map(settingsMap) ],
    [ 'currentInterface', Variable.string('iface') ],
    [ 'supportedInterfaces', Variable.array(['iface', 'iface2']) ],
    [ 'daysFromRegistration', Variable.int(10) ],
    [ 'birthdayY', Variable.int(1995) ],
    [ 'birthdayM', Variable.int(4) ],
    [ 'birthdayD', Variable.int(1) ],
]);

const condition = `
    !isPDD &&
    "exp-1234" in settings &&
    "exp-42" not in settings &&
    "iface3" not in supportedInterfaces &&
    "theme" of settings in [ "grass", "weather" ] &&
    "browser_notify_message" of settings == "false" &&
    (locale == "ru" || locale == "en") &&
    ("2" in sids || sids has "669") &&
    "attach-tab_promo" of settings == "on" &&
    "done_shown_counter" of settings != "123" &&
    daysFromRegistration >= 10 &&
    (birthdayY >= 1990 && birthdayY <= 1999) && birthdayM == 4 && birthdayD == 1
`;

console.log(check(values, condition));

// Result { value: true, error: null }

```
