# OSquery

This repo contains osquery configs. They are wrapped into the debian packages for the ease of the installation.  
Osquery is an opensourced instrument for the telemetry collection. It is cross platform SQL powered userspace tool.  

## Detailed

There are several notable things here:
* ```common``` contains packs and configs. this folder is used in almost every package.
* ```osquery-vanilla``` - is the package with the binary itself and all the unit files and init.d scripts around it.
* ```osquery-yandex-generic-config``` - configs for the osquery. both packages are necessary.
* ```osquery-ycloud-mdb*``` pacakges are separated due to historical reasons.
* ```workstations``` - everything related to the workstations. 
* ```osquery-sender``` - the endpoint to send logs to. It converts osquery json to splunk-acceptable json. Deployed in the qloud.  
* ```osquery-consistency/osquery-coverage``` - an instrument for the logs integrity monitoring.

## Usefull links

what is osquery: https://github.com/osquery/osquery
### Installing

Just add the repository to the ```/etc/apt/sources.list``` and install the package. 
