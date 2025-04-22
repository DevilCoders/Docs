### TODO List
1) Handle Races when Host/Proxy adds same Endpoint. Currently we assume that it can't happen
2) Fix threading model in EndpointStorageProxy. EndpointStorageHost is intentionally single threadded. But EndpointStorageProxy does have internal mutexes. But retrieving of Endpoint and the calling it's method is unsafe.
3) Add/Remove of Any Endpoint should work from any Proxy/Host (it will help fix first issue).


### Implementation notes
There is an EndpointHost and EndpointProxy. Both of them are implemented via YandexIO::Endpoint.

addCapability/removeCapability are always executed localy first (even if it's a EndpointProxy). After that EndpointHost broadcast event to proxies. EndpointProxy sendMessage to EndpointHost.
