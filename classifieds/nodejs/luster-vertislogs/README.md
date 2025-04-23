luster-vertislogs
===============

Stream all output from luster master and workers to files in [vertis format](https://wiki.yandex-team.ru/vertis-admin/logs/logsformat/).

## Usage

Add `"luster-vertislogs"` to `"extensions"` section in the luster configuration:

```javascript
module.exports = {
    // ...

    extensions : {
        "luster-vertislogs" : {
            // override `console.log`, `.warn`, `.info` and `.error` methods
            // to add severity marks to output
            extendConsole : true,

            // logs files, both optional
            //   {string} fileName – stream output to file
            //   {boolean} true – don't redirect output, keep as is
            //   {boolean} false – shut down output
            //   {string} 'stderr' | 'stdout' – like boolean but redirects output to specified stream
            stdout : "/var/run/luster/myapp/output.log",
            stderr : "/var/run/luster/myapp/errors.log"
        }
    }
};
```

## Usage without luster

```javascript
const VertislogsStream = require('./lib/vertislogs_stream');
const pipeProcessStream = require('./lib/pipeProcessStream');

const stdoutStream = new VertislogsStream();
stdoutStream.on('data', process.stdout.write.bind(process.stdout));
pipeProcessStream(process.stdout, stdoutStream);

const stderrStream = new VertislogsStream();
stderrStream.on('data', process.stderr.write.bind(process.stderr));
pipeProcessStream(process.stderr, stderrStream);

console.log('hello', 'i am console.log');
console.error('hello', 'i am console.error');
```
