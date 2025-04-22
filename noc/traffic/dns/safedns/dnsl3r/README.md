DNSL3R
======

This tool is a web application/server which answers: a) L3 load balancer
(keepalived) heath check qureies and b) Yandex.Deploy readiness and liveness
checks.
It's intended to run on pods with recursive DNS resolver. Load balancer can't
reliable check resolver readiness, so this app stays in between, hence DNSL3R
or DNS-to-L3-reply. It qureies local recursive resolver and answer load
balancer based on resolver status.

CLI
---

App's CLI handled by Python click library. Help message available with --help
as usual. To start app this options and arguments required:
    * --server-ip - IP address to list on (can be 'any')
    * --server-port - port to listen on
    * ip-list - it's a list of arguments (any number) provided last which
      describes IP addresses where local recursive DNS resolver listen.
Options with default values are:
    * --query-period [1.0] - period between DNS qureies, between 0.2 and 30.0
    * --query-timeout [0.5] - time to wait for answer on DNS query, between 0.1
      and query-period
    * --query-dn [ya.ru] - domain name to use in quries, supports special value
      '$self', which will be replaces by local hostname provided by
      socket.gethostname()
    * --rr-type [AAAA] - resource record type to use in query, can be AAAA or A
    * --server-logs [False] - is a flag, which activates web server logging, it
      can impact performance, but we don't aim at it
    * --log-level [warning] - this one controls level of messages coming from
      dn3lr
Also this things available:
    * --help
    * --version

Readiness checks
----------------

That one is easy, just reply 200/OK always.

Load balancer check
-------------------

To answer health checks from load balancer app needs number of things to know.

First of all, load balancer checks must be made to IP addresses behind which
DNS resolver operates, with HTTP hostname equal to that address (using brackets
as usual in case of IPv6). Otherwise app will reply with 404.

Next, a stop file will be checked (look at dnsl3r.server.STOP\_FILE). If it's
exist - 503 will be replied. It's used to provide gracefull shutdown.

Then, resolver status behind quried IP address will be checked. Status
controlled by background tasks started by server at it's startup time. Tasks
starts for every IP address provided in ip-list argument. It's run in infinite
loop queriing DNS resolver behind that IP address every query-period and
updating corresponding counter. Counter increments with every successful query
by 1, or decrements by 1 otherwise. It's limited by
dnsl3r.models.counter.MIN\_TRESHOLD\_VALUE and MAX\_THRESHOLD\_VALUE (0 and 2).
When lower bound reached, status is set to False, when upper bound reached,
status is set to True. That allows switching between states in 2 steps.
If status is True - 200 replied, otherwise - 503.
Stop file and counters stored in a server instance (sanic feature). Running
tasks in the background is sanic feature also.

Used apps
---------

    * aiodns - to query resolver
    * click - CLI
    * sanic - web framework/server
