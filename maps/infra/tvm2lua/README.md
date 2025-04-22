

### TVM2 Nginx plugin

Provides lua api to issue TVM2 service ticket for request or validate incoming service tickets before proxying requests to upstream.  
Requires configured tvmtool daemon (see [wiki/geo-infra/tvm2usage](https://wiki.yandex-team.ru/geo-infra/tvm2usage))  
Under the hood plugin uses [ticket_parser2](https://a.yandex-team.ru/arc/trunk/arcadia/library/cpp/tvmauth/client) library.


### Lua API
```configure_via_tvmtool(self_alias)```  
Call within init_by_lua* directive (on nginx master initialization)  
Validates tvmtool.conf on nginx configuration check, prevents nginx start if validation fails.
Parameter is an alias for the service configured in tvmtool.conf.  

```init_via_tvmtool()```  
Call within init_worker_by_lua* directive (on nginx worker initializtion)  
Initializes plugin communication with tvmtool daemon.  

```check_service_ticket(allow_no_ticket)```  
Call within access_by_lua* directive in location configuration.  
Validates service ticket and automatically rejects request if ticket is invalid or absent.  
To allow access without ticket, pass true in the 'allow_no_ticket' parameter.  
**On success** sets X-Ya-Src-Tvm-Id header and returns ticket source id.   
**On failure** rejects request with HTTP 403 or HTTP 500 (on internal error)

```attach_service_ticket(destination_alias)```  
Call within access_by_lua* directive in location configuration.  
Issues service ticket to given destination and places it in the X-Ya-Service-Ticket request header.  
Parameter is an alias for destination service configured in tvmtool.conf.  
Returns true on success.


### Usage

```
http {

  init_by_lua_block {
    plugin = require 'tvm2-nginx'
    plugin.configure_via_tvmtool('my-service-alias')  -- service own alias from tvmtool.conf
  }
  ...
  init_worker_by_lua_block {
    plugin = require 'tvm2-nginx'
    plugin.init_via_tvmtool() -- call after nginx workers forked 
  }

  server {
      ...
      location /some_handle {
          access_by_lua_block {
            plugin = require 'tvm2-nginx'
            plugin.attach_service_ticket('destination-alias') -- destination alias from tvmtool.conf
          }
          ...
          proxy_pass some_upstream;
      }

      location /another_handle {
          access_by_lua_block {
            plugin = require 'tvm2-nginx'
            plugin.check_service_ticket()
          }
          ...
          proxy_pass some_upstream;
      }
  }
}
```

### Killswitch

```tvm2-nginx-ctl.sh``` shell script disables plugin in case of emergency.

