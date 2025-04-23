# Failure types

При создании новой задачи Wall-E может передавать информацию о типе ошибки, из-за которой задействована автоматика.

Ниже представлен перечень этих ошибок.

## Проблемы материнской платы

* `bmc_ipmi`
* `bmc_ip_dns`
* `bmc_battery`
* `bmc_voltage`
* `bmc_other`

## Проблемы сети

* `link_malfunction`
* `link_rx_crc_errors`

## Проблемы оперативной памяти

* `mem_ecc`
* `mem_size`
* `mem_numa`
* `mem_speed`

## Проблемы накопителя

* `disk_bad_cable`
* `disk_performance`
* `disk_bad_blocks`
* `disk_unknown`
* `disk_no_check_info`
* `disk_common`

## Проблемы GPU

* `gpu_missing`
* `gpu_availability`
* `gpu_overheat`
* `gpu_capping`
* `gpu_bandwidth_too_low`
* `gpu_retired_pages`
* `gpu_power_capping`
* `gpu_retired_pages_pending`

## Проблемы CPU

* `cpu_failure`
* `cpu_capped`
* `cpu_overheated`

## Проблемы software и прочее

* `availability`
* `missing_passive_checks`
* `kernel_tainted`
* `many_reboots`
* `fs_check`
* `uplink_common`
* `rack_overheat`
* `rack_common`
* `2nd_time_node`