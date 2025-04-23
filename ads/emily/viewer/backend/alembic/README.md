# Postgres DB scheme migration

```bash
make build

# Upgrade
make upgrade

# Downgrade
make downgrade

# Create new revision
make revision
# Then, if ENUMs are used, manually add dropping them in downgrade().
# See https://github.com/sqlalchemy/alembic/issues/278#issuecomment-668238745
```

Decided not to use

```python
# ya.make
# -------
RESOURCE_FILES(
    alembic.ini
    env.py
    script.py.mako
    versions/*.py
)

# bin/__main__.py
# ---------------
from logos.libs.resource_storage import 

materialize_resources("ads/emily/viewer/backend/alembic")
```

because this script is supposed to run only from current directory.
