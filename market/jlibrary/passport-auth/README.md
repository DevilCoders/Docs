passport-auth Библиотека, позволяющая легко интегрировать в Web приложение авторизацию во внешнем/внутреннем Паспорте
==================

На текущий момент умеет:
1) Авторизовывать запрос от пользователя в BlackBox по Session_id/sessionid2.
2) Имеет реализацию Spring Security, которая авторизует пользователя в Паспорте.
3) Дополнительно имеет Spring MVC реализацию API для взаимодействия с IDM, чтобы можно было настраивать роли через IDM при использовании внутреннего Паспорта.

Пример настройки аутентификации в Паспорте:

```java
@Configuration
@EnableWebSecurity
public class SecurityConfig extends WebSecurityConfigurerAdapter {

....

    @Bean
    public Tvm2 tvm2() {
        return new Tvm2Builder()
            .setCredentials(new TvmClientCredentials(tvmClientId, tvmClientSecret))
            .setUserAgent(userAgent)
            .build();
    }

    @Bean
    public Blackbox2 blackbox2() {
        return new Blackbox2Builder()
            .setTvm(tvm2())
            .setBlackboxServiceId(blackboxTvmServiceId)
            .setUrl(blackboxUrl)
            .setUserAgent(userAgent)
            .build();
    }

    @Bean
    public PassportAuthService authService() {
        return new PassportAuthServiceBuilder()
            .setBlackBoxClient(blackbox2())
            .setServiceHost(serviceHost)
            .setUseCache(true)
            .setLoginUrl(loginUrl)
            .setRequireHttpsAuth(requireHttps)
            .setDebug(debugMode)
            .setDebugUser(debugUser)
            .setUserDao(authUserDao())
            .build();
    }

    @Override
    public void configure(WebSecurity web) {
        web.ignoring().antMatchers("/ping", "/monitoring", "/open", "/close");
        web.ignoring().antMatchers("/favicon.ico");
        web.ignoring().antMatchers("/error");
    }

    @Override
    protected void configure(HttpSecurity http) throws Exception {
        RememberMeAuthenticationFilter authFilter = new RememberMeAuthenticationFilter(
            authenticationManager(), authService()
        );

        http.authorizeRequests().anyRequest().authenticated()
            .and().addFilterBefore(authFilter, UsernamePasswordAuthenticationFilter.class)
            .formLogin().loginPage(loginUrl);

        http.csrf().disable();
    }
}
```

Для настройки интеграции с IDM нужно сделать следующее:

1. Настроить контроннер для апи сервиса IDM:

```java
@RequestMapping("/api/idm")
public class IdmController extends ru.yandex.market.passport.internal.idm.spring.IdmController {

    public IdmController(IdmDao idmDao) {
        super(idmDao);
    }
}
```

2. Выложить в тестинг и прод

3. Договориться с админами, чтобы настроили авторизацию по клиентскому сертификату для этой ручки, пример
https://st.yandex-team.ru/CSADMIN-24665 (там есть PR-ы)

4. Дать заявку на интеграцию https://wiki.yandex-team.ru/Intranet/idm/new/
