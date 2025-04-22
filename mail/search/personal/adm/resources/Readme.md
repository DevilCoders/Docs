# Resource generation instruction for personal search services

## Get services list from nanny and write it to tmp file

Url: https://nanny.yandex-team.ru/ui/#/services/

Example service list (search_services2021_manual_dirty.txt) :

```
 abook 4

    aceventura 4
        proxy 4
            prod 1
                aceventura_proxy_prod Address book esarch service
                ONLINE 2 days ago
            qa 2
                aceventura_proxy_prod_qa Ace ventura proxy qa
                ONLINE 8 days ago
                aceventura_proxy_qa Ace ventura proxy qa
                OFFLINE a year ago
            test 1
                aceventura_proxy_test Aceventura contacts test
                ONLINE 2 months ago

balancer 29

    iex-proxy-prod3 3
        production_balancer_iex_proxy_prod3_man iex-proxy-prod3.search.yandex.net in man
        ONLINE 4 months ago
        production_balancer_iex_proxy_prod3_sas iex-proxy-prod3.search.yandex.net in sas
        ONLINE 3 months ago
        production_balancer_iex_proxy_prod3_vla iex-proxy-prod3.search.yandex.net in vla
        ONLINE 3 months ago

```


## Prepare services list by bash script

```
cat search_services2021_manual_dirty.txt | grep -v "ONLINE\|OFFLINE\|UPDATING\|Group" | sed 's/^\ \ \ \ //g' | tr " " "+" | awk -F '+' '{ if ($2~/^[0-9]+/) print "\r\nSERVICE: "$1"\r\n"; else print $0}' | tr -s "+" | awk -F '+' '{ if ($3!~/^[0-9]+/)print $0}' | cut -d "+" -f 1,2 | tr -d "+"
```

Result:

```
SERVICE: aceventura

aceventura_proxy_prod
aceventura_proxy_prod_qa
aceventura_proxy_qa
aceventura_proxy_test


SERVICE: balancer



SERVICE: iex-proxy-prod3

production_balancer_iex_proxy_prod3_man
production_balancer_iex_proxy_prod3_sas
production_balancer_iex_proxy_prod3_vla
```

## Launch resourse.py and wait untill data.json will be generated

python3 resource.py


## Launch resource.py again to get template for services



