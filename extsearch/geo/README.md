## API instances
Environment     | URL
----------------|----------------------------------------------------------------
testing         | http://addrs-testing.search.yandex.net/search/stable/yandsearch
production      | http://addrs.yandex.ru:17140/yandsearch
batch geocoding | http://addrs-batch.search.yandex.net/yandsearch

## Auth
We use [TVM2 authentication](https://wiki.yandex-team.ru/passport/tvm2). Tickets are passed in `X-Ya-Service-Ticket` HTTP header.

For production API, the ticket is required.

For testing API, the ticket is optional. If you provide the header and it is invalid, an error is returned. You may force ticket checking with `tvm=1` parameter: if set, requests with no ticket are also rejected.

Environment  | TVM Application ID
-------------|-------------------
testing      | 2008261
production   | 2001886


## Parameters
Name  | Description
------|-------------------------
**general** |
[lang](https://wiki.yandex-team.ru/maps/dev/params/lang/) | response language **(required)**
`ms=pb` | turn protobuf on **(required)**
`hr` | show human readable protobuf (supported value `yes`)
`origin` | human readeable client and process description **(required)**
**search** |
[text](https://wiki.yandex-team.ru/maps/dev/params/text/) | search request
[ll](https://wiki.yandex-team.ru/maps/dev/params/ll/) + [spn](https://wiki.yandex-team.ru/maps/dev/params/spn/) or [bbox](https://wiki.yandex-team.ru/maps/dev/params/bbox/) or [wll](https://wiki.yandex-team.ru/maps/dev/params/wll/) | search area
[type](https://wiki.yandex-team.ru/maps/dev/params/type/) | search results type
[results](https://wiki.yandex-team.ru/maps/dev/params/results/) | maximum number of results
[skip](https://wiki.yandex-team.ru/maps/dev/params/skip/) | number of objects to skip in the response
[ctx](https://wiki.yandex-team.ru/maps/dev/params/ctx/) | search context
[snippets](https://wiki.yandex-team.ru/maps/dev/params/snippets/) | search snipperts
[ull](https://wiki.yandex-team.ru/maps/dev/params/ull/) | user location
[sort](https://wiki.yandex-team.ru/maps/dev/params/sort/) | search results sort
[sort_origin](https://wiki.yandex-team.ru/maps/dev/params/sort_origin/) | center of sort by distance
[mode](https://wiki.yandex-team.ru/maps/dev/params/mode/) | search mode
[rll](https://wiki.yandex-team.ru/maps/dev/params/rll/) | search along geometry
[uri](https://wiki.yandex-team.ru/maps/dev/params/uri/) | search by object id
[z](https://wiki.yandex-team.ru/maps/dev/params/z/) | search area zoom
`geometry` | add toponym geometry to response
**params of base search engines** |
[business_filter](https://wiki.yandex-team.ru/maps/dev/params/filter/) | filter businesses by features
[business_show_closed](https://wiki.yandex-team.ru/maps/dev/params/showclosed/) | add closed businesses to response
[business_oid](https://wiki.yandex-team.ru/maps/dev/params/oid/) | get businesses by id
[geocoder_pin](https://wiki.yandex-team.ru/maps/api/http/internal/search/guide/#rezhimgeokodirovanijachtozdes) | reverse geocoding according to map zoom
**experimental functionality** |
`is_chz_request` | add personal discovery (chz) response

## Response
Geosearch API returns `Response` containing search results.
When no results is found, a `Response` message with the empty `reply` field is returned.

* [common/response.proto](/arc/trunk/arcadia/maps/doc/proto/yandex/maps/proto/common2/response.proto)
* [search/search.proto](/arc/trunk/arcadia/maps/doc/proto/yandex/maps/proto/search/search.proto)

All proto files are available at https://a.yandex-team.ru/arc/trunk/arcadia/maps/doc/proto/yandex/maps/proto/search

## Batch geocoding
If you want to process a lot of geocoding or reverse gecoding requests you can use batch cluster. 
It can't guarantee stable timings and do not provide misspell correction (wrong spelling, different address forms will be ok)
but you can send huge rps to it (aprox 5000 for text requests and 15000 for reverse geocoding (coordinates) requests)

## Advanced information

https://a.yandex-team.ru/arc/trunk/arcadia/extsearch/geo/GUIDE.md

## Support
If you have any question, feel free to ask:

* Support chat https://t.me/joinchat/B2BIbEDkZbsZlHrK5IB8Hw
* In case of death of telegram https://staff.yandex-team.ru/evelkin
