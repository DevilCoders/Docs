luster-log-stat
===============

Stream luster master and workers stats to files

##To use with one logfile
Extension config example
```
"luster-log-stat": {
    path: "path/to/log
}
```

To log something just call `luster.logStat.write(str)`

##To use with several logfiles
Extension config example
```
"luster-log-stat": {
  logs: [
    {
      name: "firstLog",
      path: "path/to/first.log"
    },
    {
      name: "secondLog",
      path: "path/to/second.log"
    }
  ]
}
```
To log something you should call `luster.logStat.firstLog.write(str)` or `luster.logStat.secondLog.write(str)`
