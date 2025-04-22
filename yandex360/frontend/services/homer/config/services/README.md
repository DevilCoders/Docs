# Настройки сервисов

В `options.services[service]` может быть поле `url`. Если оно есть,
то переопределяем им соответсвующее свойство в объекте `urls`.
В примере ниже в `urls.other` будет значение `http://127.0.0.1:1234`.

Для каждого метода каждого сервиса есть дефолтные параметры для `core.got`.
Например:
  * для метода `/ninja_auth` сервиса `akita` будут параметры `(3)`;
  * для метода `/test` сервиса `akita` будут параметры `(2)`;
  * для любого метода сервиса `other` будут параметры `(4)`;
  * для любого метода сервиса `wtf` будут параметры `(1)`;
  * для метода `test` сервиса `nodefault` будут параметры `(5)`;
  * для любого другого метода сервиса `nodefault` будут параметры `(1)`.

```js
// urls.js
urls = {
    akita: 'http://akita.mail.yandex.net:11110',
    other: 'http://other.mail.yandex.net:1234'
};

// options.js
options = {
    defaults: {
        serviceOptions: { // (1)
            timeout: 1000,
            retryOnTimeout: 0
        }
    },
    services: {
        akita: {
            methods: {
                default: { // (2)
                    timeout: 500,
                    retryOnTimeout: 1
                },
                '/ninja_auth': { // (3)
                    timeout: 200,
                    retryOnTimeout: 2
                }
            }
        },
        other: {
            url: 'http://127.0.0.1:1234',
            methods: {
                default: { // (4)
                    timeout: 50,
                    retryOnTimeout: 5
                }
            }
        },
        wtf: {
            url: 'http://wtf.js'
        },
        nodefault: {
            methods: {
                test: { // (5)
                    timeout: 50,
                    retryOnTimeout: 5
                }
            }
        }
    }
};
```
