---
editable: false
---

# Method listVersions

 

 
## HTTP request {#https-request}
```
GET https://certificate-manager.{{ api-host }}/certificate-manager/v1/certificates/{certificateId}/versions
```
 
## Path parameters {#path_params}
 
Parameter | Description
--- | ---
certificateId | <p>Required. ID of the certificate to list versions for.</p> <p>The maximum string length in characters is 50.</p> 
 
## Query parameters {#query_params}
 
Parameter | Description
--- | ---
pageSize | <p>Page token. To get the next page of results, set ``page_token`` to the <a href="/docs/certificate-manager/api-ref/Certificate/list#responses">nextPageToken</a> returned by a previous list request.</p> <p>The maximum value is 1000.</p> 
pageToken | <p>Page token. To get the next page of results, set ``page_token`` to the <a href="/docs/certificate-manager/api-ref/Certificate/list#responses">nextPageToken</a> returned by a previous list request.</p> <p>The maximum string length in characters is 100.</p> 
 
## Response {#responses}
**HTTP Code: 200 - OK**

```json 
{
  "versions": [
    {
      "id": "string",
      "certificateId": "string",
      "createdAt": "string"
    }
  ],
  "nextPageToken": "string"
}
```

 
Field | Description
--- | ---
versions[] | **object**<br><p>List of versions for the specified certificate.</p> 
versions[].<br>id | **string**<br><p>ID of the version.</p> 
versions[].<br>certificateId | **string**<br><p>ID of the certificate that the version belongs to.</p> 
versions[].<br>createdAt | **string** (date-time)<br><p>Time when the version was created.</p> <p>String in <a href="https://www.ietf.org/rfc/rfc3339.txt">RFC3339</a> text format.</p> 
nextPageToken | **string**<br><p>This token allows you to get the next page of results for list requests. If the number of results is greater than the specified <a href="/docs/certificate-manager/api-ref/Certificate/list#query_params">pageSize</a>, use the ``next_page_token`` as the value for the <a href="/docs/certificate-manager/api-ref/Certificate/list#query_params">pageToken</a> query parameter in the next list request. Each subsequent list request will have its own <a href="/docs/certificate-manager/api-ref/Certificate/listVersions#responses">nextPageToken</a> to continue paging through the results.</p> 