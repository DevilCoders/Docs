## How to update groups.txt

```shell
rg AddNode yasm/front.conf/prod/nodes.conf  | awk '{print $2 " " $3}'| sed 's/[",]//g' | sort | uniq > arcadia/infra/yasm/common/groups/groups.txt
```
