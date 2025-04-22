Usage example

```
ya make billing/hot/nirvana/maintenance
```

```
./billing/hot/nirvana/maintenance/maintenance update-directory-tree //home/balance/test/new_billing \
    --config ./billing/hot/nirvana/maintenance/bnpl/directories.yaml
```

```
./billing/hot/nirvana/maintenance/maintenance nirvana-reactions --no-skip-enabled \
    --config ./billing/hot/nirvana/maintenance/bnpl/reactions-test.yaml
```

```
./billing/hot/nirvana/maintenance/maintenance clear-directory-tree-from-run-id //home/balance/prod/new_billing 2021-07-23T05:55:00
```

```
ya py billing/hot/nirvana/maintenance
```
```
import os
import nirvana_api
import reactor_client
import reactor_client.reactor_objects as robs
from billing.hot.nirvana.maintenance import nirvana_reactor
oauth_token = open(os.path.expanduser('~/.nirvana/oauth_token')).read().strip()
simple_nirvana_reactor = nirvana_reactor.SimpleNirvanaReatorClient(oauth_token, root_path=None, project_path=None, quota=None, owner=None, common_description=None)
```
