# mediaplan-auto
Как запускать тесты:
-Поднять среду, взять адрес на котором слушает среда(смотри как это делать тут https://github.yandex-team.ru/direct/mediaplan/blob/master/README.md)
 Диапозон портов, которые следуюет юзать 1347{0..9}
-Полученный адрес положить в direct.properties. 
 Например, так: 
 ```
 mediaplan.baseUrl = http://ppcdev6.yandex.ru:12345/mediaplan_mediaplan_v0.1_runtests_kcaaaaa_mysql/
 ``` 
-Для запуска всех тестов использовать: 
 ``` 
 mvn test -Plocal_testing

 ```
