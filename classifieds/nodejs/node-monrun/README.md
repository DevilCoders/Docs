# node-monrun

## Usage

~~~js
var monrun = require('node-monrun'),
    simpleCheck = new monrun.Check('simple check');

if (someJob()) {
    simpleCheck.pass();
}

if (someJob()) {
    simpleCheck.fail('error message');
}

console.log(monrun.status());
~~~

## API

### `monrun.status(): Status`

Returns the overall status for registered checks.

`Status` is a struct with the following shape:

- `code: Number` - the overall status code for all checks.
  It equals to the largest status code of all registered checks;
- `statuses: Array<CheckStatus>` - an array of statuses of registered checks that have failed.
  Every `CheckStatus` is an object of shape `{ label: String, code: Number, message: String }`.

### `monrun.Check(label: String, opts: Object)`

Creates and registers a new check.

- `label: String` - a label of the Check
- `opts: Object`
- `opts.expire: Number = 3.6e+6` - an expiration time for a particular status of the Check (milliseconds)
- `opts.capacity: Number = 100` - a window size of the Check
- `opts.warnThreshold: Number = 5` - an amount of failed checks, after which the Check is considered to be in the WARN status
- `opts.critThreshold: Number = 10` - an amount of failed checks, after which the Check is considered to be in the CRIT status

### `Check#pass()`

### `Check#fail(message: String)`
