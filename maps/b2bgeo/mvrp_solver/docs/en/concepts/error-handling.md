# Handling errors

The Yandex.Routing VRP API returns JSON in response to all requests and uses standard response codes.

In case of rare problems with Yandex servers, the API returns a 50x status code.

Any errors related to data validation or business logic are described in the response body with status code 200 and must be handled by the user.

## Repeated requests

In rare cases, there might be connection issues between your app and Yandex servers or short-term interruptions in the operation of Yandex servers.

In the event of a connection issue, we recommend that you configure request and response timeouts in your client. 10 seconds should be enough to smooth out most of the possible problems.

If there's an issue on the Yandex server side, you may receive an HTTP 5xx error code. Server-side issues are usually fixed automatically and it takes a few seconds. To ensure that your app keeps working if a connection is interrupted, we recommend sending repeated requests with a delay. To reduce the load on the servers due to repeated requests, we also recommend using increased delays between requests.

To determine the number of requests and the pause between them, take into account the total time required to process an optimization task. There is no rule of thumb for the required number of repeated requests. However, the basic recommendations are as follows.

For example, for a small task that takes 10 seconds, it's usually sufficient to send repeated requests with a delay of up to 1.5 seconds:

```
initial_delay = 0.1s
backoff_multiplier = 2
max_retries = 4

retry 1: delay 0.1s
retry 2: delay 0.1s * 2 = 0.2s
retry 3: delay 0.1s * 4 = 0.4s
retry 4: delay 0.1s * 8 = 0.8s
```

For lengthy tasks that take up to 30 minutes, you may need a longer delay:

```
initial_delay = 1s
backoff_multiplier = 2
max_retries = 32

retry 1: delay 1s
retry 2: delay 1s * 2 = 2s
retry 3: delay 1s * 4 = 4s
retry 4: delay 1s * 8 = 8s
retry 5: delay 1s * 16 = 16s
retry 6: delay 1s * 32 = 32s
...
```

<p class="p"><a href="feedback.html" class="xref button">Write to Support</a></p>

