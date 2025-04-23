## Как обновить ресурс

Если формат тензора поменялся, то нужно обновить ресурс в ya.make, заменив на новый.

```sh
yam -rttt . -F test_pull_tensor.py::test_upload_resource --test-param resource_id=2263891629 --test-stderr --yt-store
```
В выводе покажется id ресурса

```sh

Add to ya.make:

	sbr://2268521739=test_model

```

Запусти тесты и поменяй TEST_DEFAULTS в conftest.py
