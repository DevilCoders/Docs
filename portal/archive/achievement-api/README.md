# achievement-api


###Mysql
```

CREATE TABLE IF NOT EXISTS `achievements` (
    `user_id`   DECIMAL(20) PRIMARY KEY,
    `value`     VARCHAR(500)
);

```
### Postgresql
```
CREATE TABLE IF NOT EXISTS achievements (
    user_id   numeric(22) PRIMARY KEY,
    value     json
);
```