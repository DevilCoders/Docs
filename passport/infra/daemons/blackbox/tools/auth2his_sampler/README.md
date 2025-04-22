auth2his_sampler
==
It is the sampler which should be used in push-client as `pipe`.

It accepts log entry from `stdin` and prints it as-is to `stdout` if same entry was not appeared while last 1 hour.

Default config path is `/etc/yandex/passport-auth2his-sampler.conf`.
It pushes signals to `xunistater` - every second by default.

Can rotate own log with `SIGHUP`.
