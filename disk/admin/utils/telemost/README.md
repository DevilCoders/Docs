Use cases:
Show YP backends:
backend-ctrl.py yp_backends testing

Show ZK backends:
backend-ctrl.py zk_backends testing

Switch backend in ZK:
backend-ctrl.py zk_switch testing vjxl4a5efyrgtfkf.sas.yp-c.yandex.net 27zupewxssog5slv.vla.yp-c.yandex.net

Deploy unit:
backend-ctrl.py deploy testing xmpp1 ./telemost-testing.yml

Find unit for update:
backend-ctrl.py unit_for_update testing

Switch backend in ZK (for bucket):
backend-ctrl.py zk_switch testing 2 27zupewxssog5slv.vla.yp-c.yandex.net

List buckets and backends:
backend-ctrl.py zk_buckets testing

Get bucket by roomId:
backend-ctrl.py get_bucket testing 426d5ae121444edd89bec52a01fd78c3
