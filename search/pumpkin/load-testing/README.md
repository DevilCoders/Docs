# OVERVIEW

This repository contains scripts and rules for Yandex.Tank ammo generation for Yandex.Lite load testing.

# Environment preparation
## Create virtual environment

Create virtual environemnt and activate it before requirements installation, if you want to run collector within it's own virtual environment.

    virualenv ./venv
    . ./venv/bin/activate


## Install packages to current environtment.

    pip install -r requirements.txt


# UTILITIES

## collect-logs.py

Collects logs from given groups and stores it locally using 'sky run' and 'sky download' utilities.

Supports user-defined aliases for grouping logs and groups. Aliases are given in collect-logs.conf configuration file.

## filter-logs.sh

Allows you to join all collected log files and filter their contents with given filtration programm in awk language.

## generate-ammo.py

Generates ammo files using balancer logs and adds to requests some additional headers.

# EXAMPLES

## collect-logs.py

Collect last 20000 lines from '/usr/local/www/logs/current-access_log-balancer-8080' log files on hosts in I@MSK_BALANCER:

    ./venv/bin/python collect-logs.py -s 20000 I@MSK_BALANCER:/usr/local/www/logs/current-access_log-balancer-8080


Collect last 10000 lines from groups from alias 'RUS':

#### collect-logs.conf

    aliases:
      RUS:
        - I@MSK_BALANCER:/usr/local/www/logs/current-access_log-balancer-8080
        - I@SAS_BALANCER:/usr/local/www/logs/current-access_log-balancer-8082


#### command:

    ./venv/bin/python collect-logs.py -s 10000 RUS


## filter-logs.sh

Filter web-search requests from collected logs:

    filter-logs.sh logs log-filters/web-search.awk


Just glue logs from 'logs' dir and print them to stdout:

    filter-logs.sh logs


## generate-ammo.py

Generate ammo file from balancer log file "balancer_log":

    cat balancer_log | generate-ammo.py


## Whole example:

Collect logs:

    ./venv/bin/python collect-logs.py -s 20000 RUS


Filter them and generate ammo file:

    filter-logs.sh logs log-filters/web-search.awk | generate-ammo.py > web-search.ammo

