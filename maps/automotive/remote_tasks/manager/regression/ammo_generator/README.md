# How to run

```
# Generate ammo for tasks && fill database
ya make && \
    ./ammo_generator \
    --db-host sas-qaxl5a9k3j3sln05.db.yandex.net \
    --db-name remote_tasks_backend_stress \
    --db-user remote_tasks_backend \
    --db-password-secret-version ver-01edv2cvb50phxhfs0ch67esgm \
    --db-port 6432 \
    --out maps-auto-remote-tasks-manager-tasks-ammo \
    --tasks

# Generate ammo for /is_alive
ya make && \
    ./ammo_generator \
    --out maps-auto-remote-tasks-manager-is-alive-ammo \
    --alive
```

# How to upload

```
aws --endpoint-url=http://s3.mds.yandex.net \
    --profile maps_stress \
    s3 cp maps-auto-remote-tasks-manager-tasks-ammo \
    s3://maps-load-ammo/maps-auto-remote-tasks-manager-tasks-ammo

aws --endpoint-url=http://s3.mds.yandex.net \
    --profile maps_stress \
    s3 cp maps-auto-remote-tasks-manager-is-alive-ammo \
    s3://maps-load-ammo/maps-auto-remote-tasks-manager-is-alive-ammo
```

