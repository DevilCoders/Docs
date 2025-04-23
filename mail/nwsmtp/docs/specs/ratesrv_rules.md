# RateSrv rules format

**N.B.**: In fields where you can use email or uid you should always choose uid if it is present (it has priority over email in RateSrv checks). Use magic.yandex-team.ru to check address for having a uid.

## `connections_from_ip`
* Columns: sender ip-address

## `msgs_from_sndr`
* Columns: sender email or uid | sender domain

## `msgs_for_rcpt`
* Columns: recipient email or uid | recipient domain

## `msgs_for_rcpt_from_ip`
* Columns: recipient email or uid | recipient domain | sender ip-address

## `msgs_for_rcpt_from_sndr`
* Columns: sender email or uid | sender domain | recipient email or uid | recipient domain

## `bytes_for_rcpt`
* Columns: recipient email or uid | recipient domain

## `bytes_from_sndr`
* Columns: sender email or uid | sender domain

## `bytes_for_rcpt_from_ip`
* Columns: recipient email or uid | recipient domain | sender ip-address
