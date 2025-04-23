## Мониторинги жизнеспособности приложения

#### Библиотека призвана решить две проблемы:
* Использование `PingChecker` как базиса для активных ping-проверок с реализацией логики вычисления результата 
проверки самостоятельно
* Использование свежей версии СПОКа принуждает к использованию общей конфигурации со встроенными эндпоинтами
ping-проверок на базе ComplexMonitoring — но такая схема подразумевает проактивную проставку статуса каким-то демоном,
а не опрос чекеров

Проблему решаем через слияние методологий проактивных чекеров, которых опрашиваем при проверке.

#### Как использовать:
1. В любом случае необходимо добавить в конекст бины типа `HealthChecker`, для удобства есть реализация
`PingCheckerHealthCheck`, которая может использовать все реализации `PingChecker`.

2. На новом СПОКе (main-класс наследуется от MarketApplicationCommonBaseConfig) нужно
импортировать в контекст `HealthServiceConfiguration`, а также переопределить `MonitoringController` примерно следующим образом:

    ```java
    public class ApplicationMonitoringController extends MonitoringController {
        private final HealthService healthService;
    
        public ApplicationMonitoringController(
            ComplexMonitoring generalMonitoring,
            ComplexMonitoring pingMonitoring,
            HealthService healthService
        ) {
            super(generalMonitoring, pingMonitoring);
            this.healthService = healthService;
        }
        
        @Override
        public ResponseEntity<String> ping() {
            healthService.updateChecks(); // Force update checks
            return super.ping();
        }
    }
    ```
  
4. На старом СПОКе с собственной реализацией ping-контроллера можно любым способом добавить в контекст бин
`HealthService`, а в ping-проверке вызывать метод `HealthService#getHealthStatus`
и отдавать `toString` результата как ответ.
