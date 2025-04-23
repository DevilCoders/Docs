# travel.rasp.bus.db

Модуль для работы с автобусным PGaaS. Предоставляет сконфигурированную фабрику Session() для работы с базой данных и модели.

```python
from travel.rasp.bus.db import Session
from travel.rasp.bus.db.models.carrier import Carrier

session = Session()

print list(session.query(Carrier).limit(3))
```
