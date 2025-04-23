# Nanny rest client
For all you can do with Nanny service via REST api

Typical code using this library be like:

```python
from saas.library.python.sandbox import SandboxApi
from saas.library.python.nanny_rest import NannyServiceIterator
from saas.library.python.nanny_rest.resource import SandboxFile
from saas.library.python.token_store import PersistentTokenStore

required_clients = ('nanny', 'yav', 'sandbox')
PersistentTokenStore.ensure_tokens_for(required_clients)
push_client_resource = SandboxFile(
    'latest_push_client',
    **SandboxApi().get_last_released_resource('STATBOX_PUSHCLIENT').nanny_resource_info()
)


for nanny_service in NannyServiceIterator(filter_=lambda s: s.info_attrs['abc_group']=='664'):  # type: NannyServiceBase
    with nanny_service.runtime_attrs_transaction(
        f'Commit message', 'SAAS-666'
    ) as runtime_attrs:  # type: NannyServiceBaseRuntimeProxy
        runtime_attrs.set_resource(push_client_resource)
```


