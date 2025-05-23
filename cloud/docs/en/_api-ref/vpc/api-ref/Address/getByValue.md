---
editable: false
---

# Method getByValue
Returns the specified Address resource by a given value.
 
To get the list of all available Address resources, make a [list](/docs/vpc/api-ref/Address/list) request.
 
## HTTP request {#https-request}
```
GET https://vpc.{{ api-host }}/vpc/v1/addresses:byValue
```
 
## Query parameters {#query_params}
 
Parameter | Description
--- | ---
externalIpv4Address | 
 
## Response {#responses}
**HTTP Code: 200 - OK**

```json 
{
  "id": "string",
  "folderId": "string",
  "createdAt": "string",
  "name": "string",
  "description": "string",
  "labels": "object",
  "reserved": true,
  "used": true,
  "type": "string",
  "ipVersion": "string",
  "externalIpv4Address": {
    "address": "string",
    "zoneId": "string",
    "requirements": {
      "ddosProtectionProvider": "string",
      "outgoingSmtpCapability": "string"
    }
  }
}
```
An Address resource. For more information, see [Address](/docs/vpc/concepts/address).
 
Field | Description
--- | ---
id | **string**<br><p>ID of the address. Generated at creation time.</p> 
folderId | **string**<br><p>ID of the folder that the address belongs to.</p> 
createdAt | **string** (date-time)<br><p>Creation timestamp.</p> <p>String in <a href="https://www.ietf.org/rfc/rfc3339.txt">RFC3339</a> text format.</p> 
name | **string**<br><p>Name of the address. The name is unique within the folder.</p> 
description | **string**<br><p>Description of the address.</p> 
labels | **object**<br><p>Resource labels as ``key:value`` pairs.</p> 
reserved | **boolean** (boolean)<br><p>Specifies if address is reserved or not.</p> 
used | **boolean** (boolean)<br><p>Specifies if address is used or not.</p> 
type | **string**<br>Type of the IP address.<br><ul> <li>INTERNAL: Internal IP address.</li> <li>EXTERNAL: Public IP address.</li> </ul> 
ipVersion | **string**<br>Vervion of the IP address.<br><ul> <li>IPV4: IPv4 address.</li> <li>IPV6: IPv6 address.</li> </ul> 
externalIpv4Address | **object**
externalIpv4Address.<br>address | **string**<br><p>Value of address.</p> 
externalIpv4Address.<br>zoneId | **string**<br><p>Availability zone from which the address will be allocated.</p> 
externalIpv4Address.<br>requirements | **object**<br><p>Parameters of the allocated address, for example DDoS Protection.</p> 
externalIpv4Address.<br>requirements.<br>ddosProtectionProvider | **string**<br><p>DDoS protection provider ID.</p> 
externalIpv4Address.<br>requirements.<br>outgoingSmtpCapability | **string**<br><p>Capability to send SMTP traffic.</p> 