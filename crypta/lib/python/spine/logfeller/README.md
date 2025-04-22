## Logfeller parsing checks

```python
from crypta.lib.python.spine import logfeller
from crypta.lib.python.spine.juggler import juggler_check_generator

# Requires JugglerCheckGenerator
juggler = juggler_check_generator.JugglerCheckGenerator(tags=["crypta-cm"])

# Alert when logfeller fails to parse some records in the following logs
# Check's host is "crypta-logfeller", stream is used as a service with '@' replaced as '_'
for stream in [
    "crypta@prod@cm-access-log",
    "crypta@test@cm-access-log",
    "crypta@prod@cm-change-log",
    "crypta@test@cm-change-log",
    "crypta@prod@evacuation-rt-log",
    "crypta@test@evacuation-rt-log",
]:
    logfeller.add_unprased_records_check(juggler, stream)
```
