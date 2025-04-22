# luster-log-winston

Write logs with Luster and Winston.

## To use with one logfile

Extension config example:

```js
"luster-log-winston": {
    path: "<path_to_log>"
}
```

To log something just call `luster.logWinston.info(str)`.

## To use with several logfiles

Extension config example:

```js
"luster-log-winston": {
  logs: [
    {
      name: "firstLog",
      path: "path/to/first.log"
    },
    {
      json: true,
      name: "secondLog",
      path: "path/to/second.log"
    }
  ]
}
```

To log something you should call `luster.logWinston.firstLog.info(str)` or `luster.logWinston.secondLog.info(str)`.
