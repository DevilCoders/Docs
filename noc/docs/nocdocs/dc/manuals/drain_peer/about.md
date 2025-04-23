# Как снять трафик со стыка

Повесить тэг "нагрузка снята" в racktables на сеть в стыке и сделать:
```
./ann deploy -g peerings <border name>
```
При этом маршруты на экспорт пропадут, а на импорт проставится local-preference=10, если трафик со стыка не ушёл, стоит сделать noimport=True на сессии через конфиг nodeconfigs/jsdb/external-peers.py