# common-alerts

Библиотека для автоматической генерации алертов по аннотациям над методами http контроллеров.

В коде это выглядит так:

```
    // По данной аннотации сформируется алерт, который вернёт:
    //  - WARN в случае, если 1% и более вызовов завершился с кодом ошибки 5хх
    //  - ALARM в случае, если 5% и более вызовов завершился с кодом ошибки 5хх
    @ErrorPercent(warn = 1, crit = 5)

    // По данной аннотации сформируется алерт, который вернёт:
    //  - WARN в случае, если в 95-м перцентиле длительность вызова метода превысила 10 секунд
    //  - ALARM в случае, если в 95-м перцентиле длительность вызова метода превысила 15 секунд
    @Timing(warn = 10000, crit = 15000, quantile = Q95)

    @RequestMapping(value = "/shops/{shopId}/cart", method = RequestMethod.POST)
    public CartResponse cart(
            @PathVariable long shopId,
            @RequestBody Cart cart
    ) {
      // ...
    }
```

Данная библиотека не занимается сбором метрик - она лишь даёт возможность получить автоматически алерты для мониторинга
в разрезе http ручек для Соломона.

Итак, предположим у вас для вашего сервиса в Соломоне уже собираются все метрики и вы хотите настроить автоматическую
генерацию алертов для мониторинга. Вам нужно сделать следующее:

1. Подключить зависимость на эту библиотеку (Также, посмотрите список зависимостей, которые принесёт вам эта
   библиотека):

   ```
    PEERDIR (
        market/jlibrary/common-alerts
    )
   ```

2. Прочитать описание классов @Timing и @ErrorPercent, чтобы увидеть, какие параметры имеются у данных аннотаций, и
   понимать возможности.

3. Расставить аннотации @Timing и @ErrorPercent над методами контроллеров с допустимыми на ваш взгляд настройками.
   Хорошей практикой является включить в набор модульных тестов тест, который будет проверять наличие аннотаций для
   генерации алертов для каждой метода. В таком случае, при добавлении нового метода система тестирования автоматически
   сможет напомнить, что нужно указать настройки для генерации алерта.

   Если у вас есть метод, для которого данные настройки не нужны - воспользуйтесь аннотацией @NoHealth

   Пример теста:
   ```
       private static final List<Class<? extends Annotation>> ANNOTATIONS = Arrays.asList(
            RequestMapping.class,
            GetMapping.class,
            PostMapping.class,
            PutMapping.class,
            DeleteMapping.class,
            PatchMapping.class
       );

       private void checkThatMethodsAreAnnotatedWithAnnotation(Class<? extends Annotation>... annotationClasses) {
         Reflections reflections = new Reflections(packagePrefix, new MethodAnnotationsScanner());

         List<Method> methods = ANNOTATIONS.stream()
                .map(reflections::getMethodsAnnotatedWith)
                .flatMap(Set::stream)
                .filter(method -> !classesToSkip.contains(method.getDeclaringClass()))
                .filter(method -> Stream.of(annotationClasses).noneMatch(a -> method.getAnnotation(a) != null))
                .sorted(Comparator.comparing(m -> m.getDeclaringClass().getCanonicalName()))
                .collect(Collectors.toList());

         methods.forEach(m -> LOG.error("Found method without @" + annotationClasses[0].getSimpleName() + ": {}", m));

         assertThat(methods, empty());
       }

       @Test
       public void requestMappingMethodsShouldBeAnnotatedWithErrorPercentAnnotation() {
         checkThatMethodsAreAnnotatedWithAnnotation(ErrorPercent.class, NoHealth.class);
       }

       @Test
       public void requestMappingMethodsShouldBeAnnotatedWithTimings() {
         checkThatMethodsAreAnnotatedWithAnnotation(Timing.class, NoHealth.class);
       }
   ```

4. Для сбора метрик в Соломон у вас скорей всего используется LogShatter с его матчингом урлов. Для этого обычно делают
   ручку /pagematch, которая возвращает маппинг page_id на урлы вашего сервиса. Поэтому, если у вас есть в Соломон
   разрезы по ручкам, то у вас уже реализована и ручка /pagematch (либо вы используете что-то альтернативное).

   Для генерации алертов важно то, чтобы page_id в Соломоне соответствовал page, который генерируется данной
   библиотекой.

   Из коробки данная библиотека предоставляет специальный класс SpringRequestMethodProvider, который реализует интерфейс
   MethodProvider. Через данный интерфейс библиотека получает от вашего сервиса набор описаний методов для генерации
   алертов.

   SpringRequestMethodProvider - это поставщик такого описания на основании маппингов Spring. Описание бина выглядит
   обычно так:

   ```
    @Configuration
    public class WebContextConfig {

      @Bean
      // handlerMappings - поставляет Spring
      public MethodProvider methodProvider(List<RequestMappingInfoHandlerMapping> handlerMappings) {
          return new SpringRequestMethodProvider(handlerMappings);
      }
   }
   ```
   Эта реализация достаточно проста и использует автоматическое отображение url -> page_id следующего вида:
   /orders/by-shop/{shopId} ->      orders_by-shop_shopId

   Код генерации page_id находится тут:
   ru.yandex.market.health.methods.PageUtils.getPageId

   Если данный способ вам не подходит, так как page_id генерируются другим способом, то придётся сделать собственную
   реализацию интерфейса MethodProvider.

   Если так получилось, что ваш /pagematch генерировал в таком же формате, то вы можете избавиться от собственной
   реализации и перейти на реализацию из коробки:
   ```
     PageMatchProvider pageMatchProvider = new MethodPageMatchProvider(methodProvider);
     String response = pageMatchProvider.getPagePatch();
   ```

5. Реализовать собственную фабрику для генерации алертов.

   Самый простой способ - наследовать её от AbstractAlertFactory. Пример:
   ```
    public class PushApiAlertFactory extends AbstractAlertFactory {

        /**
         * Конструктор.
         *
         * @param project              проект в Соломон
         * @param service              сервис в Соломон
         * @param periodMillis         интервал расчета алерта
         * @param notificationChannels набор каналов для уведомлений
         */
        public PushApiAlertFactory(String project, String service, long periodMillis,
                                   List<String> notificationChannels) {
            super(project, service, periodMillis, notificationChannels);
        }

        protected String getSolomonSelector(HttpEndPointAlertContext context) {
            return String.format("{" +
                            "cluster='%s', " +                      // кластер
                            "service='%s', " +                      // сервиса
                            "method='%s', " +                       // page_id или метод, по сути идентификатор
                            "http_method='%s', " +                  // http verb, если на один урл сразу 2 и более действий
                            "project='%s', " +                      // проект
                            "period='%s', " +                       // период сбора метрики
                            "type='%s', " +                         // timings или 5xx-percent
                            "sensor='%s'" +                         // название метрики
                            "%s" +                                  // дополнительные ограничения
                            "}",
                    getCluster(context),
                    service,
                    context.getMethod(),
                    context.getVerb(),
                    project,
                    context.getPeriod().label(),
                    getType(context),
                    context.getKind() == AlertKind.TIMING
                            ? "http.response_milliseconds"
                            : "http.5xx_percent",
                    context.getKind() == AlertKind.TIMING
                        ? "quantile='" + context.getQuantile().dotLabel() + "'"
                        : ""
            );
        }

        protected String getCluster(HttpEndPointAlertContext context) {
            switch (context.getEnvironment()) {
                case TESTING:
                    return "testing";
                case PRESTABLE:
                    return "prestable";
                case PRODUCTION:
                default:
                    return "stable";
            }
        }
    }
   ```
   Как видно из примера - здесь просто определяется селектор для Соломон, чтобы выбрать данные для конкретной ручки
   и конкретной метрики.
   Селектор используется для двух типов алертов:
   * Алерт на превышение времени ответа ручки
   * Алерт на превышение процента количества ошибок ручки

   Метод getSolomonSelector принимает на вход context: AlertContext, где через метод getKind() можно понять селектор для
   какого типа алерта сейчас запрашивается. Для алерта на превышение времени ответа в контексте есть квантиль и если сервис
   поддерживает сбор метрик по разным квантилям, то селектор должен содержать ограничение по нему

   Для алерта на превышение процента ошибок в контексте есть тип ошибок, например, только 5хх.


6. Реализовать бин для поставки описаний алертов AlertsProvider.
   Здесь можно воспользоваться вариантом из коробки - EndPointsAlertProvider.
   Например, так:
   ```
    @Bean
    public AlertsProvider alertsProvider(
            MethodProvider methodProvider,
            @Value("${market.pushapi.solomon.project_id:market-checkout}") String projectId,
            @Value("${market.pushapi.solomon.notification_channels:telegram}") List<String> notificationChannels,
            @Value("${market.pushapi.solomon.period_millis:3720000}") int periodMillis,
            @Value("${market.pushapi.solomon.solomon_service:market-checkout-push-api}") String sensorService
    ) {
        // PushApiAlertFactory - собственная фабрика, которая наследует AbstractAlertFactory и
        // предоставляет реализацию метода getSolomonSelector

        return new EndPointsAlertProvider(
                new PushApiAlertFactory(
                        projectId,
                        sensorService,
                        periodMillis,
                        notificationChannels
                ),
                methodProvider,
                Set.of(Environment.PRODUCTION)  // набор окружений для которых генерировать алерты
        );
    }
   ```

7. Реализовать ручку, которая вернёт набор описаний алертов. Например:
   ```
    @RestController
    public class HealthController {

        private final AlertsProvider alertsProvider;

        public HealthController(AlertsProvider alertsProvider) {
            this.alertsProvider = alertsProvider;
        }

        @NoHealth
        @GetMapping(value = "/health/solomon", produces = MediaType.APPLICATION_JSON_UTF8_VALUE)
        public List<Alert> getHealthAlerts() {
            return alertsProvider.getAlerts();
        }
    }
   ```

8. Добавить в релизный пайплайн кубик, который дернёт ручку из п.7 и добавит в Соломон новые алерты.
   Пример кубика: https://tsum.yandex-team.ru/pipe/jobs/6e877320-89f7-401c-8f33-566f2f302db2
   В конфигурации Job (https://tsum.yandex-team.ru/pipe/resources/81ac60a9-732d-46f8-b430-483dfbc31069) указываем параметры и всё.

   Код данной таски по генерации можно посмотреть тут (для любознательных):
   https://a.yandex-team.ru/arc_vcs/sandbox/projects/market/checkout/MarketCheckouterGenerateAlerts/alerts.py
