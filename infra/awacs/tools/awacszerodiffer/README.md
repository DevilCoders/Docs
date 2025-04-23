```
export AWACS_TOKEN=AQAD-XXX
cat ./candidates.txt | xargs -I % ./awacszerodiffer zerodiff --namespace-id %

usage for unistat_activation
for n in `cat candidates.txt`; do ./awacszerodiffer --awacs-token=AQAD-XXX unistat_activation --namespace-id "$n"; done
saves processed namespaces to processed_namespaces.txt
```
