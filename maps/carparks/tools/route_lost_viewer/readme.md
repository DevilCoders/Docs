This tool has two parts:

1\) Route lost viewer

2\) Carparks clusters (driving arrival point, DAPs) viewer

# Route lost viewer

Service is on http://maps-mobgeoplatform-dev.vla.yp-c.yandex.net:10001/

It shows routes and tracks for user for specified time.

## Request params:

uuid - user id

upper - upper time bound

lower - lower time bound

app - application [default is 'navi']

Request example: http://maps-mobgeoplatform-dev.vla.yp-c.yandex.net:10001/?uuid={uuid}&upper={upper}&lower={lower}&app={app}

# Carparks clusters (driving arrival points, DAPs) viewer

Service is on http://maps-mobgeoplatform-dev.vla.yp-c.yandex.net:10001/daps/

It shows mined carparks clusters for specified target and date.

## Request params:

Clusterized points table path or date - path for YT table with clusters or date (YYYY-MM-DD).

Target - in new version is org_id_{id} for organizations or geo_id_{id} for toponyms. You can set target via search request.

Also old version still supported: org_id or geoobject coords '{lon} {lat}' (4 digits precision). So, all links still work properly.

# Build and run docker

Build docker image:
```
cd docker
make.sh
```
Get image id, the most recent one on top of the list:
```
docker image ls
```
Start docker container under testing robot (you'll need his YT token):
```
docker run -d -e RLV_PORT=10001 -e YT_TOKEN=`cat ~/.yt/robot_token` --net=host --name=route_lost_viewer --restart on-failure {image_id}
```

# Troubleshooting

List running docker containers and find an id of the one with  route_lost_viewer tag:
```
docker ps
```
Read logs:
```
docker logs <container id>
```
