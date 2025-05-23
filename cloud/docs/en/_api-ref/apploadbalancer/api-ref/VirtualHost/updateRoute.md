---
editable: false
---

# Method updateRoute
Updates the specified route of the specified virtual host.
 

 
## HTTP request {#https-request}
```
POST https://alb.{{ api-host }}/apploadbalancer/v1/httpRouters/{httpRouterId}/virtualHosts/{virtualHostName}:updateRoute
```
 
## Path parameters {#path_params}
 
Parameter | Description
--- | ---
httpRouterId | <p>Required. ID of the HTTP router to update a route in.</p> <p>To get the HTTP router ID, make a <a href="/docs/application-load-balancer/api-ref/HttpRouter/list">list</a> request.</p> 
virtualHostName | <p>Required. Name of the virtual host to update a route in.</p> <p>To get the virtual host name, make a <a href="/docs/application-load-balancer/api-ref/VirtualHost/list">list</a> request.</p> 
 
## Body parameters {#body_params}
 
```json 
{
  "routeName": "string",
  "updateMask": "string",

  //  includes only one of the fields `http`, `grpc`
  "http": {
    "match": {
      "httpMethod": [
        "string"
      ],
      "path": {

        // `http.match.path` includes only one of the fields `exactMatch`, `prefixMatch`
        "exactMatch": "string",
        "prefixMatch": "string",
        // end of the list of possible fields`http.match.path`

      }
    },

    // `http` includes only one of the fields `route`, `redirect`, `directResponse`
    "route": {
      "backendGroupId": "string",
      "timeout": "string",
      "idleTimeout": "string",
      "prefixRewrite": "string",
      "upgradeTypes": [
        "string"
      ],

      // `http.route` includes only one of the fields `hostRewrite`, `autoHostRewrite`
      "hostRewrite": "string",
      "autoHostRewrite": true,
      // end of the list of possible fields`http.route`

    },
    "redirect": {
      "replaceScheme": "string",
      "replaceHost": "string",
      "replacePort": "string",
      "removeQuery": true,
      "responseCode": "string",

      // `http.redirect` includes only one of the fields `replacePath`, `replacePrefix`
      "replacePath": "string",
      "replacePrefix": "string",
      // end of the list of possible fields`http.redirect`

    },
    "directResponse": {
      "status": "string",
      "body": {
        "text": "string"
      }
    },
    // end of the list of possible fields`http`

  },
  "grpc": {
    "match": {
      "fqmn": {

        // `grpc.match.fqmn` includes only one of the fields `exactMatch`, `prefixMatch`
        "exactMatch": "string",
        "prefixMatch": "string",
        // end of the list of possible fields`grpc.match.fqmn`

      }
    },

    // `grpc` includes only one of the fields `route`, `statusResponse`
    "route": {
      "backendGroupId": "string",
      "maxTimeout": "string",
      "idleTimeout": "string",

      // `grpc.route` includes only one of the fields `hostRewrite`, `autoHostRewrite`
      "hostRewrite": "string",
      "autoHostRewrite": true,
      // end of the list of possible fields`grpc.route`

    },
    "statusResponse": {
      "status": "string"
    },
    // end of the list of possible fields`grpc`

  },
  // end of the list of possible fields

}
```

 
Field | Description
--- | ---
routeName | **string**<br><p>Required. Name of the route to update.</p> <p>To get the route name, make a <a href="/docs/application-load-balancer/api-ref/VirtualHost/get">get</a> request.</p> 
updateMask | **string**<br>Field mask that specifies which attributes of the route should be updated.
http | **object**<br>New settings of the HTTP route. <br> includes only one of the fields `http`, `grpc`<br>
http.<br>match | **object**<br>Condition (predicate) used to select the route.
http.<br>match.<br>httpMethod[] | **string**<br><p>HTTP method specified in the request.</p> 
http.<br>match.<br>path | **object**<br><p>Match settings for the path specified in the request.</p> <p>If not specified, the route matches all paths.</p> <p>A string matcher resource.</p> 
http.<br>match.<br>path.<br>exactMatch | **string** <br>`http.match.path` includes only one of the fields `exactMatch`, `prefixMatch`<br><br><p>Exact match string.</p> 
http.<br>match.<br>path.<br>prefixMatch | **string** <br>`http.match.path` includes only one of the fields `exactMatch`, `prefixMatch`<br><br><p>Prefix match string.</p> 
http.<br>route | **object**<br>Forwards the request to a backend group for processing as configured. <br>`http` includes only one of the fields `route`, `redirect`, `directResponse`<br>
http.<br>route.<br>backendGroupId | **string**<br><p>Required. Backend group to forward requests to.</p> <p>Stream (TCP) backend groups are not supported.</p> 
http.<br>route.<br>timeout | **string**<br><p>Overall timeout for an HTTP connection between a load balancer node an a backend from the backend group: the maximum time the connection is kept alive for, regardless of whether data is transferred over it.</p> <p>If a connection times out, the load balancer responds to the client with a ``504 Gateway Timeout`` status code.</p> <p>Default value: ``60``.</p> 
http.<br>route.<br>idleTimeout | **string**<br><p>Idle timeout for an HTTP connection between a load balancer node an a backend from the backend group: the maximum time the connection is allowed to be idle, i.e. without any data transferred over it.</p> <p>Specifying meaningful values for both ``timeout`` and ``idle_timeout`` is useful for implementing server-push mechanisms such as long polling, server-sent events (``EventSource`` interface) etc.</p> <p>If a connection times out, the load balancer responds to the client with a ``504 Gateway Timeout`` status code.</p> <p>If not specified, no idle timeout is used, and an alive connection may be idle for any duration (see ``timeout``).</p> 
http.<br>route.<br>prefixRewrite | **string**<br><p>Replacement for the path prefix matched by ``StringMatch``.</p> <p>For instance, if ``prefixMatch`` value is ``/foo`` and ``replace_prefix`` value is ``/bar``, a request with ``/foobaz`` path is forwarded with ``/barbaz`` path. For ``exactMatch``, the whole path is replaced.</p> <p>If not specified, the path is not changed.</p> 
http.<br>route.<br>upgradeTypes[] | **string**<br><p>Supported values for HTTP ``Upgrade`` header. E.g. ``websocket``.</p> 
http.<br>route.<br>hostRewrite | **string** <br>`http.route` includes only one of the fields `hostRewrite`, `autoHostRewrite`<br><br><p>Host replacement.</p> 
http.<br>route.<br>autoHostRewrite | **boolean** (boolean) <br>`http.route` includes only one of the fields `hostRewrite`, `autoHostRewrite`<br><br><p>Automatically replaces the host with that of the target.</p> 
http.<br>redirect | **object**<br>Redirects the request as configured. <br>`http` includes only one of the fields `route`, `redirect`, `directResponse`<br>
http.<br>redirect.<br>replaceScheme | **string**<br><p>URI scheme replacement.</p> <p>If ``http`` or ``https`` scheme is to be replaced and ``80`` or ``443`` port is specified in the original URI, the port is also removed.</p> <p>If not specified, the original scheme and port are used.</p> 
http.<br>redirect.<br>replaceHost | **string**<br><p>URI host replacement.</p> <p>If not specified, the original host is used.</p> 
http.<br>redirect.<br>replacePort | **string** (int64)<br><p>URI host replacement.</p> <p>If not specified, the original host is used.</p> 
http.<br>redirect.<br>removeQuery | **boolean** (boolean)<br><p>Removes URI query.</p> 
http.<br>redirect.<br>responseCode | **string**<br>HTTP status code to use in redirect responses.<br><ul> <li>MOVED_PERMANENTLY: ``301 Moved Permanently`` status code.</li> <li>FOUND: ``302 Found`` status code.</li> <li>SEE_OTHER: ``303 See Other`` status code.</li> <li>TEMPORARY_REDIRECT: ``307 Temporary Redirect`` status code.</li> <li>PERMANENT_REDIRECT: ``308 Permanent Redirect`` status code.</li> </ul> 
http.<br>redirect.<br>replacePath | **string** <br>`http.redirect` includes only one of the fields `replacePath`, `replacePrefix`<br><br><p>Replacement for the whole path.</p> 
http.<br>redirect.<br>replacePrefix | **string** <br>`http.redirect` includes only one of the fields `replacePath`, `replacePrefix`<br><br><p>Replacement for the path prefix matched by ``StringMatch``.</p> <p>For instance, if ``prefixMatch`` value is ``/foo`` and ``replace_prefix`` value is ``/bar``, a request with ``https://example.com/foobaz`` URI is redirected to ``https://example.com/barbaz``. For ``exactMatch``, the whole path is replaced.</p> 
http.<br>directResponse | **object**<br>Instructs the load balancer to respond directly as configured. <br>`http` includes only one of the fields `route`, `redirect`, `directResponse`<br>
http.<br>directResponse.<br>status | **string** (int64)<br><p>HTTP status code to use in responses.</p> <p>Acceptable values are 100 to 599, inclusive.</p> 
http.<br>directResponse.<br>body | **object**<br><p>Response body.</p> <p>A health check payload resource.</p> 
http.<br>directResponse.<br>body.<br>text | **string**<br><p>Payload text.</p> <p>The string length in characters must be greater than 0.</p> 
grpc | **object**<br>New settings of the gRPC route. <br> includes only one of the fields `http`, `grpc`<br>
grpc.<br>match | **object**<br>Condition (predicate) used to select the route.
grpc.<br>match.<br>fqmn | **object**<br><p>Match settings for gRPC service method called in the request.</p> <p>A match string must be a fully qualified method name, e.g. ``foo.bar.v1.BazService/Get``, or a prefix of such.</p> <p>If not specified, the route matches all methods.</p> <p>A string matcher resource.</p> 
grpc.<br>match.<br>fqmn.<br>exactMatch | **string** <br>`grpc.match.fqmn` includes only one of the fields `exactMatch`, `prefixMatch`<br><br><p>Exact match string.</p> 
grpc.<br>match.<br>fqmn.<br>prefixMatch | **string** <br>`grpc.match.fqmn` includes only one of the fields `exactMatch`, `prefixMatch`<br><br><p>Prefix match string.</p> 
grpc.<br>route | **object**<br>Forwards the request to a backend group for processing as configured. <br>`grpc` includes only one of the fields `route`, `statusResponse`<br>
grpc.<br>route.<br>backendGroupId | **string**<br><p>Required. Backend group to forward requests to.</p> 
grpc.<br>route.<br>maxTimeout | **string**<br><p>Overall timeout for an underlying HTTP connection between a load balancer node an a backend from the backend group: the maximum time the connection is kept alive for, regardless of whether data is transferred over it.</p> <p>If a client specifies a lower timeout in HTTP ``grpc-timeout`` header, the ``max_timeout`` value is ignored.</p> <p>If a connection times out, the load balancer responds to the client with an ``UNAVAILABLE`` status code.</p> <p>Default value: ``60``.</p> 
grpc.<br>route.<br>idleTimeout | **string**<br><p>Idle timeout for an underlying HTTP connection between a load balancer node an a backend from the backend group: the maximum time the connection is allowed to be idle, i.e. without any data transferred over it.</p> <p>Specifying meaningful values for both ``maxTimeout`` and ``idle_timeout`` is useful for implementing server-push mechanisms such as long polling, server-sent events etc.</p> <p>If a connection times out, the load balancer responds to the client with an ``UNAVAILABLE`` status code.</p> <p>If not specified, no idle timeout is used, and an alive connection may be idle for any duration (see ``maxTimeout``).</p> 
grpc.<br>route.<br>hostRewrite | **string** <br>`grpc.route` includes only one of the fields `hostRewrite`, `autoHostRewrite`<br><br><p>Host replacement.</p> 
grpc.<br>route.<br>autoHostRewrite | **boolean** (boolean) <br>`grpc.route` includes only one of the fields `hostRewrite`, `autoHostRewrite`<br><br><p>Automatically replaces the host with that of the target.</p> 
grpc.<br>statusResponse | **object**<br>Instructs the load balancer to respond directly with a specified status. <br>`grpc` includes only one of the fields `route`, `statusResponse`<br>
grpc.<br>statusResponse.<br>status | **string**<br><p>gRPC <a href="https://grpc.github.io/grpc/core/md_doc_statuscodes.html">status code</a> to use in responses.</p> <p>gRPC status code supported for use in responses.</p> <ul> <li>OK: ``OK`` (0) status code.</li> <li>INVALID_ARGUMENT: ``INVALID_ARGUMENT`` (3) status code.</li> <li>NOT_FOUND: ``NOT_FOUND`` (5) status code.</li> <li>PERMISSION_DENIED: ``PERMISSION_DENIED`` (7) status code.</li> <li>UNAUTHENTICATED: ``UNAUTHENTICATED`` (16) status code.</li> <li>UNIMPLEMENTED: ``UNIMPLEMENTED`` (12) status code.</li> <li>INTERNAL: ``INTERNAL`` (13) status code.</li> <li>UNAVAILABLE: ``UNAVAILABLE`` (14) status code.</li> </ul> 
 
## Response {#responses}
**HTTP Code: 200 - OK**

```json 
{
  "id": "string",
  "description": "string",
  "createdAt": "string",
  "createdBy": "string",
  "modifiedAt": "string",
  "done": true,
  "metadata": "object",

  //  includes only one of the fields `error`, `response`
  "error": {
    "code": "integer",
    "message": "string",
    "details": [
      "object"
    ]
  },
  "response": "object",
  // end of the list of possible fields

}
```
An Operation resource. For more information, see [Operation](/docs/api-design-guide/concepts/operation).
 
Field | Description
--- | ---
id | **string**<br><p>ID of the operation.</p> 
description | **string**<br><p>Description of the operation. 0-256 characters long.</p> 
createdAt | **string** (date-time)<br><p>Creation timestamp.</p> <p>String in <a href="https://www.ietf.org/rfc/rfc3339.txt">RFC3339</a> text format.</p> 
createdBy | **string**<br><p>ID of the user or service account who initiated the operation.</p> 
modifiedAt | **string** (date-time)<br><p>The time when the Operation resource was last modified.</p> <p>String in <a href="https://www.ietf.org/rfc/rfc3339.txt">RFC3339</a> text format.</p> 
done | **boolean** (boolean)<br><p>If the value is ``false``, it means the operation is still in progress. If ``true``, the operation is completed, and either ``error`` or ``response`` is available.</p> 
metadata | **object**<br><p>Service-specific metadata associated with the operation. It typically contains the ID of the target resource that the operation is performed on. Any method that returns a long-running operation should document the metadata type, if any.</p> 
error | **object**<br>The error result of the operation in case of failure or cancellation. <br> includes only one of the fields `error`, `response`<br>
error.<br>code | **integer** (int32)<br><p>Error code. An enum value of <a href="https://github.com/googleapis/googleapis/blob/master/google/rpc/code.proto">google.rpc.Code</a>.</p> 
error.<br>message | **string**<br><p>An error message.</p> 
error.<br>details[] | **object**<br><p>A list of messages that carry the error details.</p> 
response | **object** <br> includes only one of the fields `error`, `response`<br><br><p>The normal response of the operation in case of success. If the original method returns no data on success, such as Delete, the response is <a href="https://developers.google.com/protocol-buffers/docs/reference/google.protobuf#empty">google.protobuf.Empty</a>. If the original method is the standard Create/Update, the response should be the target resource of the operation. Any method that returns a long-running operation should document the response type, if any.</p> 