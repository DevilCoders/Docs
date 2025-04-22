# Базовые панели метрик сервиса

## Панель состояния сервиса в Деплое

На вкладке Monitoring страницы стейджа в Деплое отображается агрегированная информация для выбранного deploy unit'а (выбирается в выпадающем списке, [пример](https://jing.yandex-team.ru/files/pirogov/Снимок%20экрана%202020-07-06%20в%2016.47.47.png)).

В головане панель доступна по адресу [https://yasm.yandex-team.ru/template/panel/yd-container-non-lvm-pod-level/](https://yasm.yandex-team.ru/template/panel/yd-container-non-lvm-pod-level/) и принимает на вход следующие параметры:
* hosts - агрегат (ASEARCH) или конкретный хост, метрики которого надо отобразить
* itype - itype голована, с которым собираются метрики в данном deploy unit'e
* stage - имя stage
* deploy_unit - имя deploy unit'a

В панели отображаются следующие метрики:

Имя | Сигнал в головане | Описание 
:--- | :--- | :---
**pods count** | | 
 Ready  | unistat-condition_pod_ready_ahhh  | Количество подов в состоянии Ready [детали](https://wiki.yandex-team.ru/deploy/docs/monitorings/user-sensors/objectconditions/)
 In progress  | unistat-condition_pod_in_progress_ahhh  | Количество подов в состоянии In Progress [детали](https://wiki.yandex-team.ru/deploy/docs/monitorings/user-sensors/objectconditions/)
 Failed  | unistat-condition_pod_failed_ahhh  | Количество подов в состоянии Failed [детали](https://wiki.yandex-team.ru/deploy/docs/monitorings/user-sensors/objectconditions/)
**events**  | | 
 Starts  | portoinst-starts_summ | Если сигнал равен 1 — то за последний период сбора статистики Голованом (5 сек) этот контейнер рестартовал хотя бы один раз, притом это должен быть именно рестарт (имя контейнера осталось тем же, а время его запуска поменялось), а не перевыкатка (имя меняется) (старт контейнера сразу после создания за рестарт не считается и сигнал на него не реагирует)
 OOM  | hsum(portoinst-ooms_slot_hgram)  | Число OOM-убийств в контейнере
 Crashes  | hsum(portoinst-cores_total_hgram)  | Количество попыток Porto отложить корку
 Cores  | hsum(portoinst-cores_dumped_hgram)  | Количество корок, реально сохраненных на диск
**usage percentage** | | 
 Memory usage of memory limit avg,Memory usage of memory limit quant=99 | havg(portoinst-memory_limit_usage_perc_hgram), quant(portoinst-memory_limit_usage_perc_hgram, 99) | Процент использования лимита памяти. Вычисляется как 100 * memory_usage / memory_limit_total
 Anon usage of anon limit avg, Anon usage of anon limit quant=99  | havg(portoinst-anon_limit_usage_perc_hgram), quant(portoinst-anon_limit_usage_perc_hgram, 99)  | Объем используемой анонимной памяти в процентах от лимита. Вычисляется как 100 * anon_usage / anon_limit_total (or memory_limit_total)
 Memory unevictable usage of memory limit avg, Memory unevictable usage of memory limit quant=99  | havg(portoinst-memory_unevictable_limit_usage_perc_hgram), quant(portoinst-memory_unevictable_limit_usage_perc_hgram, 99)  | Объем unevictable памяти в процентах от гарантии. Вычисляется как 100 * memory_total_unevictable / memory_guarantee_total
 Memory anon unevictable usage of memory limit avg, Memory anon unevictable usage of memory limit quant=99  | havg(portoinst-memory_anon_unevict_limit_usage_perc_hgram), quant(portoinst-memory_anon_unevict_limit_usage_perc_hgram, 99)  | Объем анонимной unevictable памяти в процентах от гарантии. Вычисляется как 100 * memory_total_unevictable / memory_guarantee_total
 CPU cores usage of CPU limit avg, CPU cores usage of CPU limit quant=99  | havg(portoinst-cpu_limit_usage_perc_hgram), quant(portoinst-cpu_limit_usage_perc_hgram, 99)  | Потребление CPU всеми процессами контейнера в процентах от лимита
 CPU cores system usage of CPU limit avg, CPU cores system usage of CPU limit quant=99  | havg(portoinst-cpu_system_limit_usage_perc_hgram), quant(portoinst-cpu_system_limit_usage_perc_hgram, 99)  | Потребление CPU всеми процессами контейнера, потраченное на исполнение системных вызовов, выраженное в процентах от лимита
**cpu cores** | | 
 CPU Usage avg, CPU Usage quant=99  | havg(portoinst-cpu_usage_slot_hgram), quant(portoinst-cpu_usage_slot_hgram, 99)  | Потребление CPU всеми процессами контейнера, ядер 
 CPU Wait avg, CPU Wait quant=99  | havg(portoinst-cpu_wait_slot_hgram), quant(portoinst-cpu_wait_slot_hgram, 99)  | Суммарное время ожидания процессов контейнера в очереди
 CPU Throttled avg, CPU Throttled quant=99  | havg(portoinst-cpu_throttled_slot_hgram), quant(portoinst-cpu_throttled_slot_hgram, 99)  | Метрика, показывающая сколько времени процесс провел в состоянии throttled
 CPU Guarantee min, CPU Guarantee max  | quant(portoinst-cpu_guarantee_slot_hgram, min), quant(portoinst-cpu_guarantee_slot_hgram, max)  | Объем процессорного времени, которое "гарантируется" контейнеру в течении интервала
 CPU Limit min, CPU Limit max  | quant(portoinst-cpu_limit_slot_hgram, min), quant(portoinst-cpu_limit_slot_hgram, max)  | Объем процессорного времени, выраженный в ядрах, который контейнер не может превысить за 1 секунду
**memory, gb** | | 
 Mem Usage avg, Mem Usage quant=99  | conv(havg(portoinst-memory_usage_slot_hgram), Gi), conv(quant(portoinst-memory_usage_slot_hgram, 99), Gi)  | Общий объем физических страниц контейнера (файловый кэш + anon), GB
 Mem Guarantee min, Mem Guarantee max  | conv(quant(portoinst-memory_guarantee_slot_hgram, min), Gi), conv(quant(portoinst-memory_guarantee_slot_hgram, max), Gi)  | Объем (минимальный и максимальный) гарантии контейнера по памяти, GB
 Mem Limit min, Mem Limit max  | quant(portoinst-memory_limit_slot_hgram, min), quant(portoinst-memory_limit_slot_hgram, max)  | Абсолютное значение потребления памяти, больше которого контейнер съесть не может, GB
 Anon Usage avg, Anon Usage quant=99  | havg(portoinst-anon_usage_slot_hgram), quant(portoinst-anon_usage_slot_hgram, 99)  | Объем используемой анонимной памяти контейнера, GB
 Anon Limit min, Anon Limit max  | quant(portoinst-anon_limit_slot_hgram, min), quant(portoinst-anon_limit_slot_hgram, max)  | Абсолютное значение потребления анонимной памяти, больше которого контейнер съесть не может, GB
**Page faults** | | 
 major page faults/s  | portoinst-major_page_faults_summ  | Общее количество major pagefault, в процессе которого необходимо выполнить операцию чтения с блочного/внешнего устройства - если соответсвующей страницы файла нет в кэше
 minor page faults/s  | portoinst-minor_page_faults_summ  | Количество событий (первых) обращений к виртуальной странице, при которых аллоцируется соответствующая страница физической памяти
**Network MBps** | | 
 TX MBps  | portoinst-net_mb_summ  | Исходящий трафик, MBps
 RX MBps (MTN)  | portoinst-net_rx_mb_summ  | Входящий трафик, MBps
 Fastbone TX MBps  | portoinst-net_fastbone_mb_summ  | Исходящий fastbone трафик, MBps
 Fastbone RX MBps  | portoinst-net_fastbone_rx_mb_summ  | Входящий fastbone трафик, MBps
 TX guarantee MBps  | portoinst-net_guarantee_mb_summ  | Общая сетевая гарантия (на все интерфейсы)
 TX limit MBps  | portoinst-net_limit_mb_summ  | Общий сетевой лимит (на все интерфейсы)
**Network pps** | | 
 TX pps  | portoinst-net_packets_summ  | Количество переданных пакетов, шт/с
 RX pps  | portoinst-net_rx_packets_summ  | Количество принятных пакетов , шт/с
 Fastbone TX pps  | portoinst-net_fastbone_packets_summ  | Количество пакетов, переданных по Fastbone, шт/с
 Fastbone RX pps  | portoinst-net_fastbone_rx_packets_summ  | Количество пакетов, принятных по Fastbone шт/с
 TX Drops  | portoinst-net_drops_summ  | Количество исходящих пакетов, которые контейнер дропнул, шт
 RX Drops  | portoinst-net_rx_drops_summ  | Количество входящих пакетов, которые контейнер дропнул, шт
 Fastbone TX Drops  | portoinst-net_fastbone_drops_summ  | Количество исходящих Fastbone пакетов, которые контейнер дропнул, шт
 Fastbone RX Drops  | portoinst-net_fastbone_rx_drops_summ  | Количество входящих Fastbone пакетов, которые контейнер дропнул, шт
**Disk total MBps** | | 
 FS write MBps  | portoinst-io_write_fs_bytes_tmmv  | Запись в файловую систему, MBps
 FS read MBps  | portoinst-io_read_fs_bytes_tmmv  | Чтение из файловой системы, MBps
 Disk write MBps  | portoinst-io_write_bytes_tmmv  | Запись на диск, MBps
 Disk read MBps  | portoinst-io_read_bytes_tmmv  | Чтение с диска, MBps
 /place write MBps  | portoinst-io_write_bytes_/place_tmmv  | Запись в /place, MBps
 /place read MBps  | portoinst-io_read_bytes_/place_tmmv  | Чтение из /place, MBps
 /ssd write MBps  | portoinst-io_write_bytes_/ssd_tmmv  | Запись в /ssd, MBps
 /ssd read MBps  | portoinst-io_read_bytes_/ssd_tmmv  | Чтение из /ssd, MBps
 /write MBps  | portoinst-io_write_bytes_/_tmmv  | Запись в /, MBps
 /read MBps  | portoinst-io_read_bytes_/_tmmv  | Чтение из /, MBps
**Disk total IOps** | | 
 FS iops  | portoinst-io_ops_fs_tmmv  | Количество i/o операций с файловой системой
 Disk iops  | portoinst-io_ops_tmmv  | Количество i/o операций с диском
 I/O load max  | portoinst-io_load_max  | Рассчитывается на основе суммарного выполнения времени IO-запросов контейнера за фиксированный интервал времени и значение можно интерпретировать как "глубину очереди" к диску. Чем величина выше - тем выше нагрузка на диск.
 /place iops, /ssd iops, /iops  | portoinst-io_ops_/place_tmmv,portoinst-io_ops_/ssd_tmmv portoinst-io_ops_/_tmmv  | Общее количество операций i/o к соответствующему mount point
 /place disk signal count, /ssd disk signal count, /disk signal count  | portoinst-io_read_bps_/place_hgram,portoinst-io_read_bps_/ssd_hgram,portoinst-io_read_bps_/_hgram  | Скорость чтения из раздела, байт/с
**Logs**  | | 
 Transferred Logs, MB  | unistat-pod_agent_logs_transmitter_transfered_raw_logs_deee  | Объем переданных логов, MB
 Lost logs rotated by pod_agent  | unistat-pod_agent_logs_transmitter_lost_logs_rotated_by_pod_agent_deee  | Объем логов, потерянных из-за ротации подагента, байт
 Lost logs rotated by porto  | unistat-pod_agent_logs_transmitter_lost_logs_rotated_by_porto_deee  | Объем логов, потерянных из-за ротации порто, байт



## Панель состояния хоста, на котором живет Pod сервиса Деплоя

Панель позволяет посмотреть на основных системные метрики живости хоста и хостовой инсрафтруктуры.
Панель доступна по адресу https://yasm.yandex-team.ru/template/panel/Host/, принимает следующие параметры:
* hosts - fqdn dom0-хоста, метрики которого надо отобразить

В панели отображаются следующие метрики:

Имя | Сигнал в головане | Описание 
:--- | :--- | :---
**Selection size** | | 
 Hosts  | hcount(cpu-us_hgram)  | Количество хостов, с которых снимаются данные мониторинги
**ISS** | | 
 Agents  | unistat-agent.configurations.all_ahhh | количество iss-агентов
 Configurations  | unistat-agent.configurations.all_ahhh | количество конфигураций на хосте
 Active  | unistat-agent.configurations.active_ahhh | количество активных конфигураций на хосте
**System Load quant=99** | | 
 Active tasks  | sum(quant(cpu-usage_cores_hgram, 99), 
quant(cpu-wait_cores_hgram, 99)) | сумма потребления CPU всеми процессами хоста и ожидания процессов в очереди, ядер
 Loadavg  | loadavg-abs_xhhh | Cредняя загрузка хоста
 Context switches/s  | cpu-context_switches_hgram | количество context switch'ей
 Task forks/s  | cpu-task_forks_hgram | количество форков
 Interrupts/s  | cpu-interrupts_hgram | количество прерываний на всех  ядрах
 Soft Interrupts/s  | cpu-soft_interrupts_hgram | количество прерываний, обрабатывающихся в отложенном режиме
**CPU % quant=99, avg** | | 
 System %  | cpu-sy_hgram | % времени, проводимом CPU в  kernel space
 User %  | cpu-us_hgram | % времени, проводимом CPU в user space
 Idle %  | cpu-id_hgram | % времени, проводимом CPU в состяоянии idle
**CPU cores quant=99, avg** | | 
 System  | cpu-usage_system_cores_hgram | Потребление CPU всеми процессами хоста, потраченное на исполнение системных вызовов, ядер
 Used  | cpu-usage_cores_hgram | потребление CPU всеми процессами хоста, ядер
 Idle  | cpu-idle_cores_hgram | количество ядер в состоянии idle
 Wait  | cpu-wait_cores_hgram | суммарное время ожидания процессов в очереди
**Memory GB quant=99, avg** | | 
 Used GB  | mem-used_thhh | Объем использованной памяти = (общее количество памяти - объем свободной памяти - объем кэша), Mb
 Available GB  | mem-free_thhh | Объем свободной памяти + объем кэша, Mb
 Shmem/tmpfs GB  | mem-shmem_hgram | Объем памяти, шареной между процессами (shmem and tmpfs), GB
 Cache GB  | mem-cache_thhh | Объем, занятый в ОЗУ под кэш чтения страниц с диска (файлы, директории, файлы блочных устройств, данные, относящиеся к механизму IPC, данные процессов уровня пользователя, сброшенных в область подкачки), GB
 Dirty GB  | mem-dirty_hgram | Объем "грязной" памяти (память, представляющая данные на диске, которые были изменены, но еще не были записаны на диск), GB
 Total GB  | mem-total_thhh | Общее количество памяти, GB
**Cgroups count** | | 
 cpu,memory,blkio,total  | cgroup-\<subsystem\>_count_hgram | количество cgroup в соответствующей подсистеме (и всего)
**Open files and sockets** | | 
 FD used  | fdstat-fd_used_hgram | количество использованных файловых дескрипторов
 FD limit  | fdstat-fd_available_hgram | лимит файловых дескрипторов
**Local DNS cache** | | 
 AAAA/A/MX/PTR requests  | service_bind-in_<AAAA,A,MX,PTR>_hgram, | количество соответствующих запросов к локальному DNS cache
 AAAA/A cache miss  | service_bind-out_<AAAA,A>_hgram, | количество промахов мимо кэша
 NXDOMAIN/SERVFAIL responses  | service_bind-nss_<NXDOMAIN,SERVFAIL>_hgram | количество NXDOMAIN/SERVFAIL ответов
**Network MBps** | | 
 Uplink RX MBps  |sum(netstat-ibytes-eth<0|1|2|3|4|5>_summ)| Суммарное по сетевым интерфейсам количество принятых байт
 Uplink TX MBps  |sum(netstat-obytes-eth<0|1|2|3|4|5>_summ)| Суммарное по сетевым интерфейсам количество переданных байт
 MTN \<Network\> RX MBps  | netstat-ibytes-vlanXXX_summ | Количество байт, принятых в соответствующем VLAN
 MTN \<Network\> TX MBps  | netstat-obytes-vlanXXX_summ | Количество байт, переданных в соответствующем VLAN
**Network pps** | | 
 Uplink RX pps  |sum(netstat-ipkts-eth<0|1|2|3|4|5>_summ)| Суммарное по сетевым интерфейсам количество принятых пакетов
 Uplink TX pps  |sum(netstat-opkts-eth<0|1|2|3|4|5>_summ)| Суммарное по сетевым интерфейсам количество переданных пакетов
 MTN \<Network\> RX pps  | netstat-ipkts-vlanXXX_summ | Количество пакетов, принятых в соответствующем VLAN
 MTN \<Network\> TX pps  | netstat-opkts-vlanXXX_summ | Количество пакетов, переданных в соответствующем VLAN
**Network Drop pps** | | 
 Uplink RX Drop pps  |sum(netstat-idrops-eth<0|1|2|3|4|5>_summ)| Суммарное по сетевым интерфейсам количество дропнутых входящих пакетов
 Uplink TX Drop pps  |sum(netstat-odrops-eth<0|1|2|3|4|5>_summ)| Суммарное по сетевым интерфейсам количество дропнутых исходящих пакетов
 Uplink RX Error pps  |sum(netstat-ierrs-eth<0|1|2|3|4|5>_summ)| Суммарное по сетевым интерфейсам количество ошибок приема
 Uplink TX Error pps  |sum(netstat-oerrs-eth<0|1|2|3|4|5>_summ)| Суммарное по сетевым интерфейсам количество ошибок передачи
 MTN \<Network\> RX Drop pps  | netstat-idrops-vlanXXX_summ | Количество дропнутых входящих пакетов в соответствующем VLAN
 MTN \<Network\> TX Drop pps  | netstat-odrops-vlanXXX_summ | Количество дропнутых исходящих пакетов в соответствующем VLAN
 MTN \<Network\> RX Error pps  | netstat-ierrs-vlanXXX_summ | Количество ошибок приема в соответстующем VLAN
 MTN \<Network\> TX Error pps  | netstat-oerrs-vlanXXX_summ | Количество ошибок передачи в соответстующем VLAN
**/, /home, /place, /ssd Disk IO** | | 
 read MBps  | disk-read_bytes_<mount_point>_tmmv | Объем чтения из соответствующего раздела, MBps
 write MBps  | disk-write_bytes_<mount_point>_tmmv | Объем записи в соответствующий раздел, MBps
 trim MBps  | disk-trim_bytes_<mount_point>_tmmv | Объем потриманных (при помощи fstrim) данных, MBps
 read iops  | disk-read_ops_<mount_point>_tmmv | Количество операций чтения из соответствующего раздела
 write iops  | disk-write_ops_<mount_point>_tmmv | Количество операций записи в соответствующий раздел
 trim iops  | disk-trim_ops_<mount_point>_tmmv | Количество операций трима данных
 read depth  | disk-read_time_<mount_point>_tmmv | Общее время чтения
 write depth  | disk-write_time_<mount_point>_tmmv | Общее время записи
**/, /home, /place, /ssd Disk Space** | | 
 max used %  | 100 - quant(disk-avail_space_perc_<mount_point>_thhh, min) | Процент использованного дискового пространства
 min avail %  | disk-avail_space_perc_<mount_point>_thhh | Процент доступного дискового пространства
 sum used GB  | disk-usage_space_gb_<mount_point>_tmmv | Объем использованного дискового пространства, Гб
 min avail GB  | disk-avail_space_gb_<mount_point>_tnnv | Объем доступного дискового пространства, Гб
 sum used inodes  | disk-usage_inode_<mount_point>_tmmv | Количество использованных файловых inode
 min avail inodes  | disk-avail_inode_<mount_point>_tnnv | Количество доступных файловых inode
