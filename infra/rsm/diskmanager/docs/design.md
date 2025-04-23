# Design

## Other similar projects
* [openstorage](https://github.com/libopenstorage/openstorage)
* [CSI](https://github.com/container-storage-interface/spec)

## Desing assumptions
* One disk may belongs to single VolumeGroup, for sane reliability
* Each VolumeGroup has limit of maximum number of LogicalVolumes , for sane latency
* Actions idempotence. Each action may be repeated several times.
