rpslimiter-router
=====

Request router for rps-limiter

Syntax
------

```yaml
- rpslimiter-router:
    headers:
      balancer: x-balancer
    const:
      quota: default
    urls: urls

    export:
    - urls
    - balancer

    router:
    - map: balancer
      data:
      - key: reqwizard
        const:
          quota: reqwizard
        limiter: limiter
  export: quota
```
Options
-------

TODO