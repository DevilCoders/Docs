BPF Features by Linux Kernel Version: https://github.com/iovisor/bcc/blob/master/docs/kernel-versions.md

Message formats:
  - String:
```
Len(uint16)
Data(w/o null byte)
```
  - Byte string:
```
Len(uint16)
Data(w/o null byte)
```
  - Event:
```
EventType(uint8)
EventSpecificMessage[see above]
EOF(0xEFBEADDE)
```
  - `EVENT_KIND_MK_CGROUP`:
```
ID(uint64)
Path(string)
```
  - `EVENT_KIND_RM_CGROUP` format:
```
ID(uint64)
```
  - `EVENT_KIND_SYSCALL` format: **TBD**

