### For local run

Create file `bin/config.yaml`:
```bash
cat <<EOF > bin/config.yaml
raft:
  yp_endpoint_set:
    - sas/dummy
EOF
```

Extend this file for your liking.
For now, Raft doesn't crash with empty list of endpoint sets, but it pretends like it would like to;
so having a dummy endpoint set there looks like a good idea.


### For local tests

Running Py23 tests that use same test DB is a bad idea: tests are failing with "relation ... does not exist".
To avoid this, one could run py2- or py3-only tests (and style tests separately):
```bash
ya make -tt --test-type py2test
ya make -tt --test-type py3test
ya make -t --style
```
