**Screenshot service api**

**About project:** 
Yet another screenshot api for internal web services. Contributed "as it is".
Project was written on python3 and code is pretty simple.
Main libs in project is flask and selenium.
Any arcadian can take part in development.
We can make world better toghether.

**API description:**
project rest api uses /shot route and json format.
json field name is 'url'.
Value of 'url' should be a string and match patter is http(s)://*.yandex-team.ru/*
Result of execution is a json within 'url' field name.
Url value is avatar_mds_object_url.
Type of file is png.

**Example:**

query:  $domain/shot  --header "Content-Type: application/json" -H 'Authorization: Oauth Your-token'   --request POST   --data '{"url":"ANY *.y-t.ru URL with proto"}' 

result:
{"url":"http://avatars.mdst.yandex.net/$avatar_mds_object_uri"}
file type of screenshot is png