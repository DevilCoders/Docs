Работа с парсером для prime'а: 

Вся выдача репорта сначала десериализуется в объект PrimeSearchResult.
PrimeSearchResultParser инициализируется через Converter<PrimeSearchResult, YourClass>.

Соответственно, теперь получение целевого объекта выглядит примерно вот так: 
```
MarketSearchRequest request = new MarketSearchRequest(MarketReportPlace.PRIME);
        request.setQuery("iphone");
        request.setPp(18);
DefaultAsyncMarketReportService reportService = new DefaultAsyncMarketReportService();
PrimeSearchResultParser<List<TestOffer>> parser = new PrimeSearchResultParser<>(new OffersConverter());
List<PrimeReportParserTest.TestOffer> offers = reportService.async(request, parser).join();
```

Converter выглядит примерно так:

```
import org.springframework.core.convert.converter.Converter;
 
public class OffersConverter implements Converter<PrimeSearchResult, List<TestOffer>> {

        @Override
        public List<TestOffer> convert(PrimeSearchResult source) {
            return source.getSearch().orElse(new Search()).getResults().stream()
                    .filter(x -> x.getEntity().orElse("").equals("offer"))
                    .map(x -> {
                        TestOffer testOffer = new TestOffer();
                        testOffer.setModelId(x.getModel().orElse(new Model()).getId().orElse(-1L));
                        String wareId = x.getWareId()
                                .orElseThrow(() -> new IllegalStateException(
                                        "Got invalid offer from report, cannot work with it"));
                        testOffer.setWareId(wareId);
                        testOffer.setVendorName(x.getVendor().orElse(new Vendor()).getName().orElse(null));
                        return testOffer;
                    }).collect(Collectors.toList());
        }
    }

```

**Важный момент**
В описанной модели prime-выдачи все геттеры сделаны Optional'ами для удобства обработки Nullable полей.
Исключением являются геттеры списков, они всегда выдают пустой список в случае, если пришел null.


