# luster-billing-keys

## Usage

~~~js
// worker.js

var luster = require('luster'),
    billingKeys = luster.billing;

if (billingKeys) {
    console.log('billing is available for worker %d', luster.wid);
}

// {"current":"key3==","previous":"key2=="}
JSON.stringify(billingKeys.keys);
~~~

## Configuration

~~~js
// luster.json
{
  "extensions": {
    "luster-billing-keys": {
      "path": "/etc/yandex/vertis-datasources/billing.keys"
    }
  }
}
~~~

### Keys file example

`luster-billing-keys` reads two of the most recent keys from the keys file and pushes them
to all worker processes.

~~~shell
› cat /etc/yandex/vertis-datasources/billing.keys

key3==
key2==
key1==
~~~
