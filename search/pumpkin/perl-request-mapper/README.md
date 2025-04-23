# Overview
This is a perl version of request mapper script.
Request mapper maps user's search requests to previously cached static SERP pages with request answer.

Example:
    http://yandex.ru/yandsearch?text=some%20search%20request -> 111abed2c0f7a3d30aca5e850168dbc8.html

# Details
How to map:
Mapper uses 'index' file which maps source URL with search request to destination URI.

When incoming reauest comes, perl script searches request url in source URLs list of index file and makes internal redirect to destination URI.

## Index file format
```
<source URL_1>\t<destination_URI_1>
<source URL_2>\t<destination_URI_2>
```
