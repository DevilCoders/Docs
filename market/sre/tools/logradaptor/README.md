# LogRAdaptor
> An utility to find log files that have been improperly compressed, i.e. a rotated log file haven't been removed

## Usage example

```
> cd tests/fixtures
> ../../bin/logradaptor --status-file logrotate.status --dry-run
logs/nginx/content-api-access.log.2018-04-06.gz
> ls -1 logs/nginx/content-api-access.log*
logs/nginx/content-api-access.log
logs/nginx/content-api-access.log.2018-04-06
logs/nginx/content-api-access.log.2018-04-06.gz
>
```

## Links

Motivation here https://st.yandex-team.ru/CSADMIN-22468
