# luster-billing-keys example

~~~shell
› npm run

billing is available for worker 1
billing is available for worker 2
[luster-billing-keys] update keys ["key1==","key2=="]
[luster-billing-keys] update keys ["key1==","key2=="]

server is running on http://localhost:10105
~~~

~~~shell
› kill -hup $(pgrep node | head -1)

[luster-billing-keys] update keys ["key1==","key2=="]
[luster-billing-keys] update keys ["key1==","key2=="]
~~~
