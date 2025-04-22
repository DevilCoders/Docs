Use this template to create layer: https://sandbox.yandex-team.ru/template/analytics_delta_layer_builder/view

Use the following example to setup nile client:
```
PYTHON3_LAYERS = [
    '//home/b2bgeo/analytics_delta_layers/porto_layer_search_ubuntu_bionic_app-2020-01-23-17.41.42.tar.gz',
    '//home/b2bgeo/analytics_delta_layers/python3.8_bionic_01_23_libs.tar.gz',
]
...
job = job.env(
        yt_spec_defaults=dict(
            mapper=dict(layer_paths=PYTHON3_LAYERS),
            reducer=dict(layer_paths=PYTHON3_LAYERS),
        )
    )
...
```

More details: https://wiki.yandex-team.ru/users/demidov-artem/pereezd-geoanalytics-na-python-3/

