# Overview

The Yandex.Images Search API is intended for searching the Yandex.Images index with a specific set of parameters. [Search parameters](xmlparams.md#intservicesparms) are passed to the service as an [HTTP request](xmlparams.md) using the GET method. Yandex.Images generates a response in the form of an {% if audience == "external" %}[XML document](xmlanswer.md){% endif %}{% if audience == "internal" %}[XML document](xmlanswer-internal.md){% endif %}.

Advantages of using an XML document:

- Simplified processing of search output results.
- Results are obtained faster by bypassing several stages in generating search output.

API access is restricted for external services. To get access, you must get permission from the Business Development department.

To use the Yandex.Images Search API, an external service must provide a list of IP addresses that they will be accessing the API from. The external service is provided with a user name and an API key, which will be used when forming an [HTTP request](xmlparams.md).

