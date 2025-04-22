## How to compile and run

```
# if there is no arcadia
svn checkout svn+ssh://arcadia.yandex.ru/arc/trunk/arcadia/ --depth files

# change dir to arcadia
cd arcadia

# compile tool
./ya make --checkout maps/wikimap/mapspro/tools/feedback_manipulation/

# run tool
maps/wikimap/mapspro/tools/feedback_manipulation/feedback_manipulation --config '/home/miror/arcadia/maps/wikimap/mapspro/cfg/services/services.testing_p.xml' --operation deploy 2116931
```
