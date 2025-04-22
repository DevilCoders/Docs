Вот такой mapping-objects.yaml version 2

```
groups:
  l3_balancers:
    types:
      common: mnt_traf
    stages:
      - stable
    prefix: balancer
```

соберёт в RT все хосты с тегами "stable", "balancer-common" и без тега "в оффлайне", и поместит их в группу "l3_balancers-common-stable" проекта "mnt_traf" Кондуктора.
