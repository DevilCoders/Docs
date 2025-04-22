luster-var-log [![NPM version][npm-image]][npm-link] [![Build status][ci-badge]][ci-link]
===============

[![Dependency status][deps-image]][deps-link]
[![devDependency status][devdeps-image]][devdeps-link]
[![peerDependency status][peerdeps-image]][peerdeps-link]

Stream all std output from [luster][luster-link] master and workers to files.

This extension supports:
  - logfile reopening on `SIGHUP`(by default)
  - custom log line transformation functions

## Usage

Install extension module to application:

```console
$ npm install --save luster-var-log
```

Add `"luster-var-log"` to `"extensions"` section in the luster configuration:

```javascript
module.exports = {
    extensions: {
        'luster-var-log': {
            // Signal that process should handle to reopen logfiles
            // signal: 'SIGHUP',

            // Transform each line with custom transform function
            // transformFn: function(proc, line) {return 'prefix ' + line;},

            // logs files, both optional
            //   {string} fileName – stream output to file
            //   true  – don't redirect output, keep as is
            //   false – shutdown output
            stdout: '/var/log/app/stdout.log',
            stderr: '/var/log/app/stderr.log'
        }
    }
};
```


[npm-image]: https://img.shields.io/npm/v/luster-var-log.svg?style=flat
[npm-link]: https://npmjs.org/package/luster-var-log
[deps-image]: https://img.shields.io/david/corpix/luster-var-log.svg?style=flat
[deps-link]: https://david-dm.org/corpix/luster-var-log
[devdeps-image]: https://img.shields.io/david/dev/corpix/luster-var-log.svg?style=flat
[devdeps-link]: https://david-dm.org/corpix/luster-var-log#info=peerDependencies
[peerdeps-image]: https://img.shields.io/david/peer/corpix/luster-var-log.svg?style=flat
[peerdeps-link]: https://david-dm.org/corpix/luster-var-log#info=peerDependencies
[luster-link]: https://github.com/nodules/luster
[ci-badge]: https://travis-ci.org/corpix/luster-var-log.svg?branch=master
[ci-link]: https://travis-ci.org/corpix/luster-var-log
