# ```CASES FOR TESTING```

**0. Все примеры в [песочнице](https://tech.yandex.ru/maps/jsbox/2.1/).**

**1. Должен накладываться baseUrl на относительный адрес в шаблоне. На стенде должны открываться ссылки.**  
[LINK](https://jsfiddle.net/nhmqky6L/)

**2. Должны отображаться полигоны.**  
[LINK 1](https://jsfiddle.net/1dkubxLs/1/)  
[LINK 2](https://jsfiddle.net/5h2arxuj/)  
[LINK 3](https://jsfiddle.net/qjf18xhe/)  
[LINK 4](https://jsfiddle.net/5vmutjps/)  

**4. Должны ответить 400.**  
```/services/geoxml/1.2/geoxml.xml?callback=id_155853637022396927119&url=http://8.direkt.z8.ru/shops/placemarks/0/```
```/services/geoxml/1.2/geoxml.xml?callback=id_15584404300633633818&url=http://alyniekka.com/se0ga/track2.gpx```

**5. Проверить кодировку.**  
```
/services/geoxml/1.2/geoxml.xml?callback=id_155853685540012218930&url=http://www.aptekar76.ru/yandex.php
/services/geoxml/1.2/geoxml.xml?callback=id_155853723956966219363&url=http://sebrant.ru/baloon_02.xml
/services/geoxml/1.2/geoxml.xml?callback=id_15587094511281194650&url=http://seldon.ru/maps/address_dealer_list_of_fillial.xml?ver=20180531
/services/geoxml/1.2/geoxml.xml?callback=id_154469334114190304723&url=https://cdnd5x.arora.pro/upload/65831727-1b18-4b8f-9102-06930ed20ba1/file_manager/dostavka-perm.ru/kml/map.kml
```

**6. Должен присутствовать тег \<\br \/\>.**  
```/services/geoxml/1.2/geoxml.xml?callback=id_15585381281036739015&url=https://www.askona.ru/getyml.php?city=10000092&country=%D0%A0%D0%BE%D1%81%D1%81%D0%B8%D1%8F&yahash=526```

**7. Проверить содержмиое ответа.**  
```
/services/geoxml/1.2/geoxml.xml?callback=id_155870091880526639140&url=https://maps.yuga.ru/ymaps/PBFZTCFjPBO3PCEj4BkxPCEj4ZnnipiHVyGk7WioqfOzl8PBcQAIrfckTyGOLCcn6fcHTfHhavGHLCmj6qFyP1nZi1HBLkhItJdfc0PZ7qDBLkhNPpiOr09D90A0cQxk98YDcJaMrJa0rx.xml?_=1558333260
/services/geoxml/1.2/geoxml.xml?callback=id_155870322997864348950&url=http://pet.spb.agisinfo.ru/infobase/23761/ymap
/services/geoxml/1.2/geoxml.xml?callback=id_155870697550141996401&url=http://maps.yandex.ru/export/usermaps/EV5LVY-Pl5mG7Mk2SzwEcmNWdQaStkKm/
```

**8. В балунах должны быть нормальные данные.**  
[LINK 1](https://jsfiddle.net/sbfnLpwz/)  
[LINK 2](https://jsfiddle.net/tqhsmyz5/)  
[LINK 3](https://jsfiddle.net/owd5r4ef/)  
[LINK 4](https://jsfiddle.net/atycf60n/)  
[LINK 5](https://jsfiddle.net/s8ekL4bw/)  

**9. Должна быть метка.**  
[LINK](https://jsfiddle.net/Lposa9bh/2/)

**10. Не падать на большом файле.**  
```/services/geoxml/1.2/geoxml.xml?callback=id_155879755981643894502&url=https://www.seven-sky.net/map/polygon117.xml?9```

**11. Должны появляться полигоны.**  
[LINK 1](https://jsfiddle.net/kqrLszc9/)  
[LINK 2](https://jsfiddle.net/pd70124a/)  
[LINK 3](https://jsfiddle.net/argc4tvw/)  
[LINK 4](https://jsfiddle.net/qwjh21yd/)  
[LINK 5](https://jsfiddle.net/nwzubkyL/)  
[LINK 6](https://jsfiddle.net/csbjhLtv/)  
