# Автоматическое назначение тегов
Существуют кроны, которые в автоматическом режиме могут назначать и снимать некоторые теги с объектов и сетей.  
В большинстве они определены в plugins/tags-auto-recalc.php. Если существуют другие запчасти со схожей функциональностью имеет смысл их перенести туда.
Например из scripts/auto-tags.php
Иногда их называют автоматическими тегами, но не стоит их путать с автотегами. Автотеги в текущей реализации расчитываются автоматически при подгрузке
объектов и фактически отсутствуют в дереве тегов. В случае автоматического назначения тегов используются теги именно из дерева.

# Пересчёт геотегов серверных свитчей по тегам их Dшек (recalcPerDTorTags)
Сейчас работает только для Мытищи.d1/Мытищи.d2  
Если у серверного свитча в Мытищах есть линк до Dшки или другого объекта с этими тегами, то геотег объекта заменяется.

# Пересчёт геотегов по геотегам стоек (recalcGeoTagsByRacks)
Работает над стойками попадающими под "[работает recalcGeoTagsByRacks]". Игнорирует устройства попадающие под "[геотег приколочен]".  
Изменяет геотег объектов на геотег стойки куда они смонтированы.  
Здесь стоит отметить то как стойки, смонтированные объекты и геотеги стоек попадают в RT. Стойки импортируются по правилам описанным в
Rackspace -> Dynamic Rows. Если расположение стойки попадает под регексп, то она будет импортирована в RT и в неё смонтируются соответсвующие объекты.
При импорте стойки на неё может быть назначен геотег в соответствии с описанными регекспами в plugins/bot-map.inc
В итоге, если стойка импортировалась, при импорте на неё назначился геотег и она попадает под "[работает recalcGeoTagsByRacks]", то всем объектам
смонтированным в неё не попадающим под "[геотег приколочен]" геотег будет изменён на геотег стойки.

# Пересчёт тега "сеть за динамическим фаерволом" для сетей (recalcDynFWNetTags)

# Пересчёт тега "серая сеть" (recalcGreyNetTags)

# Пересчёт тега "чужая сеть" (applyAlienNetTag)

# Пересчёт тега "fastbone" для fastbone-подсетей (fixFastboneMistaggedNets)

# Пересчёт модельных тегов на основе атрибутов (auto-tags.php)
