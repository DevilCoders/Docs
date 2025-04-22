

### Nginx plugin for exchanging user passport credentials for TVM2 user-tickets 

To minimize risks of leaking long-living credentials (like OAuth tokens or session cookies), it's recommended to use short-living [TVM2 user-tickets](https://wiki.yandex-team.ru/passport/tvm2/user-ticket/) for user authorized requests between services. 

In scenario when Nginx runs as external API gateway, this plugin allows replacing passport credentials with User-tickets before proxying request to upstreams.
Under the hood it makes request to [Blackbox](https://doc.yandex-team.ru/blackbox) methods to issue user ticket.

The plugin consists of 
* Local yacare servant `auth_agent`, that interacts with blackbox api and parses results.
* Lua script `auth-nginx.lua`, that uses Nginx cosockets api to make local http subrequest to the agent and updates original request headers.

### Lua API
Plugin designed as lua module and loaded as:  
`auth_plugin = require 'auth-nginx'`  
Result table contains api methods.

`ticket, err = auth_plugin.exchange_oauth_for_user_ticket(custom_error_handlers)`  
`ticket, err = auth_plugin.exchange_sessionid_for_user_ticket(custom_error_handlers)`  
Both methods make subrequest to local auth_agent to aquire user-ticket.  
And on success put ticket into `X-Ya-User-Ticket` request header.  
On error ticket is nil and err is:  
`nil` if no auth credential present in the request  
`401` Unauthorized - failed authentication with given credential  
`500` Internal - failed agent request  
By default request is automatically rejected on Unauthorized or Internal errors.  
To override this behaviour, pass table in `custom_error_handlers` parameter containing callbacks:
- `on_empty_auth()`
- `on_unauthorized_error()`
- `on_internal_error()`  

`auth_plugin.remove_request_oauth()`  
Removes OAuth from request headers.

`auth_plugin.remove_request_sessionid()`  
Removes Session_id and sessionid2 from request cookies.

`auth_plugin.error_handlers`  
Default error handlers table. You can override default behavior for any `exchange_*` call (with `custom_error_handler` parameter) or globally (by updating this table entries). 
- `on_empty_auth()` called when request contains no auth info. Default does nothing.  
- `on_unauthorized_error()` called when agent response is 401(Unauthorized). Default automaticaly rejects request with 401.  
- `on_internal_error()` called on unexpected agent errors (failed blackbox request, timeout, etc). Default automatically rejects request with 500.


### Configuration and usage <a name="auth_agent_setup"></a>

- Include plugin package into docker pkg.json.  
- Configure tvmtool to obtain service-tickets for Blackbox, see [instruction](https://wiki.yandex-team.ru/geo-infra/bbusage/).  
  Correct blackbox **dst_id**:  
  `222` (production blackbox) for stable  
  `239` (blackbox-mimino) for testing  
  `226` (blackbox-stress) for load  
- Don't forget to request blackbox grants ([documentation link](https://docs.yandex-team.ru/blackbox/concepts/getting-access)).

Call plugin on access phase of nginx location handler:
```
http {
...
  server {
      location /user_access_handle {
          access_by_lua_block {
            local auth_plugin = require 'auth-nginx'
            -- Example for custom error handling
            -- Want to reject requests without user credentials
            override_error_handlers = {
              on_empty_auth = function()
                  auth_plugin.reject(ngx.HTTP_UNAUTHORIZED)
              end
            }

            auth_plugin.exchange_oauth_for_user_ticket(override_error_handlers)
            auth_plugin.remove_request_oauth()
          }
          proxy_pass some_upstream;
      }
  }
}
```

#### Using auth_agent/ping in service health check
If most of your requests require user authorization, consider calling auth_agent/ping in your main /ping handle.  
This way Nanny's deploy will halt in case of problems with auth_agent and balancers won't direct traffic to failed hosts.  

Example redirecting main ping to auth_agent:
```
server {
...
    location = /ping {
        proxy_set_header Host "auth-agent.maps.yandex.ru";
        proxy_pass http://localhost:80/ping;
    }
}
```
In more advanced case, you can configure multiple subrequests in your /ping ([example](https://a.yandex-team.ru/arc/trunk/arcadia/maps/mobile/server/legacy/mapkit/docker/install/etc/nginx/sites-enabled/nginx.conf?rev=5989675#L45))
