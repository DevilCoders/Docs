# duty_count

Tool for counting a duty schedule.

## Usage
```
~$ ./duty_count --help
usage: duty_count [-h] --start-date START_DATE --end-date END_DATE [--service {datacamp,marketindexer}] [--role {datacamp_oncall,...}] [--format {text,json}]

ABC duty Schedule

optional arguments:
  -h, --help            show this help message and exit
  --start-date START_DATE
  --end-date END_DATE
  --service {datacamp,marketindexer}
  --format {text,json}
```


## Usage example
```
~$ export OAUTH_TOKEN=<OAUTH TOKEN>
~$ ./duty_count --start-date=2021-09-06 --end-date=2021-12-05 --service=datacamp
Service: datacamp
Duties: datacamp_oncall, datacamp_support, datacamp_action, datacamp_partner_support
Period: 2021-09-06 - 2021-12-05
╒════╤═══════════════╤════════════════╤════════════════╤══════════════╤═══════════════╤═══════════════════╕
│    │ Login         │   Working Days │   Weekend Days │   Total Days │   OnCall Days │ Duty Percentage   │
╞════╪═══════════════╪════════════════╪════════════════╪══════════════╪═══════════════╪═══════════════════╡
│  0 │ thesonsa      │             16 │              4 │           20 │            10 │ 25%               │
├────┼───────────────┼────────────────┼────────────────┼──────────────┼───────────────┼───────────────────┤
│  1 │ ana-samokhina │             16 │              2 │           18 │             8 │ 25%               │
├────┼───────────────┼────────────────┼────────────────┼──────────────┼───────────────┼───────────────────┤
│  2 │ krasnobaev    │             18 │              0 │           18 │             8 │ 28%               │
├────┼───────────────┼────────────────┼────────────────┼──────────────┼───────────────┼───────────────────┤
│  3 │ isabirzyanov  │             16 │              2 │           18 │             8 │ 25%               │
├────┼───────────────┼────────────────┼────────────────┼──────────────┼───────────────┼───────────────────┤
│ 19 │ razmser       │              1 │              1 │            2 │             2 │ 2%                │
╘════╧═══════════════╧════════════════╧════════════════╧══════════════╧═══════════════╧═══════════════════╛

~$ ./duty_count --start-date 2021-10-01 --end-date 2021-11-01 --service marketindexer --role datacamp_oncall --format json | jq .results[0]
{
  "id": 2877185,
  "person": {
    "login": "fess7",
    "uid": "1120000000040649"
  },
  "schedule": {
    "id": 3157,
    "name": "OnCall дежурства индексатора"
  },
  "is_approved": true,
  "start": "2021-09-30",
  "end": "2021-10-01",
  "start_datetime": "2021-09-30T12:00:00+03:00",
  "end_datetime": "2021-10-01T12:00:00+03:00"
}
```
