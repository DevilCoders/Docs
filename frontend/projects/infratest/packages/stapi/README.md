## StarTrek API client

### Installation

```
$ npm install --registry="http://npm.yandex-team.ru" @yandex-int/stapi
```

### Example

```javascript
var Client = require('stapi'),
    client = new Client({
        entrypoint: 'https://st-api.test.yandex-team.ru',
        retries: 2,
        timeout: 2000
    }),
    session = client.createSession({
        token: 'xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx'
    });

session.queues.get('AUTO', function(error, queue) {
    if (error) {
        throw error;
    }
    console.log('%s queue lead is %s.', queue.getName(), queue.getLead().getDisplay());
});

session.queues.getAll(function(error, queues) {
    // queues is not an Array, it's a PageOf(Queue)
    // methods next() and forEach() is async
    queues.forEach(function(err, queue) {
        if (err) {
            throw err;
        }
        console.log('%s – %s', queue.getKey(), queue.getName());
    });
});

var Issue = require('stapi/models/issue');

new Issue(session)
    .setQueue('AUTO')
    .setSummary('Something meaningfull')
    .setAssignee('kaero')
    .publish(function(error, issue) {
        if (error) {
            throw error;
        }
        console.log('Issue: https://st.test.yandex-team.ru/' + issue.getKey());
    });
```

### StarTrek Query Language

To get issues using [StarTrek Query Language](https://wiki.yandex-team.ru/tracker/vodstvo/query/)
call method `getAll` of the `issues` collection with option `query`:

```javascript
session.issues.getAll({ query: 'Assignee: me() and Resolution: empty()' },
    function(err, issues) {
        // ...
    });
```

### Access custom fields

Any field of model can be accesses using method `Model#getField(name)`,
but feel free to define your own model type and cast recevied model to it.

For example, issues in the queue `AUTO` has custom field `qaEngineer`, which is reference to user.

You can get it as plain JavaScript object using `Model#getField()`:

```javascript
session.issues.get('AUTO-100', function(err, issue) {
    console.dir(issue.getField('qaEngineer'));
});
```

Or use casting field to model:

```javascript
var UserRef = require('stapi/models/user-ref');

session.issues.get('AUTO-100', function(err, issue) {
    issue.getFieldAs(UserRef, 'qaEngineer').unref(function(err, user) {
        console.log('QA engineer email: %s', user.getEmail());
    });
});
```

Or define custom model and cast common Issue as your own type:

```javascript
var UserRef = require('stapi/models/user-ref'),
    Issue = require('stapi/models/issue'),
    Model = require('stapi/model');

var AutoIssue = Model.declare('AutoIssue', Issue, {
        getQAEngineer: Model.createGetterOf(UserRef, 'qaEngineer')
    });

session.issues.get('AUTO-100', function(err, issue) {
    issue.cast(AutoIssue).getQAEngineer().unref(function(err, user) {
        console.log('QA engineer email: %s', user.getEmail());
    });
});
```

### Run test suites and gather tests coverage

```console
$ npm install
$ npm test
$ npm run coverage
```

OAuth token and access to https://st-api.test.yandex-team.ru/ is required to run tests.
Launch `npm test` to give instructions to obtain and setup an OAuth token.

Some tests take a lot of time to pass, so they are disabled by default. To enable them
change the value of the field `quick` in the `test.conf.js`. Final tests coverage report
must be gathered with **quick: false**.

