l7_upstream_macro:
  version: 0.0.1
  id: {upstream_id}
  matcher:
    host_re: "{host_name}.apphost.in.yandex-team.ru"
  headers:
    - create: {{target: X-Yandex-Internal-Request, value: 1}}
  flat_scheme:
    balancer:
      backend_timeout: 20s
      connect_timeout: 100ms
      attempts: 3
      fast_attempts: 2
      do_not_retry_http_responses: true
      max_reattempts_share: 0.2
      max_pessimized_endpoints_share: 0.2
    backend_ids:
    - {backend_id}
    on_error:
      static:
        status: 504
        content: 'Service unavailable'
