How-to use:

```
jfr.sh <application-name> <duration>
```

For example:
```
jfr.sh coremon 10s
jfr.sh stockpile 10m
```

When everything is fine, output will be look like:
```
$ jfr.sh coremon 10s
240736:
Commercial Features now unlocked.
240736:
No available recordings.

Use JFR.start to start a recording.

240736:
Started recording 1. The result will be written to:

/home/gordiychuk/jfr/coremon-2018_05_23-12_15.jfr
```
