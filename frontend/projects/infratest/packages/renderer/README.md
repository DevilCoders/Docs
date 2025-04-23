## Run from sources

```console
$ ./bin/run -h
```

## Run tests

Make and use `npm test`. Node.js 8.6+ and npm required to be installed in you environment.

To keep report-renderer logs set the environment variable `RRTEST_KEEP_LOGS=1`.
Logs directory for each test will be printed to stdout.

## Ynode package
During running `./bin/run` or testing `npm test` last stable ynode package resource will be downloaded.
If you need specific resource - use `REPORT_RENDERER_NODEJS_PACKAGE_RESOURCE_ID` environment variable.

## Package
You need to have [ya tool](https://wiki.yandex-team.ru/yatool/distrib/)
```console
npm run upload
```

## Builds in the SandBox

https://sandbox.yandex-team.ru/resources?type=REPORT_RENDERER_PACKAGE&page=1&pageCapacity=10&state=READY.
