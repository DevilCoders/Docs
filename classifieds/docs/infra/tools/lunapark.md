# Организация стрельбы в lunapark

Официальная документация https://wiki.yandex-team.ru/Verticals/VSML/Development/KnowledgeBase/#kakorganizovatstrelbypost-zaprosamisjsonvlunaparke

## Как организовать стрельбы в shiva-сервис за nginx-балансером

Все примерно как описано выше, но надо понимать несколько вещей:
* надо стрелять в http, а не в https (вряд ли нам интересна скорость tls handshake)
* надо стрелять не в балансер, а в конкретную envoy-машинку. Например, `http://lb-int-01-sas.test.vertis.yandex.net`
* надо передавать заголовок `host` с именем shiva-сервиса. В общем виде он выглядит как `<service_name>-<api_name>.vrts-slb.test.vertis.yandex.net`

Таким образом у нас есть задача эмулировать вот такой curl
```
curl -sv 'http://lb-int-01-sas.test.vertis.yandex.net' -H 'host: af-desktop-web.vrts-slb.test.vertis.yandex.net'
```

Патроны, соответственно, выглядит вот такт
```
[Connection: close]
[Host: af-desktop-web.vrts-slb.test.vertis.yandex.net]
/cars/peugeot/all/
/cars/all/
/cars/used/
/cars/new/
```

Если надо пострелять в ветку в шиве, то надо передавать заголовок `x-branch-name`. Патроны становятся вот такими:
```
[Connection: close]
[Host: af-desktop-web.vrts-slb.test.vertis.yandex.net]
[x-branch-name: protobuf-exp]
/cars/peugeot/all/
/cars/all/
/cars/used/
/cars/new/
```


