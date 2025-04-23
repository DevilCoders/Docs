# Create tickets for devops compensation
The script reads `duty-devops.txt` file and create tickets in `SALARY` queue.

File `duty-devops.txt` must in the following format (login, date, weekday, hours number, type):
```
morbid          2019-01-19      Saturday        8       weekend
```

## Installation
Install dependencies.
```
$ make deps
```

## Usage
Update `duty-devops.txt`. Changes will be commited automatically.
```
$ make build
```

Create tickets
```
$ make compensate
```

Push changes to remote.
```
$ git push
```
