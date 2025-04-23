# Ammo generator for personal-api

Generates ammo for Personal-API 
stress testing in Yandex.Tank format.

## Usage
For generate mixed settings request to given service use:
```
$ go run main.go -mode settings -service {service name} -users-count {users count} -read-requests-count {requests count}   
```

For more options use `-help` key
```
$ go run main.go -help
  -mode string
    	ammo mode: settings|favorites (default "settings")
  -read-requests-count int
    	number of request to generate (default 100)
  -service string
    	service within favorites (default "realty")
  -users int
    	number of users to operate (default 10)

```
