## Библиотека для работы с ITS.
#### ITS wms - https://nanny.yandex-team.ru/ui/#/its/locations/market/wms
#### Документация ITS - https://wiki.yandex-team.ru/runtime-cloud/nanny/its/

### Как использовать
1) Создать конфиг локации [тут](https://nanny.yandex-team.ru/ui/#/its/locations/market/wms), рядом с achievement и т.д. Конфиг создают только Matry через заявку ([пример](https://st.yandex-team.ru/MARTY-5672)). Создать нужно **только локацию** по аналогии:
```yaml
wms:
  groups:
    achievement:
      production:
        filter: f@production_market_wms_achievement_sas f@production_market_wms_achievement_vla
        ruchkas:
        - market_wms_settings
        responsible:
        - vasilenko-mni
        - doanisimov
        - svc_wms
      testing:
        filter: f@testing_market_wms_achievement_vla f@testing_market_wms_achievement_sas
        ruchkas:
        - market_wms_settings
        responsible:
        - vasilenko-mni
        - doanisimov
        - svc_wms

```
Ручка `market_wms_settings` и ACL уже есть

2) Создать `@Bean` `ru.yandex.market.wms.shared.libs.its.settings.provider.SettingsProvider`
Пример:
```java
@Configuration
public class SettingsConfig {
    @Bean
    @ConditionalOnProperty(name = "controls.location", matchIfMissing = false)
    public SettingsProvider<Settings> fileSettingsProvider(
        @Value("${controls.location}") String path,
        @Value("${controls.refreshRate}") Duration refreshRate,
        @Value("${controls.initialDelay}") Duration initialDelay,
        TaskScheduler taskScheduler,
        ObjectMapper objectMapper
    ) {
        return new FileSettingsProvider(new File(path), new Settings(), objectMapper, refreshRate, initialDelay, taskScheduler);
    }

    @Bean
    @ConditionalOnMissingBean(SettingsProvider.class)
    public SettingsProvider<Settings> mockSettingsProvider() {
        return new MockSettingsProvider(new Settings());
    }
}
```
в примере `Settings` - immutable класс, представляющий конфиг. Нужно создать свой, на который будет парсится json

3) `В Nanny -> Instance Spec` добавить новую секцию в `Instance data volumes` с типом `ITS`. Пример есть в [документации](https://docs.yandex-team.ru/nanny/how-to/structured-instancectl-config#volumes)


