== Description
Coredns represents internal statistics and metrics in prometheus format. 
This plugin get metrics, translate to yasm format and than push it.

Gets metrics every **defaultInterval** (const defined in yasm.go) seconds, generate new metric names (possible any replaces) and translate it to yasm format.
and push them to HTTP API. More information about push format here https://wiki.yandex-team.ru/golovan/userdocs/push-api/?from=%2Fgolovan%2Fpush-api%2F

== Syntax
yasm {
	url ADDRESS

	itype ITYPE
	ctype CTYPE
	prj PRJ
	geo GEO

	prfx PRFX
	
	label_replace FROM TO
	name_replace FROM TO
	
	allow NAME [LABEL]
}

All options are optional
* **ADDRESS** represents pair of ip:port (default is 127.0.0.1:11005)
* **ITYPE, CTYPE, PRJ, GEO** it's like prometheus "Labels":)). See more https://wiki.yandex-team.ru/golovan/. The default are "none".
* **PRFX** adding prefix string for all metrics before push to yasm. Default is ""
* **label_replace** for flexible control name of metrics. Replace all labels which satisfing regexp **FROM** and change them **TO**
* **name_replace** is working as **label_replace** but replace name when name was generated.
	YASM metrics name generates from original prometheus name and concatenate all metric labels.
* **allow** no need to send all metrics wich coredns are collecting. We can skip all metrics which coredns exported by **NAME**
	and optional set the **LABEL** if we want to skip only metrics with **LABEL**


== Examples

yasm {
	itype runtimecloud
	prfx dnsmanager-

	allow coredns_forward_requests_total
	allow coredns_dns_request_duration_seconds AAAA

	label_replace dns://[fd53::1]:53 fd53
	label_replace [2a02:6b8::1:1]:53 ns-cache

	name_replace coredns_ ""
}

For example Coredns give us next metrics in plain text format (curl -s localhost:153/metrics):
```
...
process_cpu_seconds_total 2.24
coredns_dns_request_duration_seconds_bucket{server="dns://[fd53::1]:53",type="SRV",zone=".",le="0.00025"} 0
coredns_forward_requests_total{to="[2a02:6b8::1:1]:53"} 111
coredns_dns_request_duration_seconds_bucket{server="dns://[fd53::1]:53",type="AAAA",zone="search.yandex.net.",le="0.00025"} 0
...
```
where server="", type="", zone="", to="" are prometheus labels.

Before plugin sends metrics to the YASM API, takes steps:
	0) Filter only allowed labels, next metrics will be skiped:
```
process_cpu_seconds_total 2.24
coredns_dns_request_duration_seconds_bucket{server="dns://[fd53::1]:53",type="SRV",zone=".",le="0.00025"} 0
```
	1) replace all labels by next rules:
	replace dns://[fd53::1]:53 -> fd53
	replace [2a02:6b8::1:1]:53 -> ns-cache
	2) concatenate labels and metric name
```
coredns_forward_requests_total{to="[2a02:6b8::1:1]:53"} -> coredns_forward_requests_total_ns-cache
coredns_dns_request_duration_seconds_bucket{server="dns://[fd53::1]:53",type="AAAA",zone="search.yandex.net.",le="0.00025"} -> coredns_dns_request_duration_seconds_bucket_fd53_AAAA_search.yandex.net.
```
	3) name replacing (skip prefix coredns_)
```
coredns_forward_requests_total_ns-cache -> forward_requests_total_ns-cache
coredns_dns_request_duration_seconds_bucket_fd53_AAAA_search.yandex.net. -> dns_request_duration_seconds_bucket_fd53_AAAA_search.yandex.net.
...
```
	4) internal replacing for yasm compability (see https://wiki.yandex-team.ru/golovan/userdocs/tagsandsignalnaming/?from=%2Fgolovan%2Ftagsandsignalnaming%2F)
"." -> ""  etc ..
	5) calculate values and push
