[request./api/search]
type = sequential
locality-shuffle = true
failover-delay = 100 

[request.translit./api/search]
type = sequential
locality-shuffle = true
failover-delay = 100

[request.translit./api/suggest]
type = parallel

proxy.searchRequest(
 session,
 request,
 callback)
  
proxy.searchRequest(
 session,
 "translit",
 request,
 callback)