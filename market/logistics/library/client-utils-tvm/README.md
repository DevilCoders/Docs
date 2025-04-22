# client-utils-tvm
Библиотека для проверки тикетов TVM.

## Описание использования библиотеки

Центральной точкой входа является класс TvmSecurityConfiguration.
Чтобы проинициализировать библиотеку необходимо выполнить импорт конфигурации в спринг, например так:

    @Configuration
    @Import(TvmSecurityConfiguration.class)
    public class TvmAutoConfiguration {

Конфигурация принимает на вход TvmClient и список List<TvmTicketChecker>. 
Список cheker'ов может быть заполнен как стандартными реализациями проверок тикетов, так и кастомными.
Пример бина для стандартной проверки тикетов:

    @Bean
    @ConfigurationProperties("tvm.back-office")
    public TvmTicketChecker backOfficeChecker() {
        return new TvmTicketCheckerImpl();
    }
, где используются свойства:

- список масок методов, которые будет проверять реализация checker'а:
    

    tvm.back-office.api-methods=/back-office/*,/*/secured/*
- список идентификаторов допустимых сервисов (если не задано - допустимы любые сервисы):


    tvm.back-office.allowed-service-ids=1,3,32
- режим, в котором ошибки аутентификации будут только логироваться (аутентификация будет считаться успешной):


    tvm.back-office.log-only-mode=true
- свойство, указывающее на необходимость проверки user-тикетов


    tvm.back-office.check-user-ticket=true

Можно также задать маску для методов без аутенитификации:

    tvm.unsecured-methods=/ping    
    
## Документация TVM
[Документация](https://wiki.yandex-team.ru/passport/tvm2/)

## Сборка и тестирование
[ya.make](https://wiki.yandex-team.ru/yatool/make/)
