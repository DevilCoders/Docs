## Simple yc/postgresql api wrapper


```python
from metrika.pylib.yc.postgresql import ManagedPostgreSQL


def main()
    api = ManagedPostgreSQL(
        token='yc oauth token',
    )
    cluster = api.cluster('meta-monetize/conv/bishop')

    print(
        cluster.data.config.resources.diskSize
    )

    user = api.user('meta-monetize/conv/bishop', 'bishop')

    print(
        user.data.connLimit
    )


if __name__ == '__main__':
    main()

```
