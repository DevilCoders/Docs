```
export AWACS_TOKEN=AQAD-XXX
cat ./candidate-namespace-ids.txt | xargs -I % ./awacsemtool suggest --namespace-id % --rule tlem
```
or
```
./awacsemtool suggest --rule tlem [--do-update --ticket <text> [--update-with-diff]] --namespace-id <id> [--l7-macro-version <version>]
```
or
```
./awacsemtool suggest --rule uem --uem 1 [--do-update --ticket <text> [--update-with-diff]] --namespace-id <nid> [--balancer-id <bid>]
```
Please note that the certificate has to be imported before (using `infra/awacs/tools/awacscertsctl`).
