## TIKET
https://st.yandex-team.ru/SOC-2547

This is group of containers for coollecting logs via different proto and transfer them to Yandex SOC.
Supported protocols in sections __PORTS AND PROTOS__


## CONFIGURATION
All neccesary variables located in ./config/env.example
Copy this file to ./config/.env and fill with your values


## INSTALLATION AND RUN
TLDR: 
Just type make

make up - run containers
make buidl - only build containers to local registry
make logs - output logs from containers to STDOUT
make stop - stop all containers
make clean - remove containers and images
make copy - copy images to hidden host (NOT TESTED)


## SCHEME
https://drawio.yandex-team.ru/?page-id=ase9P3Zsab_aj80JM5k_#LLogger


## PORTS AND PROTOS

* 514\udp|tcp:  BSD Syslog
* ${HEC_PORT:-443\tcp}:  HTTP Event Collector
* CURRENTLY DONT USED 2055\udp: IPFIX/NetFlow v9
* CURRENTLY DONT USED 2056\udp: NetFlow v5
* ${SPLUNK_PORT:-3333\tcp}: Splunk
* ${QLOUD_HTTP_PORT}: port for osquery logs from workstations (Legacy name)
* 8089/tcp - Splunk deployment server for local installation agents

## IPV6
if your containers have to work with ipv6only resources or listen on ipv6 ports, you need to create ipv6 docker network and masquerade it with command:
ip6tables -t nat -A POSTROUTING -s <network_address/network_mask> ! -o docker0 -j MASQUERADE

## TODO
* Remove 3030 - unencrypted splunk
* Add encryption from splunk to Yandex
* Force certain index for all data.


## TEST
* Start linux server (you can use https://qyp.yandex-team.ru/ for example) with access to Internet
* Install docker (https://docs.docker.com/engine/install/ubuntu/)
* Install docker-compose: apt install docker-compose
* Install make: apt install make
* Check port with nmap: 
** nmap -Np -p 443,3333 <host>
** sudo nmap -nP -sU -p 514,2055,2056 <host>
* If box ipv6-only, enable ipv6: https://docs.docker.com/config/daemon/ipv6/


## Interesting links
* https://bitbucket.org/SPLServices/splunk-syslog-ng
* https://support.oneidentity.com/kb/261897/troubleshooting-syslog-ng