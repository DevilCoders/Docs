# About
Very basic description about hostmanager node info reports to YP


## Motivation
YP (scheduler primarily) needs to know about host hardware configuration, namely:
  * CPU - model, flags, number of cores, etc
  * RAM - volume
  * DISKS - configuration, storage class, size
  * NET - NIC model, speed, IP configuration
  * GPU - model, mode, RAM, etc
We have hostmanager, which can gather this information and report it directly to YP. This information is consumed
by some kind of adapter service, which transforms this information into YP `TResource` objects.

## Implementation details
We have several pieces:
  * protobuf definitions (ya_salt.proto:NodeInfo)
  * `hostman` attribute in `TNodeStatus` in YP proto
  * `lib/node_info` code which gathers host information

On every iteration, hostman tries to gather this information and report to YP via `SetHostStatus` gRPC call.