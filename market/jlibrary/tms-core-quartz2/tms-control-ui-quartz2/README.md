## UI для управления TMS

### Установка и конфигурация
Используется node 14. Можно установить через nvm

`nvm install 14.4.0`

`nvm use 14.4.0`

Подробнее ознакомиться с nvm можно [тут](https://github.com/nvm-sh/nvm)

### Локальная сборка и запуск
После конфигурации node и npm локально проект собирается при помощи

`npm ci`

При этом по файлу **package.json** будет сгенерирована папка **node_modules** с зависимостями, а также файл **package-lock.json**

В корне проекта надо создать файл .env и записать туда переменную PROXY с хостом на который будут уходить запросы, например:

`PROXY=https://cm-testing.market.yandex-team.ru/autoorder`

Запускается при помощи `npm start`

Так же, если запросы не проходят, то для localhost может потребоваться прописать куки авторизации: yandexuid, sessionid2, Session_id

### Публикация изменений в package.json
1. Добавить зависимости с помощью `npm install`.
2. Локально собрать при помощи `ya make`.

### Подключение к своему сервису

Данную бибилотеку можно подключать к java севисам Маркета, которые используют библиотеку https://a.yandex-team.ru/arc/trunk/arcadia/market/jlibrary/tms-core-quartz2/tms-core-quartz2

#### Настройки ya.make
Помимо библиотеки

`market/jlibrary/tms-core-quartz2/tms-core-quartz2`

подключаем через ya.make

`market/jlibrary/tms-core-quartz2/tms-web-quartz2`

`market/jlibrary/tms-core-quartz2/tms-control-ui-quartz2`

#### Настройки WebMvcConfigurer

Настраиваем конфигурацию статической страницы библиотекки через `WebMvcConfigurer`,
где в методе `addResourceHandlers` настраиваем доступ к статическим ресурсам,
а в методе `addViewControllers` задаем кастомный адрес страницы (в данном случае /tms-ui)

```java
@Configuration
@EnableWebMvc
public class WebConfig implements WebMvcConfigurer {

    @Override
    public void addResourceHandlers(ResourceHandlerRegistry registry) {
        registry.addResourceHandler("/**").addResourceLocations("classpath:/public/");
    }

    @Override
    public void addViewControllers(ViewControllerRegistry registry) {
        registry.addViewController("/tms-ui")
            .setViewName("forward:/index.html");
    }
}
```

В случае когда ваш сервис A (в котором настроен TMS) проксируется другим сервисом B
и доступ к ручкам сервиса A осуществляется по адресу `{хост_сервиса_B}/xxx/{ручка_сервиса_A}`,
то в `WebMvcConfigurer` потребуются дополнительная настройка (чтобы страница TMS UI была доступна по адресу `{хост_сервиса_B}/xxx/tms-ui`)

Расширенный пример конфигурации для такого случая:

```java
@Configuration
@EnableWebMvc
public class WebConfig implements WebMvcConfigurer {

    private static final String BASE_API_URL = "window.API_URL=\"/\"";

    @Value("${tms.control.ui.api.url.prefix}")
    private String tmsControlUiApiUrlPrefix; // в данном примере это "xxx"

    @Override
    public void addResourceHandlers(ResourceHandlerRegistry registry) {
        registry.addResourceHandler("/**")
            .addResourceLocations("classpath:/public/")
            .resourceChain(false)
            .addTransformer((request, resource, transformerChain) -> {
                String filename = resource.getFilename();
                if (filename != null && filename.equals("index.html")) {
                    String newApiUrl = "window.API_URL=\"/" +
                        (tmsControlUiApiUrlPrefix == null ? "" : tmsControlUiApiUrlPrefix) + "\"";
                    String html = IOUtils.toString(resource.getInputStream(), UTF_8);
                    html = html.replace(BASE_API_URL, newApiUrl);
                    return new TransformedResource(resource, html.getBytes());
                }
                return resource;
            });
    }

    @Override
    public void addViewControllers(ViewControllerRegistry registry) {
        registry.addViewController("/tms-ui")
            .setViewName("forward:/index.html");
    }
}
```
Тут в сервисе A подправляется настройка url-адреса, прописанная в уже подгруженной статической странице TMS UI

#### Ограничение прав на запуск джоб

Если необходимо навесить авторизацию на запуск джоб через страничку TMS UI, то при использовании Spring Security в проекте это можно сделать через настройки WebSecurityConfigurerAdapter

Пример для ROLE_TMS_UI_ADMIN:
```java
    @Override
    protected void configure(HttpSecurity http) throws Exception {
        var httpSecurity = http
            .authorizeRequests()
            .antMatchers("/tms/jobs/run").hasRole("TMS_UI_ADMIN")
            .permitAll()
            .anyRequest().authenticated()
            .and()
            .csrf().disable();
    }
```
