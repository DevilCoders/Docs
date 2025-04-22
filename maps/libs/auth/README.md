Library for user authorization with Blackbox api.  
Also provides automation for working with TVM through local tvmtool daemon.  

[TOC]

### Working with tvmtool daemon
`TvmtoolSettings` automatically reads tvmtool.conf contents to help correctly setup `TTvmClient` instance with connection to local tvmtool.  
While library can implicitly identify client config section (when there's only one present), it's not recommended to rely on.  
Preferable way is to explicitly specify client and blackbox aliases with `TvmtoolSettings` methods.  

Example:
```cpp
#include <maps/libs/auth/include/tvm.h>

// Usually TTvmClient instance is global
std::optional<NTvmAuth::TTvmClient> g_tvmClient;
 
int main() {
    // Load tvmtool config and explicitly select client section
    auto settings = maps::auth::TvmtoolSettings()
        .selectClientAlias("my-alias");
    // Create TTvmClient working with tvmtool
    g_tvmClient = settings.makeTvmClient();
}
```

### Blackbox environment
`BlackboxEnvironment` combines blackbox instance with it's TVM parameters: `tvmId` and `type`.  
Library provides predefined environments for known blackbox instances.  

### Blackbox api

`BlackboxApi` class wraps blackbox instance with TTvmClient and works as queries factory.  
Constructed queries are bound to the blackbox instance and automatically supplied with TVM service ticket.  

Instance of `BlackboxApi` can be initialized automatially from tvmtool settings, or setup manually.  

Example:
```cpp
// Automatically select blackbox instance from parameters set in tvmtool.conf
// Load tvmtool config and explicitly select client section
auto tvmSettings = maps::auth::TvmtoolSettings()
    .selectClientAlias("my-alias")  // select client section
    .setBlackboxAlias("blackbox");  // select blackbox dst
auto blackboxApi = maps::auth::BlackboxApi(tvmSettings);

// Manually select Blackbox "Mimino" and setup TTvmClient working through tvm-api
NTvmAuth::NTvmApi::TClientSettings tvmapiSettings;
settings.SetSelfTvmId(SELF_TVM_ID);
settings.EnableServiceTicketsFetchOptions(getSecret(), {{BLACKBOX_MIMINO.tvmId}})
auto blackboxApi = maps::auth::BlackboxApi(BLACKBOX_MIMINO, NTvmAuth::TTvmClient(tvmapiSettings));
```


### Blackbox queries

Each query class corresponds to one of Blackbox api methods ([see api documentation](https://docs.yandex-team.ru/blackbox/concepts/intro-api))  
All queries return `UserInfo` as result.  
Wnen constructed through `BlackboxApi` instance, queries are automatically supplied with TVM service ticket for the blackbox instance.  

Examples:
```cpp
#include <maps/libs/auth/include/blackbox.h>

// BlackboxApi instance usually global 
auto blackboxApi = maps::auth::BlackboxApi(
    maps::auth::TvmtoolSettings()
        .selectClientAlias("my-alias")
        .setBlackboxAlias("blackbox")
);

...

// oauth method
auto userInfo = blackboxApi.oauthQuery()
        .setToken(oauthToken)
        .setRemoteAddress(userip)
        .execute();

// user_ticket method
auto userInfo = blackboxApi.userTicketQuery()
        .setUserTicket("3:user:CJ8SEMz_3tEFGiAKBgjou-DzDhD...")
        .execute();

// sessionid method
auto userInfo = blackboxApi.userTicketQuery()
        .setSessionId(sessionIdCookie)
        .setRemoteAddress(userip)
        .setHost(cookieHost);
        .execute();
```

### Documentation links
Yandex Blackbox [reference docs](https://docs.yandex-team.ru/blackbox/concepts/getting-access).  
**NB**: Blackbox access requires explicit grants, see details in corresponding doc section.  

See [wiki/geo-infra/tvm2usage](https://wiki.yandex-team.ru/geo-infra/tvm2usage/) instructions for setting up TVM with tvmtool.
