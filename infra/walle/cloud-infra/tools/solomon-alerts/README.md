## Generate alerts in Solomon

Build:
```
ya make
```
To update YC.Wall-E alerts in cloud installation of Solomon modify
thresholds values in `thresholds.json` and run:
```
./generate-alerts <command>
## Commands:
##	missing-checks
##	active-checks-age
##	expertise-age
##	invalid-health-checks
```
