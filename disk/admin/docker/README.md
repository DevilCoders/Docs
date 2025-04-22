# yandex-disk-docker-images
Docker-образы Yandex.Disk'a и оверрайды настроек

## Как собрать образ локально
```bash
# docker должен быть запущен локально
# залогиниться в registry.yandex.net
USER_NAME=`whoami`
TOKEN=XXX # https://wiki.yandex-team.ru/qloud/docker-registry/#authorization
docker login -u $USER_NAME -p $TOKEN -u $USER_NAME@yandex-team.ru registry.yandex.net

cd disk/clusters/cluster_name
docker build . -t dev -f app.Dockerfile
docker run -it dev /bin/bash
```
