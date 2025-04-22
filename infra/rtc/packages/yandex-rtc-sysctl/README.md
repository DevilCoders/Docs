## About
This directory contains rules to build various packages for `systemd-systcl`.

## Motivation
At RTC we have hosts which (at the moment) can have several __roles__, e.g:
  * `BERT` - hosts combined in tight cluster with fast interconnect to train BERT models
  * `DNS` - hosts hosting legacy(?) RTC dns cache services
  * `EBPF` - hosts with network parameters tuned by ebf-agent
  * `RTC` - common compute nodes
etc.

Our main bare metal deployment/configuration tool is [hostctl](https://a.yandex-team.ru/arc/trunk/arcadia/infra/hostctl) is designed to be a control plane service. I.e. it avoids configuring host/OS/kernel directly, delegating all heavy lifting to packages/systemd units/porto containers.

Thus we use:
  * `systemd-sysctl` (service) - to apply sysctl parameters upon host boot and parameters update
  * `yandex-rtc-sysctl`(package) - to bring configuration files to sysctl service

thus `hostctl` role is reduced to:
  * updating package
  * restaring sysctl service
  * reporting results

## Trick
Package is always named `yandex-rtc-sysctl` and __role__ is encoded in version suffix, e.g. `yandex-rtc-sysctl=1.0-7393027-dns`. Thus we ensure that you cannot (by accident) have **two conflicting packages** on the same host. Package names acts as slot name, with only one package in the slot at a given time.
