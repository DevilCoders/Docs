Микросервис для cdn-cfg: service-discovery:

* предполагаем что сверху есть l3 балансер [1]
* предоставление api для клиентов вида

# получить соответствующие ноды с сервисами etcd/redis/...
GET api/v1.0/services/etcd/endpoints/{online,offline,all}
GET api/v1.0/services/redis/endpoints/{online,offiline,all}

online == default

# получить все peers cdn-cfg
GET api/v1.0/services

[1] cdn-cfg.tt.yandex.net 80/tcp, 2379/tcp redis?

Клиент side:  следующая логика service discovery:
* получить все сконфигурированные endpoints:

  GET api/v1.0/services/etcd/endpoints

* выбрать те которые online, или один (ближайший?) хранить 
  rtt для каждого соединения? если нет - выбирать один 
  рандомный, для этого нужен метод
  если клиент хочет учитывать rtt (выбирать наилучший)

  POST api/v1.0/services/etcd/metrics {rtt:... operations
  timers}

Сервис side:
* периодически каждая нода независимо по конфигурации сервисов
  делает опрос живости всех пиров (в том числе локального), записывает
  эту информацию в map? shared map?
