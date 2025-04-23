# spring-body-logging

Библиотека, позволяющая гибко управлять логированием тел http запросов/ответов.

```
    @PostMapping(value = "/offers/categorize")
    @LogBody
    public List<OfferBucket> categorizeOffers(
            @RequestHeader(value = X_EXPERIMENTS, required = false) String experiments,
            @ApiParam(
                    "Тип площадки, с которой происходит категоризация"
            )
            @RequestParam(value = RGB, required = false) Color rgb,
            @RequestBody OfferBucketRequest request
    ) {
```

Аннотация @LogBody нам http методом определяет необходимость логирования тела для
конкретной ручки и параметризуется двумя свойствами: request и response, отвечающими за
необходимость логирования тела запроса и ответа (по-умолчанию оба выставлены в true)
