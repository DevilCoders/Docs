#
#
#
# cc-core/selfdns-api
cc-core is a core for dns-api/dns-mgmt processing. It implements basic core processes for dns objects used in different dns services: selfdns-api, dns-api, dns-mgmt. Right now cc-core and selfdns-api are running as a single process, but it should be splitted later.
cc-core objects:
- topology (acl.json) - a map for namepspaces and subjects (users and groups)
- zones - dynamic zones delegated nsupdate enabled
- subjects - users and groups as defined in abc scopes

# backlog
- добавить/протестировать multiple A/AAAA записи в requested context
- отделить cc-core и selfdns-api, чтобы правильно всё сделать не хватило усилий для первой итерации
- собрать конфигурацию и, видимо, дописать какого-то кода ещё для selfdns-api.yandex.net, в настоящее время этот инстанс обслуживает только selfdns-api.cloud.yandex.net тут цель такая отделить уровень представления acl от физической модели зон
- добавить прототипно dns-api как отдельного потребителя cc-core
- (добавить) источники данных в cc-core: zones via xml/rt
- (добавить) источники данных в cc-core: mtn networks
- (добавить) источники данных в cc-core: abc+roles, варианты с abc+scopes реализован
- (добавить) источники данных в cc-core: macroses 
- матчинг ip адресов через rbt
- acl refactoring, сейчас есть acl1, acl2, acl3(mto)
- core function to update zone via: batching
- (3.1) nsupdate protocol
- (3.2) yp-client protocl (via ..) as ipmi zone update is implemented
- (3.3) different one more scheme ...
- (4.1) oauth functions
- (4.2) shared secret functions

- кешировать что можно в redis local, сейчас весь кеш в памяти - для инстанса Облака - это более-менее ок, кеш прогревается 10 секунд после рестарта, в больших конфигурациях это будет минуты (основное время на zookeeper конфигурации update)

функции: store cache (objects) в cc-core, read cache в cc-mgmt
