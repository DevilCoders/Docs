[![build status](https://teamcity.yandex-team.ru/app/rest/builds/buildType:DataUI_Instruments_SolomonSensors/statusIcon.svg)](https://teamcity.yandex-team.ru/viewType.html?buildTypeId=DataUI_Instruments_SolomonSensors)[![oko health](https://badger.yandex-team.ru/oko/repo/data-ui/sensors/health.svg)](https://oko.yandex-team.ru/repo/data-ui/sensors)

# sensors
js/ts библиотека сенсоров соломона.

### Виды сенсоров (https://wiki.yandex-team.ru/solomon/userguide/datamodel/#types):
1) DGAUGE
2) RATE
3) COUNTER

остальные автору не понадобились, поэтому их нет, но все можно исправить!

### Как работает
Registry предоставляет публичные методы-фабрики сенсоров, где эти сенсоры регистрируются в хранилище. ДЛя получения сенора просто импортим вызываем соотвествующий ему метод. Первым аргументом необходимо передать имя для сенсора, вторым - опциональные лейблы. Два сенсора с одинаковым именем, но разным набором лейблов считаются разными.
Для сбора данных есть метод getData(), он так же очистит значения в каждм сенсоре, при этом сенсор пересоздавать не нужно, т.к. сам объект для значения не затирается.

### Бибилотека не занимается отправкой данных в соломон, т.к. это можно сделать многими способами. Задача библиотеки - только накопление произволных сенсоров.
