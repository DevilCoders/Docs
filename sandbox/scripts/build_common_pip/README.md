# Build `sandbox.common` for PyPI

```bash
arcadia$ ya make sandbox/scripts/build_common_pip
Ok

arcadia$ sandbox/scripts/build_common_pip/build-common-pip
running sdist
<...>
running bdist_wheel
<...>

arcadia$ ls -1 *.whl *.tar.gz
sandbox_common-2019.8.31.post1567247717-py2-none-any.whl
sandbox-common-2019.8.31.post1567247717.tar.gz
```

Magic!
