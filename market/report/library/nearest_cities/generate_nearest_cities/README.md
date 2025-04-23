Get geobase for Russia:

http://geoexport.yandex.ru/?format=xml&types=0,1,2,3,4,5,6,7,8,9,10,11,12,13,14,15&fields=id,parent,name,type,locative,preposition,genitive,accusative,syn,lat,lon,chief_region,tz_offset,en_name,population&root=225

Run:

./generate_nearest_cities geobase225.xml nearest_regions.json already_big_regions.json

