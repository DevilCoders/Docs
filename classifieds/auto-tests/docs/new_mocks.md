### [MockRuleConfigurable](https://github.com/YandexClassifieds/auto-tests/blob/master/desktop-web-client/src/main/java/ru/auto/tests/desktop/rule/MockRuleConfigurable.java)
Новая рула, аналогична старой MockRule, но чутка порефачена, чтобы быть покрасивше
Основные применения функционально те же:

- mockRule.setStubs(MockStub... stubs).create() - публикует мок на основе переданных стабов;
- mockRule.setStubs(MockStub... stubs).update() - добавляет к уже существующим стабам переданные, обновляет мок;
- mockRule.overwriteStub(0, stub()) - перезаписывает стаб по индексу.
- mockRule.delete() - удаляет мок, очищает сохраненные стабы;

### [MockStub](https://github.com/YandexClassifieds/auto-tests/blob/master/desktop-web-client/src/main/java/ru/auto/tests/desktop/mock/MockStub.java)
Объект стаба. Добавляет возможностью создавать с нуля свой или редактировать имеющийся стаб.

- MockStub.stub() - создает объект стаба, его следует наполнить нужными полями с помощью методов with. **Обязательно** указывать withPredicateType(PredicateType predicateType),  с соответствующим типом предиката(DEEP_EQUALS, EQUALS, MATCHES и т.д.). В настоящий момент типы предикатов OR, NOT, AND, INJECT не поддерживаются. Пример создания своего объекта стаба:
   ```
  stub().withPredicateType(DEEP_EQUALS)
            .withPath(CARFAX_BOUGHT_REPORTS_RAW)
            .withMethod(GET)
            .withRequestQuery(query().setPageSize("10"))
            .withResponseBody(carfaxReportsResponse().setReports(
                          boughtReportRawExample().setIsFavorite(true)).build());

- MockStub.stub(String pathToMockFile) - создает объект стаба на основе переданного json файла. Т.е. можно добавлять моки как и раньше, с немного другим синтаксисом:

  ```
  Сейчас:
  mockRule.setStubs(stub("desktop/SessionAuthUser"), stub("desktop/BillingAutoruPayment")).create();
  
  Раньше: 
  mockRule.newMock().with("desktop/SessionAuthUser", "desktop/BillingAutoruPayment").post()

-  объект MockStub собранный на основе переданного json файла можно редактировать. В данный момент нельзя отредактировать тип предиката. Все остальные поля редактируются. Для применения редактирования **обязательно** указывать withPredicateType(PredicateType predicateType), с соответствующим типом предиката из JSON'a который мы передаем на вход stub(). Пример редактирования:
    ```
    stub("poffer/UserDraftCarsDraftIdC2bApplicationInfo").withPredicateType(MATCHES)
              .withResponseBody(c2bApplicationInfoExample().setCanApply(false).getBody()));

    stub("poffer/UserDraftCarsDraftIdC2bApplicationInfo").withPredicateType(MATCHES)
              .withMethod(POST).withResponseBody("poffer/UserDraftCarsDraftIdC2bApplicationInfo");

- В первом случае выше мы собрали тело ответа сами, на основе класса MockC2BApplicationInfo.java, в котором указан пример JSON'a для использования и реализован метод setCanApply(boolean canApply), для добавления соответствующего поля. Во втором случае мы изменили метод на POST + изменили тело на json из файла;
- используемые в моках пути к ручкам следует добавлять в desktop.mock.Paths;
- используемые query параметры следует добавлять в mock.beans.Query;
- в классе [PredicateTypeDependentMethods](https://github.com/YandexClassifieds/auto-tests/blob/master/desktop-web-client/src/main/java/ru/auto/tests/desktop/mock/PredicateTypeDependentMethods.java) хранятся методы по созданию предиката соответствующего типа или по получении параметров предиката соответствующего типа. Это требуется из-за неудобной структуры предиката. Нужно заранее знать какого типа будет предикат. Пример предиката:
```
  "predicates": [
    {
      "matches": {
        "path": "/1.0/user/draft/cars/",
        "method": "GET"
      }
    }
  ]
```

###  Объекты ответа

withRequestBody() и withResponseBody() принимают на вход либо путь до Json'a, либо JsonObject. Несколько примеров создания нужного объекта ответа:
- в [MockStub()](https://github.com/YandexClassifieds/auto-tests/blob/master/desktop-web-client/src/main/java/ru/auto/tests/desktop/mock/MockStub.java) метод withStatusSuccessResponse(). Внутри него создается простой JsonObject успешного ответа и сразу сеттится. Такой ответ универсален для многих ручек, поэтому вынесен в MockStub;
- [MockC2BApplicationInfo.java](https://github.com/YandexClassifieds/auto-tests/blob/master/desktop-web-client/src/main/java/ru/auto/tests/desktop/mock/MockC2BApplicationInfo.java) создает объект мока на основе Json'a из константы, реализован метод setCanApply();
- [MockCarfaxReportsList.java](https://github.com/YandexClassifieds/auto-tests/blob/master/desktop-web-client/src/main/java/ru/auto/tests/desktop/mock/MockCarfaxReportsList.java) создает объект мока ответа ручки со списком отчетов на основе шаблона ответа ручки Json'a из константы. Отдельно наполняется отчетами класса [MockCarfaxReport.java](https://github.com/YandexClassifieds/auto-tests/blob/master/desktop-web-client/src/main/java/ru/auto/tests/desktop/mock/MockCarfaxReport.java). Ещё один пример создания мока для листинга офферов [MockUserOffers.java](https://github.com/YandexClassifieds/auto-tests/blob/c39f8d43b56444d2ad2d9f624cbf5d22dc2219a8/desktop-web-client/src/main/java/ru/auto/tests/desktop/mock/MockUserOffers.java), который наполняется объектами офферов [MockUserOffer.java)](https://github.com/YandexClassifieds/auto-tests/blob/c39f8d43b56444d2ad2d9f624cbf5d22dc2219a8/desktop-web-client/src/main/java/ru/auto/tests/desktop/mock/MockUserOffer.java) . 

### Примеры тестов

- [первый](https://github.com/YandexClassifieds/auto-tests/pull/1416/files#diff-e3fc84096d94617e00a76a3661ad7d470e273d7286da0f71b14ce6ec564d57cc). Тут можно обратить внимание на вынесенный в самый низ теста собранный стаб, в котором мы сетаем одно поле isFavorite. Тоже самое можно было бы сделать со стабом к ручке FAVORITES_CARS_PATH, так как они отличаются только методами, первый POST, второй DELETE;
- [второй](https://github.com/YandexClassifieds/auto-tests/pull/1416/files#diff-333dc7018583c04a6ee07d4fd326a614e528ceeda29997551e94de099399a3bb). Тут пример того, как мы по всему тесту используем один и тот же стаб на основе Json файлика, но в одном из случаев меняем ему body.
- [третий](https://github.com/YandexClassifieds/auto-tests/blob/c39f8d43b56444d2ad2d9f624cbf5d22dc2219a8/desktop-lk-web-tests/src/test/java/ru/auto/tests/desktop/lk/sales/VasAutoprolongActiveOptionTest.java). 
