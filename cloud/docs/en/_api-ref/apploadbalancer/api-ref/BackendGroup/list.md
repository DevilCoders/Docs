---
editable: false
---

# Method list
Lists backend groups in the specified folder.
 

 
## HTTP request {#https-request}
```
GET https://alb.{{ api-host }}/apploadbalancer/v1/backendGroups
```
 
## Query parameters {#query_params}
 
Parameter | Description
--- | ---
folderId | <p>Required. ID of the folder to list backend groups in.</p> <p>To get the folder ID, make a <a href="/docs/resource-manager/api-ref/Folder/list">list</a> request.</p> 
pageSize | <p>The maximum number of results per page to return. If the number of available results is larger than ``page_size``, the service returns a <a href="/docs/application-load-balancer/api-ref/BackendGroup/list#responses">nextPageToken</a> that can be used to get the next page of results in subsequent list requests. Default value: 100.</p> <p>Acceptable values are 0 to 1000, inclusive.</p> 
pageToken | <p>Page token. To get the next page of results, set ``page_token`` to the <a href="/docs/application-load-balancer/api-ref/BackendGroup/list#responses">nextPageToken</a> returned by a previous list request.</p> <p>The maximum string length in characters is 100.</p> 
filter | <p>A filter expression that filters backend groups listed in the response.</p> <p>The expression must specify:</p> <ol> <li>The field name. Currently you can use filtering only on <a href="/docs/application-load-balancer/api-ref/BackendGroup#representation">BackendGroup.name</a> field.</li> <li>An ``=`` operator.</li> <li>The value in double quotes (``"``). Must be 3-63 characters long and match the regular expression ``[a-z][-a-z0-9]{1,61}[a-z0-9]``. Example of a filter: ``name=my-backend-group``.</li> </ol> <p>The maximum string length in characters is 1000.</p> 
 
## Response {#responses}
**HTTP Code: 200 - OK**

```json 
{
  "backendGroups": [
    {
      "id": "string",
      "name": "string",
      "description": "string",
      "folderId": "string",
      "labels": "object",
      "createdAt": "string",

      // `backendGroups[]` includes only one of the fields `http`, `grpc`, `stream`
      "http": {
        "backends": [
          {
            "name": "string",
            "backendWeight": "integer",
            "loadBalancingConfig": {
              "panicThreshold": "string",
              "localityAwareRoutingPercent": "string",
              "strictLocality": true,
              "mode": "string"
            },
            "port": "string",
            "healthchecks": [
              {
                "timeout": "string",
                "interval": "string",
                "intervalJitterPercent": "number",
                "healthyThreshold": "string",
                "unhealthyThreshold": "string",
                "healthcheckPort": "string",

                // `backendGroups[].http.backends[].healthchecks[]` includes only one of the fields `plaintext`, `tls`
                "stream": {
                  "send": {
                    "text": "string"
                  },
                  "receive": {
                    "text": "string"
                  }
                },
                "http": {
                  "host": "string",
                  "path": "string",
                  "useHttp2": true
                },
                "grpc": {
                  "serviceName": "string"
                },
                // end of the list of possible fields`backendGroups[].http.backends[].healthchecks[]`

                "plaintext": {},
                "tls": {
                  "sni": "string",
                  "validationContext": {

                    // `backendGroups[].http.backends[].healthchecks[].tls.validationContext` includes only one of the fields `trustedCaId`, `trustedCaBytes`
                    "trustedCaId": "string",
                    "trustedCaBytes": "string",
                    // end of the list of possible fields`backendGroups[].http.backends[].healthchecks[].tls.validationContext`

                  }
                }
              }
            ],
            "tls": {
              "sni": "string",
              "validationContext": {

                // `backendGroups[].http.backends[].tls.validationContext` includes only one of the fields `trustedCaId`, `trustedCaBytes`
                "trustedCaId": "string",
                "trustedCaBytes": "string",
                // end of the list of possible fields`backendGroups[].http.backends[].tls.validationContext`

              }
            },
            "useHttp2": true,

            // `backendGroups[].http.backends[]` includes only one of the fields `targetGroups`, `storageBucket`
            "targetGroups": {
              "targetGroupIds": [
                "string"
              ]
            },
            "storageBucket": {
              "bucket": "string"
            },
            // end of the list of possible fields`backendGroups[].http.backends[]`

          }
        ],

        // `backendGroups[].http` includes only one of the fields `connection`, `header`, `cookie`
        "connection": {
          "sourceIp": true
        },
        "header": {
          "headerName": "string"
        },
        "cookie": {
          "name": "string",
          "ttl": "string"
        },
        // end of the list of possible fields`backendGroups[].http`

      },
      "grpc": {
        "backends": [
          {
            "name": "string",
            "backendWeight": "integer",
            "loadBalancingConfig": {
              "panicThreshold": "string",
              "localityAwareRoutingPercent": "string",
              "strictLocality": true,
              "mode": "string"
            },
            "port": "string",
            "healthchecks": [
              {
                "timeout": "string",
                "interval": "string",
                "intervalJitterPercent": "number",
                "healthyThreshold": "string",
                "unhealthyThreshold": "string",
                "healthcheckPort": "string",

                // `backendGroups[].grpc.backends[].healthchecks[]` includes only one of the fields `plaintext`, `tls`
                "stream": {
                  "send": {
                    "text": "string"
                  },
                  "receive": {
                    "text": "string"
                  }
                },
                "http": {
                  "host": "string",
                  "path": "string",
                  "useHttp2": true
                },
                "grpc": {
                  "serviceName": "string"
                },
                // end of the list of possible fields`backendGroups[].grpc.backends[].healthchecks[]`

                "plaintext": {},
                "tls": {
                  "sni": "string",
                  "validationContext": {

                    // `backendGroups[].grpc.backends[].healthchecks[].tls.validationContext` includes only one of the fields `trustedCaId`, `trustedCaBytes`
                    "trustedCaId": "string",
                    "trustedCaBytes": "string",
                    // end of the list of possible fields`backendGroups[].grpc.backends[].healthchecks[].tls.validationContext`

                  }
                }
              }
            ],
            "tls": {
              "sni": "string",
              "validationContext": {

                // `backendGroups[].grpc.backends[].tls.validationContext` includes only one of the fields `trustedCaId`, `trustedCaBytes`
                "trustedCaId": "string",
                "trustedCaBytes": "string",
                // end of the list of possible fields`backendGroups[].grpc.backends[].tls.validationContext`

              }
            },
            "targetGroups": {
              "targetGroupIds": [
                "string"
              ]
            }
          }
        ],

        // `backendGroups[].grpc` includes only one of the fields `connection`, `header`, `cookie`
        "connection": {
          "sourceIp": true
        },
        "header": {
          "headerName": "string"
        },
        "cookie": {
          "name": "string",
          "ttl": "string"
        },
        // end of the list of possible fields`backendGroups[].grpc`

      },
      "stream": {
        "backends": [
          {
            "name": "string",
            "backendWeight": "integer",
            "loadBalancingConfig": {
              "panicThreshold": "string",
              "localityAwareRoutingPercent": "string",
              "strictLocality": true,
              "mode": "string"
            },
            "port": "string",
            "healthchecks": [
              {
                "timeout": "string",
                "interval": "string",
                "intervalJitterPercent": "number",
                "healthyThreshold": "string",
                "unhealthyThreshold": "string",
                "healthcheckPort": "string",

                // `backendGroups[].stream.backends[].healthchecks[]` includes only one of the fields `plaintext`, `tls`
                "stream": {
                  "send": {
                    "text": "string"
                  },
                  "receive": {
                    "text": "string"
                  }
                },
                "http": {
                  "host": "string",
                  "path": "string",
                  "useHttp2": true
                },
                "grpc": {
                  "serviceName": "string"
                },
                // end of the list of possible fields`backendGroups[].stream.backends[].healthchecks[]`

                "plaintext": {},
                "tls": {
                  "sni": "string",
                  "validationContext": {

                    // `backendGroups[].stream.backends[].healthchecks[].tls.validationContext` includes only one of the fields `trustedCaId`, `trustedCaBytes`
                    "trustedCaId": "string",
                    "trustedCaBytes": "string",
                    // end of the list of possible fields`backendGroups[].stream.backends[].healthchecks[].tls.validationContext`

                  }
                }
              }
            ],
            "tls": {
              "sni": "string",
              "validationContext": {

                // `backendGroups[].stream.backends[].tls.validationContext` includes only one of the fields `trustedCaId`, `trustedCaBytes`
                "trustedCaId": "string",
                "trustedCaBytes": "string",
                // end of the list of possible fields`backendGroups[].stream.backends[].tls.validationContext`

              }
            },
            "enableProxyProtocol": true,
            "targetGroups": {
              "targetGroupIds": [
                "string"
              ]
            }
          }
        ],
        "connection": {
          "sourceIp": true
        }
      },
      // end of the list of possible fields`backendGroups[]`

    }
  ],
  "nextPageToken": "string"
}
```

 
Field | Description
--- | ---
backendGroups[] | **object**<br><p>List of backend groups in the specified folder.</p> 
backendGroups[].<br>id | **string**<br><p>ID of the backend group. Generated at creation time.</p> 
backendGroups[].<br>name | **string**<br><p>Name of the backend group. The name is unique within the folder. The string length in characters is 3-63.</p> 
backendGroups[].<br>description | **string**<br><p>Description of the backend group. The string is 0-256 characters long.</p> 
backendGroups[].<br>folderId | **string**<br><p>ID of the folder that the backend group belongs to.</p> 
backendGroups[].<br>labels | **object**<br><p>Backend group labels as ``key:value`` pairs. For details about the concept, see <a href="/docs/overview/concepts/services#labels">documentation</a>. The maximum number of labels is 64.</p> 
backendGroups[].<br>createdAt | **string** (date-time)<br><p>Creation timestamp.</p> <p>String in <a href="https://www.ietf.org/rfc/rfc3339.txt">RFC3339</a> text format.</p> 
backendGroups[].<br>http | **object**<br>List of HTTP backends that the backend group consists of. <br>`backendGroups[]` includes only one of the fields `http`, `grpc`, `stream`<br>
backendGroups[].<br>http.<br>backends[] | **object**<br>HTTP backend to add to the backend group.
backendGroups[].<br>http.<br>backends[].<br>name | **string**<br><p>Required. Name of the backend.</p> <p>Value must match the regular expression ``[a-z][-a-z0-9]{1,61}[a-z0-9]``.</p> 
backendGroups[].<br>http.<br>backends[].<br>backendWeight | **integer** (int64)<br><p>Backend weight. Traffic is distributed between backends of a backend group according to their weights.</p> <p>Weights must be set either for all backends in a group or for none of them. Setting no weights is the same as setting equal non-zero weights for all backends.</p> <p>If the weight is non-positive, traffic is not sent to the backend.</p> 
backendGroups[].<br>http.<br>backends[].<br>loadBalancingConfig | **object**<br>Load balancing configuration for the backend.
backendGroups[].<br>http.<br>backends[].<br>loadBalancingConfig.<br>panicThreshold | **string** (int64)<br><p>Threshold for panic mode.</p> <p>If percentage of healthy backends in the group drops below threshold, panic mode will be activated and traffic will be routed to all backends, regardless of their health check status. This helps to avoid overloading healthy backends. For details about panic mode, see <a href="/docs/application-load-balancer/concepts/backend-group#panic-mode">documentation</a>.</p> <p>If the value is ``0``, panic mode will never be activated and traffic is routed only to healthy backends at all times.</p> <p>Default value: ``0``.</p> <p>Acceptable values are 0 to 100, inclusive.</p> 
backendGroups[].<br>http.<br>backends[].<br>loadBalancingConfig.<br>localityAwareRoutingPercent | **string** (int64)<br><p>Percentage of traffic that a load balancer node sends to healthy backends in its availability zone. The rest is divided equally between other zones. For details about zone-aware routing, see <a href="/docs/application-load-balancer/concepts/backend-group#locality">documentation</a>.</p> <p>If there are no healthy backends in an availability zone, all the traffic is divided between other zones.</p> <p>If ``strictLocality`` is ``true``, the specified value is ignored. A load balancer node sends all the traffic within its availability zone, regardless of backends' health.</p> <p>Default value: ``0``.</p> <p>Acceptable values are 0 to 100, inclusive.</p> 
backendGroups[].<br>http.<br>backends[].<br>loadBalancingConfig.<br>strictLocality | **boolean** (boolean)<br><p>Specifies whether a load balancer node should only send traffic to backends in its availability zone, regardless of their health, and ignore backends in other zones.</p> <p>If set to ``true`` and there are no healthy backends in the zone, the node in this zone will respond to incoming traffic with errors. For details about strict locality, see <a href="/docs/application-load-balancer/concepts/backend-group#locality">documentation</a>.</p> <p>If ``strict_locality`` is ``true``, the value specified in ``localityAwareRoutingPercent`` is ignored.</p> <p>Default value: ``false``.</p> 
backendGroups[].<br>http.<br>backends[].<br>loadBalancingConfig.<br>mode | **string**<br><p>Load balancing mode for the backend.</p> <p>For details about load balancing modes, see <a href="/docs/application-load-balancer/concepts/backend-group#balancing-mode">documentation</a>.</p> <p>A load balancing mode resource. For details about the concept, see <a href="/docs/application-load-balancer/concepts/backend-group#balancing-mode">documentation</a>.</p> <ul> <li> <p>ROUND_ROBIN: Round robin load balancing mode.</p> <p>All endpoints of the backend take their turns to receive requests attributed to the backend.</p> </li> <li> <p>RANDOM: Random load balancing mode. Default value.</p> <p>For a request attributed to the backend, an endpoint that receives it is picked at random.</p> </li> <li> <p>LEAST_REQUEST: Least request load balancing mode.</p> <p>To pick an endpoint that receives a request attributed to the backend, the power of two choices algorithm is used; that is, two endpoints are picked at random, and the request is sent to the one which has the fewest active requests.</p> </li> <li> <p>MAGLEV_HASH: Maglev hashing load balancing mode.</p> <p>Each endpoint is hashed, and a hash table with 65537 rows is filled accordingly, so that every endpoint occupies the same amount of rows. An attribute of each request is also hashed by the same function (if session affinity is enabled for the backend group, the attribute to hash is specified in session affinity configuration). The row with the same number as the resulting value is looked up in the table to determine the endpoint that receives the request.</p> <p>If the backend group with session affinity enabled contains more than one backend with positive weight, endpoints for backends with ``MAGLEV_HASH`` load balancing mode are picked at ``RANDOM`` instead.</p> </li> </ul> 
backendGroups[].<br>http.<br>backends[].<br>port | **string** (int64)<br><p>Port used by all targets to receive traffic.</p> <p>Acceptable values are 0 to 65535, inclusive.</p> 
backendGroups[].<br>http.<br>backends[].<br>healthchecks[] | **object**<br><p>Health checks to perform on targets from target groups. For details about health checking, see <a href="/docs/application-load-balancer/concepts/backend-group#health-checks">documentation</a>.</p> <p>If no health checks are specified, active health checking is not performed.</p> 
backendGroups[].<br>http.<br>backends[].<br>healthchecks[].<br>timeout | **string**<br><p>Required. Health check timeout.</p> <p>The timeout is the time allowed for the target to respond to a check. If the target doesn't respond in time, the check is considered failed.</p> 
backendGroups[].<br>http.<br>backends[].<br>healthchecks[].<br>interval | **string**<br><p>Required. Base interval between consecutive health checks.</p> 
backendGroups[].<br>http.<br>backends[].<br>healthchecks[].<br>intervalJitterPercent | **number** (double)
backendGroups[].<br>http.<br>backends[].<br>healthchecks[].<br>healthyThreshold | **string** (int64)<br><p>Number of consecutive successful health checks required to mark an unhealthy target as healthy.</p> <p>Both ``0`` and ``1`` values amount to one successful check required.</p> <p>The value is ignored when a load balancer is initialized; a target is marked healthy after one successful check.</p> <p>Default value: ``0``.</p> 
backendGroups[].<br>http.<br>backends[].<br>healthchecks[].<br>unhealthyThreshold | **string** (int64)<br><p>Number of consecutive failed health checks required to mark a healthy target as unhealthy.</p> <p>Both ``0`` and ``1`` values amount to one unsuccessful check required.</p> <p>The value is ignored if a health check is failed due to an HTTP ``503 Service Unavailable`` response from the target (not applicable to TCP stream health checks). The target is immediately marked unhealthy.</p> <p>Default value: ``0``.</p> 
backendGroups[].<br>http.<br>backends[].<br>healthchecks[].<br>healthcheckPort | **string** (int64)<br><p>Port used for health checks.</p> <p>If not specified, the backend port (``port`` or ``port``) is used for health checks.</p> <p>Acceptable values are 0 to 65535, inclusive.</p> 
backendGroups[].<br>http.<br>backends[].<br>healthchecks[].<br>stream | **object**<br>TCP stream health check settings. <br>`backendGroups[].http.backends[].healthchecks[]` includes only one of the fields `stream`, `http`, `grpc`<br>
backendGroups[].<br>http.<br>backends[].<br>healthchecks[].<br>stream.<br>send | **object**<br><p>Message sent to targets during TCP data transfer.</p> <p>If not specified, no data is sent to the target.</p> <p>A health check payload resource.</p> 
backendGroups[].<br>http.<br>backends[].<br>healthchecks[].<br>stream.<br>send.<br>text | **string**<br><p>Payload text.</p> <p>The string length in characters must be greater than 0.</p> 
backendGroups[].<br>http.<br>backends[].<br>healthchecks[].<br>stream.<br>receive | **object**<br><p>Data that must be contained in the messages received from targets for a successful health check.</p> <p>If not specified, no messages are expected from targets, and those that are received are not checked.</p> <p>A health check payload resource.</p> 
backendGroups[].<br>http.<br>backends[].<br>healthchecks[].<br>stream.<br>receive.<br>text | **string**<br><p>Payload text.</p> <p>The string length in characters must be greater than 0.</p> 
backendGroups[].<br>http.<br>backends[].<br>healthchecks[].<br>http | **object**<br>HTTP health check settings. <br>`backendGroups[].http.backends[].healthchecks[]` includes only one of the fields `stream`, `http`, `grpc`<br>
backendGroups[].<br>http.<br>backends[].<br>healthchecks[].<br>http.<br>host | **string**<br><p>Value for the HTTP/1.1 ``Host`` header or the HTTP/2 ``:authority`` pseudo-header used in requests to targets.</p> 
backendGroups[].<br>http.<br>backends[].<br>healthchecks[].<br>http.<br>path | **string**<br><p>Required. HTTP path used in requests to targets: request URI for HTTP/1.1 request line or value for the HTTP/2 ``:path`` pseudo-header.</p> 
backendGroups[].<br>http.<br>backends[].<br>healthchecks[].<br>http.<br>useHttp2 | **boolean** (boolean)<br><p>Enables HTTP/2 usage in health checks.</p> <p>Default value: ``false``, HTTP/1.1 is used.</p> 
backendGroups[].<br>http.<br>backends[].<br>healthchecks[].<br>grpc | **object**<br>gRPC health check settings. <br>`backendGroups[].http.backends[].healthchecks[]` includes only one of the fields `stream`, `http`, `grpc`<br>
backendGroups[].<br>http.<br>backends[].<br>healthchecks[].<br>grpc.<br>serviceName | **string**<br><p>Name of the gRPC service to be checked.</p> <p>If not specified, overall health is checked.</p> <p>For details about the concept, see <a href="https://github.com/grpc/grpc/blob/master/doc/health-checking.md">GRPC Health Checking Protocol</a>.</p> 
backendGroups[].<br>http.<br>backends[].<br>healthchecks[].<br>plaintext | **object** <br>`backendGroups[].http.backends[].healthchecks[]` includes only one of the fields `plaintext`, `tls`<br><br><p>Transport settings to be used instead of the settings configured per-cluster</p> 
backendGroups[].<br>http.<br>backends[].<br>healthchecks[].<br>tls | **object** <br>`backendGroups[].http.backends[].healthchecks[]` includes only one of the fields `plaintext`, `tls`<br><br><p>Transport settings to be used instead of the settings configured per-cluster</p> 
backendGroups[].<br>http.<br>backends[].<br>healthchecks[].<br>tls.<br>sni | **string**<br><p>SNI string for TLS connections.</p> 
backendGroups[].<br>http.<br>backends[].<br>healthchecks[].<br>tls.<br>validationContext | **object**<br><p>Validation context for backend TLS connections.</p> <p>A TLS validation context resource.</p> 
backendGroups[].<br>http.<br>backends[].<br>healthchecks[].<br>tls.<br>validationContext.<br>trustedCaId | **string** <br>`backendGroups[].http.backends[].healthchecks[].tls.validationContext` includes only one of the fields `trustedCaId`, `trustedCaBytes`<br>
backendGroups[].<br>http.<br>backends[].<br>healthchecks[].<br>tls.<br>validationContext.<br>trustedCaBytes | **string** <br>`backendGroups[].http.backends[].healthchecks[].tls.validationContext` includes only one of the fields `trustedCaId`, `trustedCaBytes`<br><br><p>X.509 certificate contents in PEM format.</p> 
backendGroups[].<br>http.<br>backends[].<br>tls | **object**<br>Settings for TLS connections between load balancer nodes and backend targets.  If specified, the load balancer establishes TLS-encrypted TCP connections with targets and compares received certificates with the one specified in `validationContext`. If not specified, the load balancer establishes unencrypted TCP connections with targets.
backendGroups[].<br>http.<br>backends[].<br>tls.<br>sni | **string**<br><p>Server Name Indication (SNI) string for TLS connections.</p> 
backendGroups[].<br>http.<br>backends[].<br>tls.<br>validationContext | **object**<br><p>Validation context for TLS connections.</p> <p>A TLS validation context resource.</p> 
backendGroups[].<br>http.<br>backends[].<br>tls.<br>validationContext.<br>trustedCaId | **string** <br>`backendGroups[].http.backends[].tls.validationContext` includes only one of the fields `trustedCaId`, `trustedCaBytes`<br>
backendGroups[].<br>http.<br>backends[].<br>tls.<br>validationContext.<br>trustedCaBytes | **string** <br>`backendGroups[].http.backends[].tls.validationContext` includes only one of the fields `trustedCaId`, `trustedCaBytes`<br><br><p>X.509 certificate contents in PEM format.</p> 
backendGroups[].<br>http.<br>backends[].<br>useHttp2 | **boolean** (boolean)<br><p>Enables HTTP/2 usage in connections between load balancer nodes and backend targets.</p> <p>Default value: ``false``, HTTP/1.1 is used.</p> 
backendGroups[].<br>http.<br>backends[].<br>targetGroups | **object**<br>Target groups that belong to the backend. For details about target groups, see [documentation](/docs/application-load-balancer/concepts/target-group). <br>`backendGroups[].http.backends[]` includes only one of the fields `targetGroups`, `storageBucket`<br>
backendGroups[].<br>http.<br>backends[].<br>targetGroups.<br>targetGroupIds[] | **string**<br><p>Required. List of ID's of target groups that belong to the backend.</p> <p>To get the ID's of all available target groups, make a <a href="/docs/application-load-balancer/api-ref/TargetGroup/list">list</a> request.</p> <p>Must contain at least one element.</p> 
backendGroups[].<br>http.<br>backends[].<br>storageBucket | **object**<br>Object Storage bucket to use as the backend. For details about buckets, see [documentation](/docs/storage/concepts/bucket).  If a bucket is used as a backend, the list of bucket objects and the objects themselves must be publicly accessible. For instructions, see [documentation](/docs/storage/operations/buckets/bucket-availability). <br>`backendGroups[].http.backends[]` includes only one of the fields `targetGroups`, `storageBucket`<br>
backendGroups[].<br>http.<br>backends[].<br>storageBucket.<br>bucket | **string**<br><p>Required. Name of the bucket.</p> 
backendGroups[].<br>http.<br>connection | **object**<br>Connection-based session affinity configuration.  For now, a connection is defined only by an IP address of the client. <br>`backendGroups[].http` includes only one of the fields `connection`, `header`, `cookie`<br>
backendGroups[].<br>http.<br>connection.<br>sourceIp | **boolean** (boolean)<br><p>Specifies whether an IP address of the client is used to define a connection for session affinity.</p> 
backendGroups[].<br>http.<br>header | **object**<br>HTTP-header-field-based session affinity configuration. <br>`backendGroups[].http` includes only one of the fields `connection`, `header`, `cookie`<br>
backendGroups[].<br>http.<br>header.<br>headerName | **string**<br><p>Name of the HTTP header field that is used for session affinity.</p> <p>The string length in characters must be 1-256.</p> 
backendGroups[].<br>http.<br>cookie | **object**<br>Cookie-based session affinity configuration. <br>`backendGroups[].http` includes only one of the fields `connection`, `header`, `cookie`<br>
backendGroups[].<br>http.<br>cookie.<br>name | **string**<br><p>Name of the cookie that is used for session affinity.</p> <p>The string length in characters must be 1-256.</p> 
backendGroups[].<br>http.<br>cookie.<br>ttl | **string**<br><p>Maximum age of cookies that are generated for sessions.</p> <p>If set to ``0``, session cookies are used, which are stored by clients in temporary memory and are deleted on client restarts.</p> <p>If not set, the balancer does not generate cookies and only uses incoming ones for establishing session affinity.</p> 
backendGroups[].<br>grpc | **object**<br>List of gRPC backends that the backend group consists of. <br>`backendGroups[]` includes only one of the fields `http`, `grpc`, `stream`<br>
backendGroups[].<br>grpc.<br>backends[] | **object**<br>gRPC backend to add to the backend group.
backendGroups[].<br>grpc.<br>backends[].<br>name | **string**<br><p>Required. Name of the backend.</p> <p>Value must match the regular expression ``[a-z][-a-z0-9]{1,61}[a-z0-9]``.</p> 
backendGroups[].<br>grpc.<br>backends[].<br>backendWeight | **integer** (int64)<br><p>Backend weight. Traffic is distributed between backends of a backend group according to their weights.</p> <p>Weights must be set either for all backends of a group or for none of them. Setting no weights is the same as setting equal non-zero weights for all backends.</p> <p>If the weight is non-positive, traffic is not sent to the backend.</p> 
backendGroups[].<br>grpc.<br>backends[].<br>loadBalancingConfig | **object**<br>Load balancing configuration for the backend.
backendGroups[].<br>grpc.<br>backends[].<br>loadBalancingConfig.<br>panicThreshold | **string** (int64)<br><p>Threshold for panic mode.</p> <p>If percentage of healthy backends in the group drops below threshold, panic mode will be activated and traffic will be routed to all backends, regardless of their health check status. This helps to avoid overloading healthy backends. For details about panic mode, see <a href="/docs/application-load-balancer/concepts/backend-group#panic-mode">documentation</a>.</p> <p>If the value is ``0``, panic mode will never be activated and traffic is routed only to healthy backends at all times.</p> <p>Default value: ``0``.</p> <p>Acceptable values are 0 to 100, inclusive.</p> 
backendGroups[].<br>grpc.<br>backends[].<br>loadBalancingConfig.<br>localityAwareRoutingPercent | **string** (int64)<br><p>Percentage of traffic that a load balancer node sends to healthy backends in its availability zone. The rest is divided equally between other zones. For details about zone-aware routing, see <a href="/docs/application-load-balancer/concepts/backend-group#locality">documentation</a>.</p> <p>If there are no healthy backends in an availability zone, all the traffic is divided between other zones.</p> <p>If ``strictLocality`` is ``true``, the specified value is ignored. A load balancer node sends all the traffic within its availability zone, regardless of backends' health.</p> <p>Default value: ``0``.</p> <p>Acceptable values are 0 to 100, inclusive.</p> 
backendGroups[].<br>grpc.<br>backends[].<br>loadBalancingConfig.<br>strictLocality | **boolean** (boolean)<br><p>Specifies whether a load balancer node should only send traffic to backends in its availability zone, regardless of their health, and ignore backends in other zones.</p> <p>If set to ``true`` and there are no healthy backends in the zone, the node in this zone will respond to incoming traffic with errors. For details about strict locality, see <a href="/docs/application-load-balancer/concepts/backend-group#locality">documentation</a>.</p> <p>If ``strict_locality`` is ``true``, the value specified in ``localityAwareRoutingPercent`` is ignored.</p> <p>Default value: ``false``.</p> 
backendGroups[].<br>grpc.<br>backends[].<br>loadBalancingConfig.<br>mode | **string**<br><p>Load balancing mode for the backend.</p> <p>For details about load balancing modes, see <a href="/docs/application-load-balancer/concepts/backend-group#balancing-mode">documentation</a>.</p> <p>A load balancing mode resource. For details about the concept, see <a href="/docs/application-load-balancer/concepts/backend-group#balancing-mode">documentation</a>.</p> <ul> <li> <p>ROUND_ROBIN: Round robin load balancing mode.</p> <p>All endpoints of the backend take their turns to receive requests attributed to the backend.</p> </li> <li> <p>RANDOM: Random load balancing mode. Default value.</p> <p>For a request attributed to the backend, an endpoint that receives it is picked at random.</p> </li> <li> <p>LEAST_REQUEST: Least request load balancing mode.</p> <p>To pick an endpoint that receives a request attributed to the backend, the power of two choices algorithm is used; that is, two endpoints are picked at random, and the request is sent to the one which has the fewest active requests.</p> </li> <li> <p>MAGLEV_HASH: Maglev hashing load balancing mode.</p> <p>Each endpoint is hashed, and a hash table with 65537 rows is filled accordingly, so that every endpoint occupies the same amount of rows. An attribute of each request is also hashed by the same function (if session affinity is enabled for the backend group, the attribute to hash is specified in session affinity configuration). The row with the same number as the resulting value is looked up in the table to determine the endpoint that receives the request.</p> <p>If the backend group with session affinity enabled contains more than one backend with positive weight, endpoints for backends with ``MAGLEV_HASH`` load balancing mode are picked at ``RANDOM`` instead.</p> </li> </ul> 
backendGroups[].<br>grpc.<br>backends[].<br>port | **string** (int64)<br><p>Port used by all targets to receive traffic.</p> <p>Acceptable values are 0 to 65535, inclusive.</p> 
backendGroups[].<br>grpc.<br>backends[].<br>healthchecks[] | **object**<br><p>Health checks to perform on targets from target groups. For details about health checking, see <a href="/docs/application-load-balancer/concepts/backend-group#health-checks">documentation</a>.</p> <p>If no health checks are specified, active health checking is not performed.</p> 
backendGroups[].<br>grpc.<br>backends[].<br>healthchecks[].<br>timeout | **string**<br><p>Required. Health check timeout.</p> <p>The timeout is the time allowed for the target to respond to a check. If the target doesn't respond in time, the check is considered failed.</p> 
backendGroups[].<br>grpc.<br>backends[].<br>healthchecks[].<br>interval | **string**<br><p>Required. Base interval between consecutive health checks.</p> 
backendGroups[].<br>grpc.<br>backends[].<br>healthchecks[].<br>intervalJitterPercent | **number** (double)
backendGroups[].<br>grpc.<br>backends[].<br>healthchecks[].<br>healthyThreshold | **string** (int64)<br><p>Number of consecutive successful health checks required to mark an unhealthy target as healthy.</p> <p>Both ``0`` and ``1`` values amount to one successful check required.</p> <p>The value is ignored when a load balancer is initialized; a target is marked healthy after one successful check.</p> <p>Default value: ``0``.</p> 
backendGroups[].<br>grpc.<br>backends[].<br>healthchecks[].<br>unhealthyThreshold | **string** (int64)<br><p>Number of consecutive failed health checks required to mark a healthy target as unhealthy.</p> <p>Both ``0`` and ``1`` values amount to one unsuccessful check required.</p> <p>The value is ignored if a health check is failed due to an HTTP ``503 Service Unavailable`` response from the target (not applicable to TCP stream health checks). The target is immediately marked unhealthy.</p> <p>Default value: ``0``.</p> 
backendGroups[].<br>grpc.<br>backends[].<br>healthchecks[].<br>healthcheckPort | **string** (int64)<br><p>Port used for health checks.</p> <p>If not specified, the backend port (``port`` or ``port``) is used for health checks.</p> <p>Acceptable values are 0 to 65535, inclusive.</p> 
backendGroups[].<br>grpc.<br>backends[].<br>healthchecks[].<br>stream | **object**<br>TCP stream health check settings. <br>`backendGroups[].grpc.backends[].healthchecks[]` includes only one of the fields `stream`, `http`, `grpc`<br>
backendGroups[].<br>grpc.<br>backends[].<br>healthchecks[].<br>stream.<br>send | **object**<br><p>Message sent to targets during TCP data transfer.</p> <p>If not specified, no data is sent to the target.</p> <p>A health check payload resource.</p> 
backendGroups[].<br>grpc.<br>backends[].<br>healthchecks[].<br>stream.<br>send.<br>text | **string**<br><p>Payload text.</p> <p>The string length in characters must be greater than 0.</p> 
backendGroups[].<br>grpc.<br>backends[].<br>healthchecks[].<br>stream.<br>receive | **object**<br><p>Data that must be contained in the messages received from targets for a successful health check.</p> <p>If not specified, no messages are expected from targets, and those that are received are not checked.</p> <p>A health check payload resource.</p> 
backendGroups[].<br>grpc.<br>backends[].<br>healthchecks[].<br>stream.<br>receive.<br>text | **string**<br><p>Payload text.</p> <p>The string length in characters must be greater than 0.</p> 
backendGroups[].<br>grpc.<br>backends[].<br>healthchecks[].<br>http | **object**<br>HTTP health check settings. <br>`backendGroups[].grpc.backends[].healthchecks[]` includes only one of the fields `stream`, `http`, `grpc`<br>
backendGroups[].<br>grpc.<br>backends[].<br>healthchecks[].<br>http.<br>host | **string**<br><p>Value for the HTTP/1.1 ``Host`` header or the HTTP/2 ``:authority`` pseudo-header used in requests to targets.</p> 
backendGroups[].<br>grpc.<br>backends[].<br>healthchecks[].<br>http.<br>path | **string**<br><p>Required. HTTP path used in requests to targets: request URI for HTTP/1.1 request line or value for the HTTP/2 ``:path`` pseudo-header.</p> 
backendGroups[].<br>grpc.<br>backends[].<br>healthchecks[].<br>http.<br>useHttp2 | **boolean** (boolean)<br><p>Enables HTTP/2 usage in health checks.</p> <p>Default value: ``false``, HTTP/1.1 is used.</p> 
backendGroups[].<br>grpc.<br>backends[].<br>healthchecks[].<br>grpc | **object**<br>gRPC health check settings. <br>`backendGroups[].grpc.backends[].healthchecks[]` includes only one of the fields `stream`, `http`, `grpc`<br>
backendGroups[].<br>grpc.<br>backends[].<br>healthchecks[].<br>grpc.<br>serviceName | **string**<br><p>Name of the gRPC service to be checked.</p> <p>If not specified, overall health is checked.</p> <p>For details about the concept, see <a href="https://github.com/grpc/grpc/blob/master/doc/health-checking.md">GRPC Health Checking Protocol</a>.</p> 
backendGroups[].<br>grpc.<br>backends[].<br>healthchecks[].<br>plaintext | **object** <br>`backendGroups[].grpc.backends[].healthchecks[]` includes only one of the fields `plaintext`, `tls`<br><br><p>Transport settings to be used instead of the settings configured per-cluster</p> 
backendGroups[].<br>grpc.<br>backends[].<br>healthchecks[].<br>tls | **object** <br>`backendGroups[].grpc.backends[].healthchecks[]` includes only one of the fields `plaintext`, `tls`<br><br><p>Transport settings to be used instead of the settings configured per-cluster</p> 
backendGroups[].<br>grpc.<br>backends[].<br>healthchecks[].<br>tls.<br>sni | **string**<br><p>SNI string for TLS connections.</p> 
backendGroups[].<br>grpc.<br>backends[].<br>healthchecks[].<br>tls.<br>validationContext | **object**<br><p>Validation context for backend TLS connections.</p> <p>A TLS validation context resource.</p> 
backendGroups[].<br>grpc.<br>backends[].<br>healthchecks[].<br>tls.<br>validationContext.<br>trustedCaId | **string** <br>`backendGroups[].grpc.backends[].healthchecks[].tls.validationContext` includes only one of the fields `trustedCaId`, `trustedCaBytes`<br>
backendGroups[].<br>grpc.<br>backends[].<br>healthchecks[].<br>tls.<br>validationContext.<br>trustedCaBytes | **string** <br>`backendGroups[].grpc.backends[].healthchecks[].tls.validationContext` includes only one of the fields `trustedCaId`, `trustedCaBytes`<br><br><p>X.509 certificate contents in PEM format.</p> 
backendGroups[].<br>grpc.<br>backends[].<br>tls | **object**<br>Settings for TLS connections between load balancer nodes and backend targets.  If specified, the load balancer establishes HTTPS (HTTP over TLS) connections with targets and compares received certificates with the one specified in `validationContext`. If not specified, the load balancer establishes unencrypted HTTP connections with targets.
backendGroups[].<br>grpc.<br>backends[].<br>tls.<br>sni | **string**<br><p>Server Name Indication (SNI) string for TLS connections.</p> 
backendGroups[].<br>grpc.<br>backends[].<br>tls.<br>validationContext | **object**<br><p>Validation context for TLS connections.</p> <p>A TLS validation context resource.</p> 
backendGroups[].<br>grpc.<br>backends[].<br>tls.<br>validationContext.<br>trustedCaId | **string** <br>`backendGroups[].grpc.backends[].tls.validationContext` includes only one of the fields `trustedCaId`, `trustedCaBytes`<br>
backendGroups[].<br>grpc.<br>backends[].<br>tls.<br>validationContext.<br>trustedCaBytes | **string** <br>`backendGroups[].grpc.backends[].tls.validationContext` includes only one of the fields `trustedCaId`, `trustedCaBytes`<br><br><p>X.509 certificate contents in PEM format.</p> 
backendGroups[].<br>grpc.<br>backends[].<br>targetGroups | **object**<br>Target groups that belong to the backend. For details about target groups, see [documentation](/docs/application-load-balancer/concepts/target-group).
backendGroups[].<br>grpc.<br>backends[].<br>targetGroups.<br>targetGroupIds[] | **string**<br><p>Required. List of ID's of target groups that belong to the backend.</p> <p>To get the ID's of all available target groups, make a <a href="/docs/application-load-balancer/api-ref/TargetGroup/list">list</a> request.</p> <p>Must contain at least one element.</p> 
backendGroups[].<br>grpc.<br>connection | **object**<br>Connection-based session affinity configuration.  For now, a connection is defined only by an IP address of the client. <br>`backendGroups[].grpc` includes only one of the fields `connection`, `header`, `cookie`<br>
backendGroups[].<br>grpc.<br>connection.<br>sourceIp | **boolean** (boolean)<br><p>Specifies whether an IP address of the client is used to define a connection for session affinity.</p> 
backendGroups[].<br>grpc.<br>header | **object**<br>HTTP-header-field-based session affinity configuration. <br>`backendGroups[].grpc` includes only one of the fields `connection`, `header`, `cookie`<br>
backendGroups[].<br>grpc.<br>header.<br>headerName | **string**<br><p>Name of the HTTP header field that is used for session affinity.</p> <p>The string length in characters must be 1-256.</p> 
backendGroups[].<br>grpc.<br>cookie | **object**<br>Cookie-based session affinity configuration. <br>`backendGroups[].grpc` includes only one of the fields `connection`, `header`, `cookie`<br>
backendGroups[].<br>grpc.<br>cookie.<br>name | **string**<br><p>Name of the cookie that is used for session affinity.</p> <p>The string length in characters must be 1-256.</p> 
backendGroups[].<br>grpc.<br>cookie.<br>ttl | **string**<br><p>Maximum age of cookies that are generated for sessions.</p> <p>If set to ``0``, session cookies are used, which are stored by clients in temporary memory and are deleted on client restarts.</p> <p>If not set, the balancer does not generate cookies and only uses incoming ones for establishing session affinity.</p> 
backendGroups[].<br>stream | **object**<br>List of stream (TCP) backends that the backend group consists of. <br>`backendGroups[]` includes only one of the fields `http`, `grpc`, `stream`<br>
backendGroups[].<br>stream.<br>backends[] | **object**<br>New settings for the Stream backend.
backendGroups[].<br>stream.<br>backends[].<br>name | **string**<br><p>Name of the backend.</p> <p>Value must match the regular expression ``[a-z][-a-z0-9]{1,61}[a-z0-9]``.</p> 
backendGroups[].<br>stream.<br>backends[].<br>backendWeight | **integer** (int64)<br><p>Backend weight. Traffic is distributed between backends of a backend group according to their weights.</p> <p>Weights must be set either for all backends in a group or for none of them. Setting no weights is the same as setting equal non-zero weights for all backends.</p> <p>If the weight is non-positive, traffic is not sent to the backend.</p> 
backendGroups[].<br>stream.<br>backends[].<br>loadBalancingConfig | **object**<br>Load balancing configuration for the backend.
backendGroups[].<br>stream.<br>backends[].<br>loadBalancingConfig.<br>panicThreshold | **string** (int64)<br><p>Threshold for panic mode.</p> <p>If percentage of healthy backends in the group drops below threshold, panic mode will be activated and traffic will be routed to all backends, regardless of their health check status. This helps to avoid overloading healthy backends. For details about panic mode, see <a href="/docs/application-load-balancer/concepts/backend-group#panic-mode">documentation</a>.</p> <p>If the value is ``0``, panic mode will never be activated and traffic is routed only to healthy backends at all times.</p> <p>Default value: ``0``.</p> <p>Acceptable values are 0 to 100, inclusive.</p> 
backendGroups[].<br>stream.<br>backends[].<br>loadBalancingConfig.<br>localityAwareRoutingPercent | **string** (int64)<br><p>Percentage of traffic that a load balancer node sends to healthy backends in its availability zone. The rest is divided equally between other zones. For details about zone-aware routing, see <a href="/docs/application-load-balancer/concepts/backend-group#locality">documentation</a>.</p> <p>If there are no healthy backends in an availability zone, all the traffic is divided between other zones.</p> <p>If ``strictLocality`` is ``true``, the specified value is ignored. A load balancer node sends all the traffic within its availability zone, regardless of backends' health.</p> <p>Default value: ``0``.</p> <p>Acceptable values are 0 to 100, inclusive.</p> 
backendGroups[].<br>stream.<br>backends[].<br>loadBalancingConfig.<br>strictLocality | **boolean** (boolean)<br><p>Specifies whether a load balancer node should only send traffic to backends in its availability zone, regardless of their health, and ignore backends in other zones.</p> <p>If set to ``true`` and there are no healthy backends in the zone, the node in this zone will respond to incoming traffic with errors. For details about strict locality, see <a href="/docs/application-load-balancer/concepts/backend-group#locality">documentation</a>.</p> <p>If ``strict_locality`` is ``true``, the value specified in ``localityAwareRoutingPercent`` is ignored.</p> <p>Default value: ``false``.</p> 
backendGroups[].<br>stream.<br>backends[].<br>loadBalancingConfig.<br>mode | **string**<br><p>Load balancing mode for the backend.</p> <p>For details about load balancing modes, see <a href="/docs/application-load-balancer/concepts/backend-group#balancing-mode">documentation</a>.</p> <p>A load balancing mode resource. For details about the concept, see <a href="/docs/application-load-balancer/concepts/backend-group#balancing-mode">documentation</a>.</p> <ul> <li> <p>ROUND_ROBIN: Round robin load balancing mode.</p> <p>All endpoints of the backend take their turns to receive requests attributed to the backend.</p> </li> <li> <p>RANDOM: Random load balancing mode. Default value.</p> <p>For a request attributed to the backend, an endpoint that receives it is picked at random.</p> </li> <li> <p>LEAST_REQUEST: Least request load balancing mode.</p> <p>To pick an endpoint that receives a request attributed to the backend, the power of two choices algorithm is used; that is, two endpoints are picked at random, and the request is sent to the one which has the fewest active requests.</p> </li> <li> <p>MAGLEV_HASH: Maglev hashing load balancing mode.</p> <p>Each endpoint is hashed, and a hash table with 65537 rows is filled accordingly, so that every endpoint occupies the same amount of rows. An attribute of each request is also hashed by the same function (if session affinity is enabled for the backend group, the attribute to hash is specified in session affinity configuration). The row with the same number as the resulting value is looked up in the table to determine the endpoint that receives the request.</p> <p>If the backend group with session affinity enabled contains more than one backend with positive weight, endpoints for backends with ``MAGLEV_HASH`` load balancing mode are picked at ``RANDOM`` instead.</p> </li> </ul> 
backendGroups[].<br>stream.<br>backends[].<br>port | **string** (int64)<br><p>Port used by all targets to receive traffic.</p> <p>Acceptable values are 0 to 65535, inclusive.</p> 
backendGroups[].<br>stream.<br>backends[].<br>healthchecks[] | **object**<br><p>Health checks to perform on targets from target groups. For details about health checking, see <a href="/docs/application-load-balancer/concepts/backend-group#health-checks">documentation</a>.</p> <p>If no health checks are specified, active health checking is not performed.</p> 
backendGroups[].<br>stream.<br>backends[].<br>healthchecks[].<br>timeout | **string**<br><p>Required. Health check timeout.</p> <p>The timeout is the time allowed for the target to respond to a check. If the target doesn't respond in time, the check is considered failed.</p> 
backendGroups[].<br>stream.<br>backends[].<br>healthchecks[].<br>interval | **string**<br><p>Required. Base interval between consecutive health checks.</p> 
backendGroups[].<br>stream.<br>backends[].<br>healthchecks[].<br>intervalJitterPercent | **number** (double)
backendGroups[].<br>stream.<br>backends[].<br>healthchecks[].<br>healthyThreshold | **string** (int64)<br><p>Number of consecutive successful health checks required to mark an unhealthy target as healthy.</p> <p>Both ``0`` and ``1`` values amount to one successful check required.</p> <p>The value is ignored when a load balancer is initialized; a target is marked healthy after one successful check.</p> <p>Default value: ``0``.</p> 
backendGroups[].<br>stream.<br>backends[].<br>healthchecks[].<br>unhealthyThreshold | **string** (int64)<br><p>Number of consecutive failed health checks required to mark a healthy target as unhealthy.</p> <p>Both ``0`` and ``1`` values amount to one unsuccessful check required.</p> <p>The value is ignored if a health check is failed due to an HTTP ``503 Service Unavailable`` response from the target (not applicable to TCP stream health checks). The target is immediately marked unhealthy.</p> <p>Default value: ``0``.</p> 
backendGroups[].<br>stream.<br>backends[].<br>healthchecks[].<br>healthcheckPort | **string** (int64)<br><p>Port used for health checks.</p> <p>If not specified, the backend port (``port`` or ``port``) is used for health checks.</p> <p>Acceptable values are 0 to 65535, inclusive.</p> 
backendGroups[].<br>stream.<br>backends[].<br>healthchecks[].<br>stream | **object**<br>TCP stream health check settings. <br>`backendGroups[].stream.backends[].healthchecks[]` includes only one of the fields `stream`, `http`, `grpc`<br>
backendGroups[].<br>stream.<br>backends[].<br>healthchecks[].<br>stream.<br>send | **object**<br><p>Message sent to targets during TCP data transfer.</p> <p>If not specified, no data is sent to the target.</p> <p>A health check payload resource.</p> 
backendGroups[].<br>stream.<br>backends[].<br>healthchecks[].<br>stream.<br>send.<br>text | **string**<br><p>Payload text.</p> <p>The string length in characters must be greater than 0.</p> 
backendGroups[].<br>stream.<br>backends[].<br>healthchecks[].<br>stream.<br>receive | **object**<br><p>Data that must be contained in the messages received from targets for a successful health check.</p> <p>If not specified, no messages are expected from targets, and those that are received are not checked.</p> <p>A health check payload resource.</p> 
backendGroups[].<br>stream.<br>backends[].<br>healthchecks[].<br>stream.<br>receive.<br>text | **string**<br><p>Payload text.</p> <p>The string length in characters must be greater than 0.</p> 
backendGroups[].<br>stream.<br>backends[].<br>healthchecks[].<br>http | **object**<br>HTTP health check settings. <br>`backendGroups[].stream.backends[].healthchecks[]` includes only one of the fields `stream`, `http`, `grpc`<br>
backendGroups[].<br>stream.<br>backends[].<br>healthchecks[].<br>http.<br>host | **string**<br><p>Value for the HTTP/1.1 ``Host`` header or the HTTP/2 ``:authority`` pseudo-header used in requests to targets.</p> 
backendGroups[].<br>stream.<br>backends[].<br>healthchecks[].<br>http.<br>path | **string**<br><p>Required. HTTP path used in requests to targets: request URI for HTTP/1.1 request line or value for the HTTP/2 ``:path`` pseudo-header.</p> 
backendGroups[].<br>stream.<br>backends[].<br>healthchecks[].<br>http.<br>useHttp2 | **boolean** (boolean)<br><p>Enables HTTP/2 usage in health checks.</p> <p>Default value: ``false``, HTTP/1.1 is used.</p> 
backendGroups[].<br>stream.<br>backends[].<br>healthchecks[].<br>grpc | **object**<br>gRPC health check settings. <br>`backendGroups[].stream.backends[].healthchecks[]` includes only one of the fields `stream`, `http`, `grpc`<br>
backendGroups[].<br>stream.<br>backends[].<br>healthchecks[].<br>grpc.<br>serviceName | **string**<br><p>Name of the gRPC service to be checked.</p> <p>If not specified, overall health is checked.</p> <p>For details about the concept, see <a href="https://github.com/grpc/grpc/blob/master/doc/health-checking.md">GRPC Health Checking Protocol</a>.</p> 
backendGroups[].<br>stream.<br>backends[].<br>healthchecks[].<br>plaintext | **object** <br>`backendGroups[].stream.backends[].healthchecks[]` includes only one of the fields `plaintext`, `tls`<br><br><p>Transport settings to be used instead of the settings configured per-cluster</p> 
backendGroups[].<br>stream.<br>backends[].<br>healthchecks[].<br>tls | **object** <br>`backendGroups[].stream.backends[].healthchecks[]` includes only one of the fields `plaintext`, `tls`<br><br><p>Transport settings to be used instead of the settings configured per-cluster</p> 
backendGroups[].<br>stream.<br>backends[].<br>healthchecks[].<br>tls.<br>sni | **string**<br><p>SNI string for TLS connections.</p> 
backendGroups[].<br>stream.<br>backends[].<br>healthchecks[].<br>tls.<br>validationContext | **object**<br><p>Validation context for backend TLS connections.</p> <p>A TLS validation context resource.</p> 
backendGroups[].<br>stream.<br>backends[].<br>healthchecks[].<br>tls.<br>validationContext.<br>trustedCaId | **string** <br>`backendGroups[].stream.backends[].healthchecks[].tls.validationContext` includes only one of the fields `trustedCaId`, `trustedCaBytes`<br>
backendGroups[].<br>stream.<br>backends[].<br>healthchecks[].<br>tls.<br>validationContext.<br>trustedCaBytes | **string** <br>`backendGroups[].stream.backends[].healthchecks[].tls.validationContext` includes only one of the fields `trustedCaId`, `trustedCaBytes`<br><br><p>X.509 certificate contents in PEM format.</p> 
backendGroups[].<br>stream.<br>backends[].<br>tls | **object**<br>Settings for TLS connections between load balancer nodes and backend targets.  If specified, the load balancer establishes HTTPS (HTTP over TLS) connections with targets and compares received certificates with the one specified in `validationContext`. If not specified, the load balancer establishes unencrypted HTTP connections with targets.
backendGroups[].<br>stream.<br>backends[].<br>tls.<br>sni | **string**<br><p>Server Name Indication (SNI) string for TLS connections.</p> 
backendGroups[].<br>stream.<br>backends[].<br>tls.<br>validationContext | **object**<br><p>Validation context for TLS connections.</p> <p>A TLS validation context resource.</p> 
backendGroups[].<br>stream.<br>backends[].<br>tls.<br>validationContext.<br>trustedCaId | **string** <br>`backendGroups[].stream.backends[].tls.validationContext` includes only one of the fields `trustedCaId`, `trustedCaBytes`<br>
backendGroups[].<br>stream.<br>backends[].<br>tls.<br>validationContext.<br>trustedCaBytes | **string** <br>`backendGroups[].stream.backends[].tls.validationContext` includes only one of the fields `trustedCaId`, `trustedCaBytes`<br><br><p>X.509 certificate contents in PEM format.</p> 
backendGroups[].<br>stream.<br>backends[].<br>enableProxyProtocol | **boolean** (boolean)<br><p>If set, proxy protocol will be enabled for this backend.</p> 
backendGroups[].<br>stream.<br>backends[].<br>targetGroups | **object**<br>Target groups that belong to the backend.
backendGroups[].<br>stream.<br>backends[].<br>targetGroups.<br>targetGroupIds[] | **string**<br><p>Required. List of ID's of target groups that belong to the backend.</p> <p>To get the ID's of all available target groups, make a <a href="/docs/application-load-balancer/api-ref/TargetGroup/list">list</a> request.</p> <p>Must contain at least one element.</p> 
backendGroups[].<br>stream.<br>connection | **object**<br>Connection-based session affinity configuration.  For now, a connection is defined only by an IP address of the client.
backendGroups[].<br>stream.<br>connection.<br>sourceIp | **boolean** (boolean)<br><p>Specifies whether an IP address of the client is used to define a connection for session affinity.</p> 
nextPageToken | **string**<br><p>Token for getting the next page of the list. If the number of results is greater than the specified <a href="/docs/application-load-balancer/api-ref/BackendGroup/list#query_params">pageSize</a>, use ``next_page_token`` as the value for the <a href="/docs/application-load-balancer/api-ref/BackendGroup/list#query_params">pageToken</a> parameter in the next list request.</p> <p>Each subsequent page will have its own ``next_page_token`` to continue paging through the results.</p> 