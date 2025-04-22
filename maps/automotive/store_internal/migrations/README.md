# Migrations
https://github.com/yandex/pgmigrate is used to manage internal store database evolution

First change to directory `maps/automotive/store_internal`

## View current state
```
> pgmigrate -c $CONNECTION_STRING info
{
    "2": {
        "description": "Forced baseline",
        "transactional": true,
        "version": 2,
        "installed_on": "2019-11-06 19:53:15",
        "type": "manual",
        "installed_by": "store_internal"
    }
}
```

## Apply migration $N
```
> pgmigrate -c $CONNECTION_STRING -t $N migrate
```