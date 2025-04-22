# express-sendlinksms [![Build Status](http://drone.haze.yandex.net/api/badge/github.yandex-team.ru/project-stub/express-sendlinksms/status.svg?branch=master)](http://drone.haze.yandex.net/github.yandex-team.ru/project-stub/express-sendlinksms)

sendlinksms midleware for express

## Install

Set your npm registry server to `http://npm.yandex-team.ru` then `npm install express-sendlinksms`

## Example

```js
var app = express();

// Зависимости
app.enable('trust proxy');
app.use(express.cookieParser());
app.use(require('express-blackbox')());
app.use(require('express-geobase')());
app.use(require('express-langdetect')());

app.use(require('express-sendlinksms')());

app.get('/', function (req, res) {
    req.sendlinksms('maps', '+79090115050').then(function (status) {
        if (status === 'ok') {
    	    res.send(200);
        } else {
            res.send(400); // Что-то не так
        }
    }, function () {
    	res.send(500);
    });
});
```
