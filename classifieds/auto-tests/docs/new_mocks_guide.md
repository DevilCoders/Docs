# Готовим моки правильно
Для начала определяемся со структурой мока, на основе категорий моков ниже.

## Простой мок - без query/body в предикате, со стандартным ответом
 ```
{
  "predicates": [
    {
      "deepEquals": {
        "path": "/1.0/user/offers/moto/1076842087-f1e84",
        "method": "DELETE"
      }
    }
  ],
  "responses": [
    {
      "is": {
        "headers": {
          "Content-Type": "application/json"
        },
        "body": {
          "status": "SUCCESS"
        },
        "statusCode": 200
      }
    }
  ]
}
```
Этот мок достаточно простой и его нужно наполнять с нуля, а не из файла с JSON'ом.
Для начала мы создаем объект класса MockStub, который затем будем наполнять. Это делается коммандой:
 ```
 stub()
 ```


Предикат заполняется этими методами:
```
withPredicateType(PredicateType.DEEP_EQUALS)
withPath("/1.0/user/offers/moto/1076842087-f1e84")
withMethod(Method.DELETE)
```
Но, для удобства, в [MockStub](https://github.com/YandexClassifieds/auto-tests/blob/test_fixes/desktop-web-client/src/main/java/ru/auto/tests/desktop/mock/MockStub.java),
есть метод withDeleteDeepEquals(String path). И достаточно вызвать его с нужным путём:
```
withDeleteDeepEquals("/1.0/user/offers/moto/1076842087-f1e84")
```
Это будет аналогично записи с withPredicateType, withMethod, withPath выше.

Используемые пути нужно положить константами в [Paths](https://github.com/YandexClassifieds/auto-tests/blob/test_fixes/desktop-web-client/src/main/java/ru/auto/tests/desktop/mock/Paths.java). 
Сюда добавляем пути без айдишников. В данном случае правильно добавить такую константу, если её еще там нет:
```
public static final String USER_OFFERS_MOTO = "/1.0/user/offers/moto";
```
А в тесте добавить ID оффера при прокидывании пути:
```
withDeleteDeepEquals(format("%s/1076842087-f1e84", USER_OFFERS_MOTO))
```

Ответ мока тоже простой и часто встречающийся, для него в [MockStub](https://github.com/YandexClassifieds/auto-tests/blob/test_fixes/desktop-web-client/src/main/java/ru/auto/tests/desktop/mock/MockStub.java)
существует готовый метод withStatusSuccessResponse(), который добавляет хэдер "Content-Type": "application/json", 
заполняет statusCode = 200 и добавляет body = {"status": "SUCCESS"}.

### Готовый объект мока
Т.е. чтобы полностью собрать такой мок с нуля, требуется выполнить:
 ```
stub().withDeleteDeepEquals(format("%s/1076842087-f1e84", USER_OFFERS_MOTO))
    .withStatusSuccessResponse();
```
Если в тесте ID «1076842087-f1e84» используется несколько раз, его стоит вынести в константы теста.
## Предикат с query, со стандартным ответом
Этот случай отличается от предыдущего только наличием query в предикате и другим методом:
```
{
  "predicates": [
    {
      "deepEquals": {
        "path": "/1.0/user/transaction/user:5547637-37d4c5a1bb02051ad394cfc6ab5cec78-1562075233402/prolongable",
        "method": "PUT",
        "query": {
          "domain": "autoru"
        }
      }
    }
  ],
  "responses": [
    {
      "is": {
        "headers": {
          "Content-Type": "application/json"
        },
        "body": {
          "status": "SUCCESS"
        },
        "statusCode": 200
      }
    }
  ]
}
```
### Для добавления query параметров, нам требуется:

- открыть бин [Query](https://github.com/YandexClassifieds/auto-tests/blob/test_fixes/desktop-web-client/src/main/java/ru/auto/tests/desktop/mock/beans/Query.java);
- добавить в него все наши используемые query параметры, если их там ещё нет. В данном случае `String domain;` там уже есть;
- при наполнении стаба, использовать метод `withRequestQuery(Query query)`;
- в него передать наши query параметры вот так:
  ```
  withRequestQuery(query().setDomain("autoru"))
  ```
  Метод setDomain() сгенерировался сам, на основе названия переменной в Query из-за использования аннотации @Setter над классом Query.
Его не нужно писать самому, достаточно просто добавить переменную в Query с названием query параметра.

### Готовый объект мока
Чтобы полностью собрать такой мок с нуля, требуется выполнить такой код:
 ```
stub().withPutDeepEquals("/1.0/user/transaction/user:5547637-37d4c5a1bb02051ad394cfc6ab5cec78-1562075233402/prolongable")
    .withRequestQuery(query().setDomain("autoru"))
    .withStatusSuccessResponse();
```



### Если поле в JSON'e не подходит для названия переменной
Если мы добавляем переменную, которая в JSON'e называется не по нашему код-стайлу, нужно пользоваться аннотацией `@SerializedName(String name)`.

Подробнее:
- `"page_size"`  - нижнее подчеркивание мы используем в константах(например PAGE_SIZE), и так переменную нельзя
  называть. Правильно назвать её pageSize, но добавить аннотацию с названием "page_size", в которую эта переменная превратится при создании JSON'a.
  Делается это так:
  ```
  @SerializedName("page_size")
  String pageSize;
  ```
- `"1920px"` - переменная не может называться с цифры, но в JSON'e поле может начинаться с цифры. В таком случае
  правильно назвать переменную px1920, но добавить аннотацию с названием "1920px", в которую эта переменная сериализуется в JSON'e.
  Например:
  ```
  @SerializedName("1920px")
  String px1920;
  ```
- аннотацию @SerializedName() добавляем только тогда, когда поле в JSON'e называется так, как мы не можем назвать переменную.
  Во всех остальных случаях имя полу в JSON'e = имени переменной в Query.

## Не стандартный ответ / огромный JSON  в ответе
Очень часто в тестах нам нужно получить один и тот-же объект мока, но с чуть разными значениями каких-либо полей.
Например, нам нужно замокать оффер, но для разных кейсов он должен быть в разных состояниях:
- разный id;
- is_favorite = true/false;
- status = ACTIVE/INACTIVE/...;
- разный price;
- и т.д.

Раньше, для каждого из этих состояний мы заводили отдельный JSON с соответствующим ответом и предикатом.

Сейчас, перед написанием тестов, всегда нужно подумать - можем ли мы как-то оптимизировать это?

Проще всего написать stub("desktop/UserOffersCarsUsedInactive") и создать мок на основе готового файлика. 
Но, если в задаче мы, например, создаем несколько моков для карточки тачки/мото/грузовика и в каждом из них меняем одно 
поле или один объект - это неоптимальное решение.

Приведу недавний пример. Задача - в листинге ЛК офферов покупать VAS на авто/мото/грузовике.

### Подробно разбираем пример ниже, открой [**ссылку!**](https://github.com/YandexClassifieds/auto-tests/pull/1421/commits/c39f8d43b56444d2ad2d9f624cbf5d22dc2219a8)

Пример по переводу этой задачи со старой схемы моков на новую. На этом тестовом классе сэкономили 9 JSON'ов.


В задаче было 3 JSON мока, которые возвращали ЛК листинг с одним car/moto/truck оффером, которому добавлялся VAS протухающий завтра.

Если присмотреться, то суть задачи - добавить офферу car/moto/truck вот такой объект в service, который означает что VAS
протухнет завтра. Раньше заменялся параметр «ALL_SALE_TOPLIST_EXPIRE_DATE» на завтрашнюю дату:
```
"services": [
    {
      "is_active": true,
      "create_date": "1559816905000",
      "service": "all_sale_toplist",
      "prolongable": false,
      "expire_date": "%ALL_SALE_TOPLIST_EXPIRE_DATE%"
    }
  ]
```
Т.е. нам не важно какое авто/мото/грузовик добавлены, главное чтобы они были соответствующей категории и имели этот 
объект в services в JSON'e.

### Что нужно?
Для решения этой задачи, создадим 2 класса описывающих моки:

- [MockUserOffers](https://github.com/YandexClassifieds/auto-tests/blob/test_fixes/desktop-web-client/src/main/java/ru/auto/tests/desktop/mock/MockUserOffers.java), 
этот класс отвечает за создания мока для ответа ручки "/1.0/user/offers/cars", которая возвращает листинг офферов ЛК. Пример её ответа, без офферов:
  ```
  {
    "pagination": {
      "page_size": 10,
      "page": 1,
      "total_offers_count": 1,
      "total_page_count": 1
    },
    "offers": [],
    "status": "SUCCESS"
  }
  ``` 
- [MockUserOffer](https://github.com/YandexClassifieds/auto-tests/blob/test_fixes/desktop-web-client/src/main/java/ru/auto/tests/desktop/mock/MockUserOffer.java),
этот класс отвечает за создания мока оффера, который мы положим в список "offers" объекта MockUserOffers выше.

Мы разделили наш JSON мока на два - мок листинга и мок конкретного оффера для того чтобы:

- создав MockUserOffers, мы можем свободно изменять поля пагинации, общего кол-во офферов, удобно добавлять какие угодно офферы, изменять status ответа;
- создав MockUserOffer, мы можем свободно конфигурировать конкретные офферы, менять им поля, создать примеры офферов для
авто/мото/грузовиков и использовать их потом.

**Общее правило** - если мы делаем объект мока для листинга каких-либо объектов, нужно делать 2 мок класса, первый для
описания ответа ручки, второй для описания объектов, которые мы можем положить в массив внутри ответа ручки.

### Создаем мок для объекта внутри массива ответа другой ручки / мок для ответа ручки без листинга

В данном примере создадим мок для объекта оффера, который возвращается в списке ЛК офферов от ручки "/1.0/user/offers/cars".

- создаем класс [MockUserOffer](https://github.com/YandexClassifieds/auto-tests/blob/test_fixes/desktop-web-client/src/main/java/ru/auto/tests/desktop/mock/MockUserOffer.java),
он должен называться соответственно названию ручки, где он используется;

- в нём создаем переменную, в которой будет храниться наш объект мока, заметьте это JsonObject;

  ```
  @Getter
  @Setter
  @Accessors(chain = true)
  JsonObject body;
  ```

- создаем конструктор класса, его задача по переданному пути взять json файл с моком, распарсить его в JsonObject и 
положить в переменную body:
  ```
  private MockUserOffer(String pathToTemplate) {
          this.body = new GsonBuilder().create().fromJson(getResourceAsString(pathToTemplate), JsonObject.class);
      }
  ```
- создаем метод, для получения нового объекта MockUserOffer, чтобы вызывать его внутри параметризованных тестов, 
передав путь аргументом:
  ```
  public static MockUserOffer mockUserOffer(String pathToTemplate) {
          return new MockUserOffer(pathToTemplate);
      }
  ```
- добавляем константы с путем до машины, мото, грузовика. В JSON'ах по этому пути лежат актуальные примеры активных 
офферов сответствующих категорий и их можно использовать в дальнейших тестах, поэтому добавляем в название констант - 
«EXAMPLE»:
  ```
  public static final String USER_OFFER_CAR_EXAMPLE = "mocksConfigurable/user/UserOfferCar.json";
  public static final String USER_OFFER_MOTO_EXAMPLE = "mocksConfigurable/user/UserOfferMoto.json";
  public static final String USER_OFFER_TRUCK_EXAMPLE = "mocksConfigurable/user/UserOfferTruck.json";
  ```
- для удобства, можем добавить методы, чтобы сразу же вызывать нужный мок оффера, не используя mockUserOffer(String pathToTemplate):
  ```
  public static MockUserOffer car() {
      return mockUserOffer(USER_OFFER_CAR_EXAMPLE);
  }
  
  public static MockUserOffer moto() {
      return mockUserOffer(USER_OFFER_MOTO_EXAMPLE);
  }
  
  public static MockUserOffer truck() {
      return mockUserOffer(USER_OFFER_TRUCK_EXAMPLE);
  }
  ```
- затем добавляем методы, с помощью которых мы можем редактировать наш объект. В нашем примере требовалось офферу 
добавить массив services с объектом VAS протухающим завтра, он должен выглядеть вот так:
  ```
  "services": [
      {
        "is_active": true,
        "create_date": "1559816905000",
        "service": "all_sale_toplist",
        "prolongable": false,
        "expire_date": "%ALL_SALE_TOPLIST_EXPIRE_DATE%"
      }
    ]
  ```
  Для этого пишем такой метод:

  ```
  public MockUserOffer setAllSaleToplistServiceExpiredTomorrow() {
          long tomorrow = Timestamp.valueOf(LocalDate.parse(LocalDate.now().toString()).plusDays(1).atStartOfDay())
                  .getTime();
  
          JsonObject service = new JsonObject();
          service.addProperty("service", "all_sale_toplist");
          service.addProperty("is_active", true);
          service.addProperty("create_date", "1559816905000");
          service.addProperty("prolongable", false);
          service.addProperty("expire_date", Long.toString(tomorrow));
  
          JsonArray services = new JsonArray();
          services.add(service);
  
          body.add("services", services);
          return this;
      }
  ```
  В нём:

  - long tomorrow - возрващает timestamp завтрашнего дня, было и раньше, можно не обращать внимание;
  - `JsonObject service = new JsonObject();` - создаем JsonObject для нашего объекта сервиса;
  - с помощью методов `addProperty("fieldName", "field_value")` - наполянем этот объект данными, перед значение tomorrow 
  в поле expire_date;
  - `JsonArray services = new JsonArray();` - создаем пустой JsonArray;
  - `services.add(service);` - добавляем наш созданный сервис в JsonArray services;
  - `body.add("services", services);` - в body лежит наш оффер, который мы положили туда по переданному пути. Методом 
  «add» мы добавляем объект services в наш JsonObject и называем его "services". Если раньше в поле "services" был 
  другой объект, он перезапишется на переданный. Это важно применять, так как мы заранее не знаем, есть ли в body объект
  services и если есть - это array c элементами или без. Всегда лучше создать его с нуля и записать в body.
  
- если нам нужно изменить поле в глубине JsonObject'a, например поле «is_favorite» вот тут:
  ```
  {
    "raw_report": {
      "report_offer_info": {
          "offer_id": "1076842087-f1e84",
          "is_favorite": false
      }
    }
  }
  ```
  Потребуется углубляться в объект и уже внутри добавлять нужное значение параметра "is_favorite":
  ```
  body.getAsJsonObject("raw_report").getAsJsonObject("report_offer_info").addProperty("is_favorite", isFavorite)
  ```

### Создаем мок для ответа ручки с листингом других объектов

В данном примере создадим мок для ответа, который возвращается от ручки "/1.0/user/offers/cars", по которому мы 
получаем листинг офферов ЛК.

- создаем класс [MockUserOffers](https://github.com/YandexClassifieds/auto-tests/blob/test_fixes/desktop-web-client/src/main/java/ru/auto/tests/desktop/mock/MockUserOffers.java),
  он должен называться соответственно названию ручки, где он используется;
- в нём создаем переменную, в которой будет храниться наш объект мока;

  ```
  @Getter
  @Setter
  @Accessors(chain = true)
  JsonObject body;
  ```
- создаем еще одну переменную, в ней будут храниться офферы класса MockUserOffer, которые мы описывали выше:

  ```
  @Getter
  private List<MockUserOffer> offers;
  ```
- создаем конструктор класса, его задача по переданному пути взять json файл с моком, распарсить его в JsonObject и
  положить в переменную body:
  ```
  private MockUserOffers(String pathToTemplate) {
        this.body = new GsonBuilder().create().fromJson(getResourceAsString(pathToTemplate), JsonObject.class);
    }
  ```
- добавляем константу с путём до шаблона ответа листинга:
  ```
  private static final String USER_OFFERS_TEMPLATE = "mocksConfigurable/user/UserOffersTemplate.json";
  ```
  Обратите внимание, она ссылается на такой JSON:
  ```
  {
    "pagination": {
      "page_size": 10,
      "page": 1,
      "total_offers_count": 0,
      "total_page_count": 1
    },
    "offers": [],
    "status": "SUCCESS"
  }
  ```
  Этот JSON без офферов, просто минимальный набор данных, поэтому мы добавляем к названию константы TEMPLATE. Если бы в
нём были офферы - это был бы EXAMPLE.
- создаем метод, для получения нового объекта MockUserOffers, на основе шаблона выше:
  ```
  public static MockUserOffers userOffersResponse() {
        return new MockUserOffers(USER_OFFERS_TEMPLATE);
    }
  ```
- добавляем метод `setOffers(MockUserOffer... userOffers)`:
  ```
  public MockUserOffers setOffers(MockUserOffer... userOffers) {
          offers = new ArrayList<>();
          offers.addAll(Arrays.asList(userOffers));
          return this;
      }
  ```
  Он принимает на вход любое кол-во объектов офферов класса MockUserOffer. Создает в переменной offers пустой ArrayList
и добавляет в него все переданные в setOffers офферы.
- добавляем метод `build()`:
  ```
  public JsonObject build() {
          offers.forEach(report -> body.getAsJsonArray("offers").add(report.getBody()));
          body.getAsJsonObject("pagination").addProperty("total_offers_count", offers.size());
          return body;
      }
  ```
  Он обходит все офферы, которые мы засетали в переменную offers, и добавляет их в основное тело ответа body, в список 
offers. Затем устанавливает соответствующее число "total_offers_count" в объекте "pagination".

### Готовый объект мока
[Пример теста](https://github.com/YandexClassifieds/auto-tests/blob/c39f8d43b56444d2ad2d9f624cbf5d22dc2219a8/desktop-lk-web-tests/src/test/java/ru/auto/tests/desktop/lk/sales/VasAutoprolongActiveOptionTest.java)
с моками описанными выше.

В итоге, описав мок для листинга лк оффера и для самого оффера - мы можем собрать это в один объект.
У нас уже всё готово для этого, делается это так:
```
stub().withGetDeepEquals("/1.0/user/offers/cars")
      .withResponseBody(
          userOffersResponse().setOffers(
              mockUserOffer(USER_OFFER_CAR_EXAMPLE).setAllSaleToplistServiceExpiredTomorrow())
          .build())
```
Здесь:
- `withGetDeepEquals("/1.0/user/offers/cars")` - сетаем тип предиката DEEP_EQUALS, метод GET, путь = "/1.0/user/offers/cars";
- `withResponseBody(JsonObject responseBody)` - добавляем тело ответа;
- `userOffersResponse()` - метод из MockUserOffers, создает ответ листинга на основе шаблона;
- `setOffers(MockUserOffer... userOffers)` - метод из MockUserOffers, наполняет переменную offers переданными офферами;
- `mockUserOffer(USER_OFFER_CAR_EXAMPLE)` - создает объект оффера на основе переданного пути из константы;
- `setAllSaleToplistServiceExpiredTomorrow()` - метод из MockUserOffer, добавляет service с проотухающим VAS'ом в объект оффера;
- `build()` - метод из MockUserOffers, на основе офферов в переменной offers собирает JsonObject с листингом офферов.
