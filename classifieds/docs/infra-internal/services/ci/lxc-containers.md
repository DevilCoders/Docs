## LXC контейнеры в вертикалях

В аркадии нет прямой поддержки докера, только lxс контейнеры и porto. Но в lxc контейнере можно запустить докер (и такой контейнер уже есть)

### Как найти

Все используемые в ci контейнеры можно найти [поиском по аркадии](https://a.yandex-team.ru/search?search=container_resource,%5Eclassifieds%2F.*a.yaml,jC,arcadia,,200&repo=arc_vcs), стоит посмотреть что там есть перед тем, [как создавать новый](https://docs.yandex-team.ru/sandbox/dev/environment#custom-environment).

Тут будет список важных контейнеров, которые имеет смысл переиспользовать, добавляйте свои, если считаете нужным:

| ресурс | что там                    |
| ---------|------------------------------------|
|3342470530| docker                     	|
|2877230037| docker, jq, bazel, grpcurl 	|
|2902051351| Java 8 and sbt             	|
|2864087804| Java 8 and Maven           	|
|2888321490| protobuf 3.16.x            	|
|2894043086| nodejs, protoc             	|
|3062180833| python, protoc             	|
|2986919603| python3, pip3, bazel, buildozer    |
