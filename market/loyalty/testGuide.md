# Рекомендации по написанию тестов

## Название тестового класса должно включать в себя название тестируемого класса
<details><summary>...</summary>

### Мотивация
Можно быстро просмотреть все тесты, связанные с конкретным классом.
Для этого достаточно выделить название класса и нажать Ctrl+N 
### Пример
Класс: DiscountController  
Тестовые классы: 
- DiscountControllerTest
- DiscountControllerValidationTest
- ConcurrentDiscountControllerTest
</details>

## Название теста должно начинаться с should
<details><summary>...</summary>

### Мотивация
1. В структуре класса (окно в IDEA) все тесты будут показаны подряд - легко просмотреть весь набор тестов
2. Вынуждает четко описать, что конкретно тестируется
### Пример
shouldSendOnlyOneCouponOnRetry
shouldFailIfPromoNotActive
</details>

## Название теста должно быть связано либо с контрактом тестируемого объекта, либо с конкретным кейсом бизнес логики
<details><summary>...</summary>

### Мотивация
1. При просмотре списка тестов, можно понять гарантии, предоставляемые тестируемым объектом и степень покрытия тестами функционала.
2. При тестировании композиции достаточно убедиться в том, что делегат был вызван, так как его контракт подтвержден тестами.
Особенно это актуально при тестировании контроллеров - тестировать вставку всего набора объектов в БД, к примеру, будет слишком дорого   
### Пример
ForceCreateCouponEventTest:
- shouldSendCoupon
- shouldSendOnlyOneCouponOnRetry
- shouldProduceCouponToConsumer
- shouldSendCouponWithUidIfGiven
- shouldSaveTriggerEventResult
- shouldFailIfPromoNotActive
- shouldFailIfNoTriggerFound
</details>

## Given-When-Then стиль написания тестов
<details><summary>...</summary>

Given - исходное состояние (моки + объекты в базе). Либо в начале теста, либо в @Before  
When - действие: вызов метода, вызов контроллера  
Then - проверка исполнения контракта
### Мотивация
1. Тест легче читать
2. При падении теста область поиска сужается до пересечния Given & When
### Пример
```java
public class ForceCreateCouponEventTest {
    @Test
    public void shouldSaveTriggerEventResult() {
        //given
        Promo promo = createPromo();
        triggersFactory.createForceCreateCouponTrigger(promo);
        //when
        triggerService.processEvent(promo.getId(), createForceCreateCouponEvent(EMAIL, CLIENT_UNIQUE_KEY), TriggerEventType.FORCE_CREATE_COUPON);
        //then
        List<BaseTriggerEvent> events = triggerEventDao.getAll();
        assertThat(events, hasSize(1));

        ForceCreateCouponEvent event = (ForceCreateCouponEvent) events.get(0);
        assertEquals(EMAIL, event.getEmail());
        assertEquals(TriggerEventProcessedResult.SUCCESS, event.getProcessedResult());
    }
}
```
</details>

## Тестируйте поведение тестируемого объекта, а не реализацию: "черный ящик"
<details><summary>...</summary>

### Мотивация
1. Уменьшает шанс расхождения реализации и контракта
2. Облегчает рефакторинг реализации 
</details>

## Используйте константы или переменные
<details><summary>...</summary>

Константы предпочтительнее, но если данные касаются отдельного теста, то лучше использовать переменные
### Мотивация
1. Легче читать
2. Связвает given и then
3. Упрощает рефакторинг
### Пример
```java
public class ReservationServiceTest {
    @Test
    public void shouldConsiderReserveOnGetBalance() {
        BigDecimal spendQuantity = BigDecimal.valueOf(3);
        spendItem(spendQuantity, uid);

        reservationService.reserve(uid, FlashOfferUtils.DEFAULT_OFFER_WARE_ID, RESERVE_QUANTITY.intValue());

        assertThat(
            budgetService.getBalance(flashOffer.getBudgetAccountId()),
            comparesEqualTo(INITIAL_STOCK.subtract(spendQuantity).subtract(RESERVE_QUANTITY))
        );

        assertThat(
            budgetService.getItemStockWithReservations(flashOffer),
            comparesEqualTo(INITIAL_STOCK.subtract(spendQuantity))
        );
    }
}
```
</details>

## Используйте factory для создания данных для тестирования
<details><summary>...</summary>

### Мотивация
1. Проще рефакторить - при появлении новых параметров меньше мест для исправления
2. Легче читать
3. Зачастую в factory будут передаваться только те параметры, которые имеют значение для текущего теста
### Пример
Было
```java
public class TriggerOrderInStatusXTest {
    @Before
    public void init() {
        triggerService.addTrigger(Trigger.builder(TriggerEventType.ORDER_STATUS_UPDATED)
                    .setPromoId(promo.getId())
                    .setAction(triggerUtils.getActionFactory(TriggerActionType.SEND_COUPON_BY_IDENTITY_ACTION).create(null, "{\"emailTemplateId\":\"0\"}"))
                    .addRestriction(triggerUtils.getRestrictionFactory(TriggerRestrictionType.ORDER_STATUS_RESTRICTION).create(null, String.valueOf(OrderStatus.DELIVERED.getId())))
                    .addRestriction(triggerUtils.getRestrictionFactory(TriggerRestrictionType.ACTION_ONCE_RESTRICTION).create(null, null))
                    .build());
    }
}
```
Стало
```java
public class TriggerOrderInStatusXTest {
    @Before
    public void init() {
        triggersFactory.createOrderStatusUpdatedTrigger(promo, OrderStatus.DELIVERED, OrderStatus.PICKUP);
    }
}
```
</details>

## Тестируйте только одну вещь за раз
<details><summary>...</summary>

### Мотивация
1. Тесты короче - легче читать
2. При появлении ошибки только один тест упадет на assert (остальные должны упасть с exception) - именно этот тест будет показывать на баг
3. Уменьшается количество тестового кода, который необходимо поправить при изменении функционала. Иногда можно просто удалить уже неактуальный тест.
### Note
Если упал большой тест и не так просто понять почему, легче откатить свои изменения, разбить его на маленькие тесты, 
вернуть свои изменения обратно и исправить уже один небольшой тест.  
Когда разбивал тесты, замечал, что иногда итоговый код оказывается не намного длинее исходного, несмотря на дублирование given и when 
за счет уменьшения количества временных переменных
### Пример
Было
```java
public class ReservationServiceTest {
     @Test
     public void unreserve() {
         reservationService.reserve(uid, FlashOfferUtils.DEFAULT_OFFER_WARE_ID, RESERVE_QUANTITY.intValue());
         Long reservationAccountId = getReservation().getAccountId();
         assertThat(budgetService.getBalance(reservationAccountId), comparesEqualTo(RESERVE_QUANTITY));
         assertThat(budgetService.getBalance(offerBudgetAccountId), comparesEqualTo(INITIAL_STOCK.subtract(RESERVE_QUANTITY)));
 
         int historyCountBefore = flashHistoryDao.getAllRecords().size();
 
         clock.spendTime(HOLD_RESERVE_FOR_MINUTES + 1, ChronoUnit.MINUTES);
 
         reservationService.unreserveOld();
         assertThat(budgetService.getBalance(reservationAccountId), comparesEqualTo(BigDecimal.ZERO));
         assertThat(budgetService.getBalance(offerBudgetAccountId), comparesEqualTo(INITIAL_STOCK));
 
         assertThat(getReservation().getBeginTime(), nullValue());
         assertThat(flashHistoryDao.getAllRecords(), hasSize(historyCountBefore + 1));
     }
}
```
Стало
```java
public class ReservationServiceTest {
    @Test
    public void shouldClearBeginTimeFieldOnUnreserve() {
        reservationService.reserve(uid, FlashOfferUtils.DEFAULT_OFFER_WARE_ID, RESERVE_QUANTITY.intValue());

        clock.spendTime(HOLD_RESERVE_FOR_MINUTES + 1, ChronoUnit.MINUTES);
        reservationService.unreserveOld();

        assertThat(getReservation().getBeginTime(), nullValue());
    }

    @Test
    public void shouldSaveHistoryOnUnreserve() {
        reservationService.reserve(uid, FlashOfferUtils.DEFAULT_OFFER_WARE_ID, RESERVE_QUANTITY.intValue());
        int historyCountBefore = flashHistoryDao.getAllRecords().size();

        clock.spendTime(HOLD_RESERVE_FOR_MINUTES + 1, ChronoUnit.MINUTES);
        reservationService.unreserveOld();

        assertThat(flashHistoryDao.getAllRecords(), hasSize(historyCountBefore + 1));
    }

    @Test
    public void shouldTransferStockFromBudgetToReserve() {
        reservationService.reserve(uid, FlashOfferUtils.DEFAULT_OFFER_WARE_ID, RESERVE_QUANTITY.intValue());

        assertThat(budgetService.getBalance(getReservation().getAccountId()), comparesEqualTo(RESERVE_QUANTITY));
        assertThat(budgetService.getBalance(offerBudgetAccountId), comparesEqualTo(INITIAL_STOCK.subtract(RESERVE_QUANTITY)));
    }
    
    @Test
    public void shouldReturnStockToBudgetOnUnreserve() {
        reservationService.reserve(uid, FlashOfferUtils.DEFAULT_OFFER_WARE_ID, RESERVE_QUANTITY.intValue());

        clock.spendTime(HOLD_RESERVE_FOR_MINUTES + 1, ChronoUnit.MINUTES);

        reservationService.unreserveOld();
        assertThat(budgetService.getBalance(getReservation().getAccountId()), comparesEqualTo(BigDecimal.ZERO));
        assertThat(budgetService.getBalance(offerBudgetAccountId), comparesEqualTo(INITIAL_STOCK));
    }
}
```
</details>
