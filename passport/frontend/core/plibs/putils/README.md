```javascript
require('putils')

require('putils').i18n
    .setAllowedLangs(['ru', 'en'])
    .setKeysets(['Common', 'EULA', 'Frontend'])
    .loadFromDir(__dirname + '/loc');
require('putils').i18n('ru', 'someKey')

require('putils').csrf.setSalt('aehohwa8Aeth8aen')
require('putils').csrf(uid, yandexuid)
```
