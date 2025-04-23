MBI PARTNER-TVM (библиотека для работы с tvm в mbi)

## Разработка
Разработка идет в arc. Настройка arc: https://wiki.yandex-team.ru/arcadia/arc/
1. Создать проект для Idea: `ya ide idea -r /Users/neliubin/IdeaProjects/mbi-partner-tvm -l /Users/neliubin/arc/arcadia/market/mbi/partner-tvm --iml-in-project-root`

## Использование 
Библиотека предоставляет реализации фильтров, auth-менеджеров и тестовых заглушек.
Для работы с библиотекой необходимо:
1. Добавить зависимость `mbi-partner-tvm` в свой проект
2. Подключить конфиг `TvmConfig` (e.g.: `@Import(TvmConfig.class)`)
3. Добавить фильтр `TvmAuthenticationFilter`. Для этого удобно использовать `TvmAdjuster`
4. Установить проперти: `mbi.partner_tvm.tvm2.client_id`, `mbi.partner_tvm.tvm2.allowed_client_ids`, `mbi.partner_tvm.tvm2.secret`

На этом подключение закончено. TVM будет работать. Пример конфига:
```
@Configuration
@EnableWebSecurity
@Import({ TvmConfig.class })
@ParametersAreNonnullByDefault
public class MvcSecurityConfig extends WebSecurityConfigurerAdapter {
    private static final List<String> UNSECURED_METHODS = new ImmutableList.Builder<String>()
            // Health / Graceful shutdown
            .add("/ping")
            .add("/monitoring")
            .add("/close")
            .add("/open")
            .add("/pagematch")
            .build();
            
    private final TvmAdjuster tvmAdjuster;
    
    public MvcSecurityConfig(final TvmAdjuster tvmAdjuster) {
        this.tvmAdjuster = tvmAdjuster;
    }
    
    @Override
    public void configure(final WebSecurity web) {
        web.ignoring()
              .antMatchers(UNSECURED_METHODS.toArray(new String[0]));
     }
}

```

### Настройка в тестах
По умолчанию в тестах используется боевая версия tvm. Если в тестах нет необходимости использовать реальный tvm, 
то необходимо установить значение проперти `mbi.partner_tvm.tvm2.enabled=false`.
Тогда будет использоваться фейковая версия tvm, подробнее о ней написано ниже

### Локальный запуск без TVM
Для локального запуска tvm можно отключить. Достаточно установить проперти `mbi.partner_tvm.tvm2.enabled=false`.
Фактически при установке этого свойства tvm не отключается полностью, вместо реальных tvm-client'a и authenticationManager'a используются их фейковые реализации
(manager пропускает абсолютно все запросы, tvm-client создает простые тикеты и ничего не проверяет), фильтры при этом создаются настоящие. 

### Подключение к существующему проекту
Существует несколько возможных стратегий проверки сервис/юзер тикетов `TicketCheckStrategy`, подробнее о них можно прочитать в документации.  
По умолчанию установлены стратегии: для сервис тикетов `REQUIRED`, поменять его можно, изменив значение проперти `mbi.partner_tvm.tvm2.service_ticket.check`; 
для юзер тикетов `OPTIONAL_EXCEPTION`, поменять его можно, изменив значение проперти `mbi.partner_tvm.tvm2.user_ticket.check`.

### Обработка ошибок
Если возникла ошибка, то будет выброшено исключение `TvmAuthenticationException`. 
Есть дефолтный  обработчик `TvmAuthenticationFailureHandler`, который использует формат из `partner-error-info`. 
Его можно отключить через `mbi.partner_tvm.tvm2.default_failure_handler.enabled=false`. И после этого можно задать свой

### Возможные проблемы
Конфиги подключаются через `@ConditionalOnProperty`. Там берутся проперти из Environment. 
Ваши проперти из `.properties` файлов могут не попадать туда. Решение - использовать `ru.yandex.market.application.properties.AppPropertyContextInitializer`
Это реализация `ApplicationContextInitializer`, добавляющая в `org.springframework.core.env.Environment` `.properties` файлы из директории `properties.d`.checkUserTicket` класса `TvmAuthenticationManager` и переопределить бин `authenticationManager` 