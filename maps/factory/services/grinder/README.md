# Grinder

## General information

| What | Who |
| ---- | --- |
| Ответственные разработчики | Дмитрий Сухов (quoter@yandex-team.ru) |
| Отвественные SRE | Дмитрий Сухов (quoter@yandex-team.ru) |
| Исходники | https://a.yandex-team.ru/arc/trunk/arcadia/maps/factory/services/grinder |
| Сервис в ABC | https://abc.yandex-team.ru/services/maps-core-factory-grinder/ |
| CI (TestEnv) - Покоммитный | https://testenv.yandex-team.ru/?screen=job_history&database=maps_tests&job_name=BUILD_DOCKER_MAPS_CORE_NMAPS_MRC_GRINDER |

## Service infrastructure

### Instances, graphics, monitorings

## Service infrastructure

### Instances, graphics, monitorings

| Staging | Nanny service | Graphics panel | Monitoring checks |
| ------- | ------------- | -------------- | ----------------- |
| Stable | [maps_core_factory_grinder_stable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_factory_grinder_stable/) | [ core-factory-grinder.stable ](https://yasm.yandex-team.ru/template/panel/maps-core-factory-grinder-stable-panel-main/) | [ maps_core_factory_grinder_stable ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_factory_grinder_stable) |
| Testing | [maps_core_factory_grinder_testing](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_factory_grinder_testing/) | [ core-factory-grinder.testing ](https://yasm.yandex-team.ru/template/panel/maps-core-factory-grinder-testing-panel-main/) | [ maps_core_factory_grinder_testing ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_factory_grinder_testing) |

[Monitorings all (tag=a_prj_maps-core-factory-grinder)](https://juggler.yandex-team.ru/aggregate_checks/?query=tag%3Da_prj_maps-core-factory-grinder)

### Balancers

| Staging | Name | AWACS Balancer | Balancer Panel | Balancer Nanny services |
| ------- | ---- | -------------- | -------------- | ----------------------- |
| Stable | Default | [core-factory-grinder.maps.yandex.net](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/core-factory-grinder.maps.yandex.net/) | [core-factory-grinder.maps.yandex.net](https://yasm.yandex-team.ru/template/panel/balancer_common_panel/fqdn=core-factory-grinder.maps.yandex.net;itype=balancer;ctype=prod;locations=vla,sas,man;prj=core-factory-grinder-maps;signal=service_total) | [rtc_balancer_core-factory-grinder_maps_yandex_net_man](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-factory-grinder_maps_yandex_net_man)<br>[rtc_balancer_core-factory-grinder_maps_yandex_net_sas](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-factory-grinder_maps_yandex_net_sas)<br>[rtc_balancer_core-factory-grinder_maps_yandex_net_vla](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-factory-grinder_maps_yandex_net_vla) |
| Testing | Default | [core-factory-grinder.testing.maps.yandex.net](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/core-factory-grinder.testing.maps.yandex.net/) | [core-factory-grinder.testing.maps.yandex.net](https://yasm.yandex-team.ru/template/panel/balancer_common_panel/fqdn=core-factory-grinder.testing.maps.yandex.net;itype=balancer;ctype=prod;locations=sas;prj=core-factory-grinder-testing-maps;signal=service_total) | [rtc_balancer_core-factory-grinder_testing_maps_yandex_net_sas](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-factory-grinder_testing_maps_yandex_net_sas) |

## What happens when service is down

## Logs

| Name | URL/path |
|---|---|
| Nginx | /var/log/nginx/* |
| Yacare service | /var/log/yandex/maps/grinder/* |
| Grinder master service | /var/log/yandex/maps/factorygrinder-master/* |
| Supervisord | /var/log/supervisor/* |
| Syslog (unfiltered) | /var/log/syslog |
| YT  | https://yql.yandex-team.ru : SELECT * FROM hahn.`logs/maps-log/1d/2019-08-20` WHERE vhost LIKE 'core-factory-grinder.maps.yandex.net' limit 1; |

## How to fix common problems

### postponed-tasks

Типичное сообщение об ошибке выглядит вот так:
```
CRIT on maps_core_factory_grinder_stable:postponed-tasks
At 2022-02-27 19:03:53

Description:
2/0/3 (0/1) Error: posponed tasks - 1, the oldest task - 4h 22m (maps-core-factory-grinder-stable-2.vla.yp-c.yandex.net). Error: posponed tasks - 1, the oldest task - 4h 34m (maps-core-factory-grinder-stable-2.man.yp-c.yandex.net)
```
Сообщение говорит, что есть grinder-задача, которая не была назначена на исполнителя, подробнее про состояния задач в grinder можно почитать тут https://wiki.yandex-team.ru/maps/dev/core/grinder/#taskstatetransitions.

Как диагностировать проблему:
1) Надо выяснить, что это за задача, для этого на любом из хостов сервиса выполнить команду:
```
# /usr/lib/yandex/maps/grinder/bin/check-postponed-tasks --list --warn-timeout 30m --err-timeout 120m
621b600a6d57bc538036c86c	maps.factory.pylibs.celery.signals.signals_tiles_update.update_tiles	18h 46m
```
В данном случае мы узнаем, что задача с идентификатором `621b600a6d57bc538036c86c` и типом `maps.factory.pylibs.celery.signals.signals_tiles_update.update_tiles` находится в состоянии postponed более 18 часов.

2) Грепнуть логи `grinder-master` по этому идентификатору, удобнее всего это делать с помощью `executer`
```
[Serial] quoter> exec n:maps_core_factory_grinder_stable zgrep 621b600a6d57bc538036c86c /var/log/yandex/maps/grinder-master/grinder-master.log*

=== maps-core-factory-grinder-stable-2.man.yp-c.yandex.net (@man), 1/3 ===
/var/log/yandex/maps/grinder-master/grinder-master.log.1.gz:[2022-02-27 17:06:16] info: Master [638145_642482605@maps-core-factory-grinder-stable-2.man.yp-c.yandex.net]: received new task 621b600a6d57bc538036c86c, data: { "args" : { "task_id" : 658391, "type" : "maps.factory.pylibs.celery.signals.signals_tiles_update.update_tiles" }, "status" : 21 }
/var/log/yandex/maps/grinder-master/grinder-master.log.1.gz:[2022-02-27 17:06:16] warning: Master [638145_642482605@maps-core-factory-grinder-stable-2.man.yp-c.yandex.net]: task [621b600a6d57bc538036c86c] was started, it could not be rescheduled


Task on maps-core-factory-grinder-stable-2.man.yp-c.yandex.net exited normally with exit status 1

=== maps-core-factory-grinder-stable-1.sas.yp-c.yandex.net (@sas), 2/3 ===


Task on maps-core-factory-grinder-stable-1.sas.yp-c.yandex.net exited normally with exit status 1

=== maps-core-factory-grinder-stable-2.vla.yp-c.yandex.net (@vla), 3/3 ===


Task on maps-core-factory-grinder-stable-2.vla.yp-c.yandex.net exited normally with exit status 1
```
3) Посмотреть лог изменения статусов задачи
```
curl -sH "Host:core-factory-grinder.maps.yandex.net" 'http://localhost/tasklog/621b600a6d57bc538036c86c' | python -m "json.tool"
[
    {
        "msg": "Unsubmitted",
        "pid": "511_144502@maps-core-factory-grinder-stable-1.sas.yp-c.yandex.net",
        "status": "New",
        "ts": 1645961226662
    },
    {
        "msg": "Submitted",
        "pid": "105_134079@maps-core-factory-grinder-stable-1.sas.yp-c.yandex.net",
        "status": "New",
        "ts": 1645961226749
    },
    {
        "msg": "186_1299989749@maps-core-factory-lt-stable-3.sas.yp-c.yandex.net",
        "pid": "105_134079@maps-core-factory-grinder-stable-1.sas.yp-c.yandex.net",
        "status": "Assigned",
        "ts": 1645961226749
    },
    {
        "msg": "",
        "pid": "186_1299989749@maps-core-factory-lt-stable-3.sas.yp-c.yandex.net",
        "status": "Queued",
        "ts": 1645961226764
    },
    {
        "msg": "",
        "pid": "186_1299989749@maps-core-factory-lt-stable-3.sas.yp-c.yandex.net",
        "status": "Started",
        "ts": 1645961226778
    },
    {
        "msg": "Task exited with nonzero exit status 1\n/-S/maps/libs/common/impl/exception.cpp:41:0 in maps::Exception::Exception(std::__y1::basic_string<char, std::__y1::char_traits<char>, std::__y1::allocator<char> >) [0x227ac5f]\n/-S/maps/libs/common/impl/exception.cpp:33:0 in maps::Exception::Exception() [0x227ab75]\n/place/sandbox-data/tasks/2/4/1217139142/__FUSE/mount_path_eb6afcd2-5b40-499c-ba3a-608886f9da62/maps/tools/grinder-worker-controller/lib/worker.cpp:198:0 in maps::grinder_controller::UniversalWorker::checkTerminationStatus(maps::grinder::worker::Task const&, maps::process::ProcessStatus const&) [0x265fea6]\n/place/sandbox-data/tasks/2/4/1217139142/__FUSE/mount_path_eb6afcd2-5b40-499c-ba3a-608886f9da62/maps/tools/grinder-worker-controller/lib/worker.cpp:162:0 in maps::grinder_controller::UniversalWorker::runTask(maps::grinder::worker::Task const&) [0x265ee60]\n/place/sandbox-data/tasks/2/4/1217139142/__FUSE/mount_path_eb6afcd2-5b40-499c-ba3a-608886f9da62/contrib/libs/cxxsupp/libcxx/include/__functional/function.h:506:0 in std::__y1::__function::__value_func<void (maps::grinder::worker::Task const&)>::operator()(maps::grinder::worker::Task const&) const [0x279b65e]\n/place/sandbox-data/tasks/2/4/1217139142/__FUSE/mount_path_eb6afcd2-5b40-499c-ba3a-608886f9da62/contrib/libs/cxxsupp/libcxx/include/__functional/function.h:1190:0 in std::__y1::function<void (maps::grinder::worker::Task const&)>::operator()(maps::grinder::worker::Task const&) const [0x279b65e]\n/place/sandbox-data/tasks/2/4/1217139142/__FUSE/mount_path_eb6afcd2-5b40-499c-ba3a-608886f9da62/maps/tools/grinder/worker/worker.cpp:691:0 in maps::grinder::worker::WorkerNode::Impl::executeHandler(maps::grinder::worker::WorkerNode::Impl::TaskState const&, std::__y1::function<void (maps::grinder::worker::Task const&)>) [0x279b65e]\n/place/sandbox-data/tasks/2/4/1217139142/__FUSE/mount_path_eb6afcd2-5b40-499c-ba3a-608886f9da62/maps/tools/grinder/worker/worker.cpp:629:0 in maps::grinder::worker::WorkerNode::Impl::handleTask(std::__y1::shared_ptr<maps::grinder::worker::WorkerNode::Impl::TaskState>, std::__y1::function<void (maps::grinder::worker::Task const&)>)::'lambda'()::operator()() const [0x279acae]\n/place/sandbox-data/tasks/2/4/1217139142/__FUSE/mount_path_eb6afcd2-5b40-499c-ba3a-608886f9da62/contrib/restricted/boost/boost/asio/handler_invoke_hook.hpp:69:0 in void boost::asio::asio_handler_invoke<maps::grinder::worker::WorkerNode::Impl::handleTask(std::__y1::shared_ptr<maps::grinder::worker::WorkerNode::Impl::TaskState>, std::__y1::function<void (maps::grinder::worker::Task const&)>)::'lambda'()>(maps::grinder::worker::WorkerNode::Impl::handleTask(std::__y1::shared_ptr<maps::grinder::worker::WorkerNode::Impl::TaskState>, std::__y1::function<void (maps::grinder::worker::Task const&)>)::'lambda'()&, ...) [0x279a7c4]\n/place/sandbox-data/tasks/2/4/1217139142/__FUSE/mount_path_eb6afcd2-5b40-499c-ba3a-608886f9da62/contrib/restricted/boost/boost/asio/detail/handler_invoke_helpers.hpp:37:0 in void boost_asio_handler_invoke_helpers::invoke<maps::grinder::worker::WorkerNode::Impl::handleTask(std::__y1::shared_ptr<maps::grinder::worker::WorkerNode::Impl::TaskState>, std::__y1::function<void (maps::grinder::worker::Task const&)>)::'lambda'(), maps::grinder::worker::WorkerNode::Impl::handleTask(std::__y1::shared_ptr<maps::grinder::worker::WorkerNode::Impl::TaskState>, std::__y1::function<void (maps::grinder::worker::Task const&)>)::'lambda'()>(maps::grinder::worker::WorkerNode::Impl::handleTask(std::__y1::shared_ptr<maps::grinder::worker::WorkerNode::Impl::TaskState>, std::__y1::function<void (maps::grinder::worker::Task const&)>)::'lambda'()&, maps::grinder::worker::WorkerNode::Impl::handleTask(std::__y1::shared_ptr<maps::grinder::worker::WorkerNode::Impl::TaskState>, std::__y1::function<void (maps::grinder::worker::Task const&)>)::'lambda'()&) [0x279a7c4]\n/place/sandbox-data/tasks/2/4/1217139142/__FUSE/mount_path_eb6afcd2-5b40-499c-ba3a-608886f9da62/contrib/restricted/boost/boost/asio/detail/handler_work.hpp:82:0 in void boost::asio::detail::handler_work<maps::grinder::worker::WorkerNode::Impl::handleTask(std::__y1::shared_ptr<maps::grinder::worker::WorkerNode::Impl::TaskState>, std::__y1::function<void (maps::grinder::worker::Task const&)>)::'lambda'(), boost::asio::system_executor>::complete<maps::grinder::worker::WorkerNode::Impl::handleTask(std::__y1::shared_ptr<maps::grinder::worker::WorkerNode::Impl::TaskState>, std::__y1::function<void (maps::grinder::worker::Task const&)>)::'lambda'()>(maps::grinder::worker::WorkerNode::Impl::handleTask(std::__y1::shared_ptr<maps::grinder::worker::WorkerNode::Impl::TaskState>, std::__y1::function<void (maps::grinder::worker::Task const&)>)::'lambda'()&, maps::grinder::worker::WorkerNode::Impl::handleTask(std::__y1::shared_ptr<maps::grinder::worker::WorkerNode::Impl::TaskState>, std::__y1::function<void (maps::grinder::worker::Task const&)>)::'lambda'()&) [0x279a7c4]\n/place/sandbox-data/tasks/2/4/1217139142/__FUSE/mount_path_eb6afcd2-5b40-499c-ba3a-608886f9da62/contrib/restricted/boost/boost/asio/detail/completion_handler.hpp:70:0 in boost::asio::detail::completion_handler<maps::grinder::worker::WorkerNode::Impl::handleTask(std::__y1::shared_ptr<maps::grinder::worker::WorkerNode::Impl::TaskState>, std::__y1::function<void (maps::grinder::worker::Task const&)>)::'lambda'()>::do_complete(void*, boost::asio::detail::scheduler_operation*, boost::system::error_code const&, unsigned long) [0x279a7c4]\n/place/sandbox-data/tasks/2/4/1217139142/__FUSE/mount_path_eb6afcd2-5b40-499c-ba3a-608886f9da62/contrib/restricted/boost/boost/asio/detail/scheduler_operation.hpp:40:0 in boost::asio::detail::scheduler_operation::complete(void*, boost::system::error_code const&, unsigned long) [0x264e686]\n/place/sandbox-data/tasks/2/4/1217139142/__FUSE/mount_path_eb6afcd2-5b40-499c-ba3a-608886f9da62/contrib/restricted/boost/boost/asio/detail/impl/scheduler.ipp:401:0 in boost::asio::detail::scheduler::do_run_one(boost::asio::detail::conditionally_enabled_mutex::scoped_lock&, boost::asio::detail::scheduler_thread_info&, boost::system::error_code const&) [0x264e686]\n/place/sandbox-data/tasks/2/4/1217139142/__FUSE/mount_path_eb6afcd2-5b40-499c-ba3a-608886f9da62/contrib/restricted/boost/boost/asio/detail/impl/scheduler.ipp:154:0 in boost::asio::detail::scheduler::run(boost::system::error_code&) [0x264e0d0]\n/place/sandbox-data/tasks/2/4/1217139142/__FUSE/mount_path_eb6afcd2-5b40-499c-ba3a-608886f9da62/contrib/restricted/boost/boost/asio/impl/io_context.ipp:62:0 in boost::asio::io_context::run() [0x269aeb4]\n/place/sandbox-data/tasks/2/4/1217139142/__FUSE/mount_path_eb6afcd2-5b40-499c-ba3a-608886f9da62/maps/tools/grinder/worker/api.cpp:233:0 in maps::grinder::worker::run(maps::grinder::worker::Options const&)::$_1::operator()() const [0x269aeb4]\n/place/sandbox-data/tasks/2/4/1217139142/__FUSE/mount_path_eb6afcd2-5b40-499c-ba3a-608886f9da62/contrib/libs/cxxsupp/libcxx/include/type_traits:3716:0 in decltype(static_cast<maps::grinder::worker::run(maps::grinder::worker::Options const&)::$_1>(fp)()) std::__y1::__invoke<maps::grinder::worker::run(maps::grinder::worker::Options const&)::$_1>(maps::grinder::worker::run(maps::grinder::worker::Options const&)::$_1&&) [0x269aeb4]\n/place/sandbox-data/tasks/2/4/1217139142/__FUSE/mount_path_eb6afcd2-5b40-499c-ba3a-608886f9da62/contrib/libs/cxxsupp/libcxx/include/thread:280:0 in void std::__y1::__thread_execute<std::__y1::unique_ptr<std::__y1::__thread_struct, std::__y1::default_delete<std::__y1::__thread_struct> >, maps::grinder::worker::run(maps::grinder::worker::Options const&)::$_1>(std::__y1::tuple<std::__y1::unique_ptr<std::__y1::__thread_struct, std::__y1::default_delete<std::__y1::__thread_struct> >, maps::grinder::worker::run(maps::grinder::worker::Options const&)::$_1>&, std::__y1::__tuple_indices<>) [0x269aeb4]\n/place/sandbox-data/tasks/2/4/1217139142/__FUSE/mount_path_eb6afcd2-5b40-499c-ba3a-608886f9da62/contrib/libs/cxxsupp/libcxx/include/thread:291:0 in void* std::__y1::__thread_proxy<std::__y1::tuple<std::__y1::unique_ptr<std::__y1::__thread_struct, std::__y1::default_delete<std::__y1::__thread_struct> >, maps::grinder::worker::run(maps::grinder::worker::Options const&)::$_1> >(void*) [0x269aeb4]\n???:0:0 in ??? [0x7f04057736da]\n???:0:0 in ??? [0x7f040549c71e]\n",
        "pid": "186_1299989749@maps-core-factory-lt-stable-3.sas.yp-c.yandex.net",
        "status": "Failed",
        "ts": 1645966885037
    }
]
```

4) Посмотреть логи на воркере, где задача выполнялась.

[What can go wrong in RTC](https://wiki.yandex-team.ru/users/imseleznev/whatcangowronginrtc)

## Documentation

- [Grinder](https://wiki.yandex-team.ru/maps/dev/core/grinder/)

## Known clients

## SLA

## Persistent Volumes

* /logs - логи, сюда ставится симлинка из /var/log

## Firewall macroses

| staging | URL |
|---|---|
| stable | [ \_MAPS_CORE_FACTORY_GRINDER_STABLE_RTC_NETS_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_CORE_FACTORY_GRINDER_STABLE_RTC_NETS_ ) |
| testing | [ \_MAPS_CORE_FACTORY_GRINDER_TESTING_RTC_NETS_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_CORE_FACTORY_GRINDER_TESTING_RTC_NETS_ ) |

## Regression Stress Testing Configurations
