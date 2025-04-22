# Intro
This directory contains collection of yandex linux-kernel tests.

## Content
### misc
Flexiable collection of Yandex related kernel tests written on pytest3. Mostly oriented on cgroup API.
- Helpers and fixtures
  - [cgroup.py](misc/kern/cgroup.py): Cgroup-v1 wrapper
  - [disk.py](misc/kern/disk.py): block device and disk API
  - [fio.py](misc/kern/fio.py): fio tool wraper
  - [kernel.py](misc/kern/kernel.py): kernel helpers and wrapper
  - [namespace.py](misc/kern/namespace.py): namespace api wrappers
  - [pagemap.py](mis.c/kern/pagemap.py): page mapping helpers
  - [proc.py](misc/kern/proc.py): proc-fs helpers
  - [syscall.py](misc/kern/syscall.py): syscall wrappers
  - [task.py](misc/kern/task.py): task executors helpers

Current task [KERNEL-458](https://st.yandex-team.ru/KERNEL-458)
- Tests
  - Sysfs knobs tests
    - test_block_interface.py
    - test_cgroup_blkio_knobs.py
    - test_cgroup_interface.py
  - Regression tests and feature tests
    - test_cgroup_blkio_leakage.py
    - test_cgroup_memory_recharge.py
    - test_ext4_lazytime_update.py
    - test_ext4_falloc.py
    - test_fadvise_noreuse.py
    - test_ipv6_auto_flowlabels.py
    - test_madvise.py
    - test_memory_compaction_poisoning.py
    - test_mount_remount_locking.py
    - test_nvidia_module.py
    - test_porto_ptrace_kludge.py
  - Stress tests
    - test_cgroup_juggler.py
  - Performance tests, should be executed real HW. Exptects to work unreliable in distbuild.
    - test_cgroup_blkio_throttler.py
    - test_cgroup_cpuacct_knobs.py
    - test_cgroup_memory_oom.py
    - test_iostat.py
    - test_madvise_stockpile_balance.py
    - test_sched_file_idle_cpu.py
  
### recipe
Collection on test recipies 
### xfstests-bld
Arcadia harness for [xfstest-bld](https://github.com/tytso/xfstests-bld) from Tytso
**TODO** Currenlty is broken [KERNEL-264](https://st.yandex-team.ru/KERNEL-264)

## Execution environments
Misc tests compiled as library, execution environments located in [infra/kernel/ci/ut](https://a.yandex-team.ru/arc/trunk/arcadia/infra/kernel/ci/ut)
