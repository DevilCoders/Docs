![](https://jing.yandex-team.ru/files/roboslone/1-4.png)

`horadric`'s magic allows protobuf to be transmuted into other things, like python/typescript wrappers or SQLAlchemy models.

# Compilation
```bash
ya m -r --checkout $ARCADIA/search/horadric
```

# Usage
```bash
# Full argument keys:
ya tool horadric --config /path/to/horadric.conf --output-dir /path/to/generated --protoc-dir /path/to/protoc

# Short argument keys:
ya tool horadric -c /path/to/horadric.conf -o /path/to/generated -p /path/to/protoc

# With target project dir
#   The project directory is used only to find the config
ya tool horadric /path/to/project

# By default horadric try to use 'config.yaml', 'horadric.conf' or '.horadric.conf' as config path
```

Example:
```protobuf
// auth.proto

message User {
    option (db.table) = true;

    string name = 1 [(db.primary_key) = true];
}
```

```typescript
// messages.ts

export class User implements interfaces.IUser {
    public name: string

    public constructor (
        name: string = ''
    ) {
        this.name = name
    }

    public static FromData(data: interfaces.IUserData): User {
        if (data === undefined) {
            return new User()
        }

        return new User(
            data.name,
        )
    }
}
```

```python
# messages.py

class User(object):
    PROTO_CLASS = structures.auth_pb2.User

    JSON_FIELD_NAMES = {
        'name': 'name',
    }

    FIELD_NAMES = {
        'name': 'name',
    }

    VALIDATORS = {
    }

    @classmethod
    def from_get_params(cls, params):
        message = cls()
        message.name = str(params.get('name', ''))

        return message

    def __init__(self, name=''):
        """
        :type name: typing.Union[str, unicode]
        """
        self.name = name  # type: typing.Union[str, unicode]

    def __new__(cls, *args, **kwargs):
        return structures.auth_pb2.User(*args, **kwargs)

    CopyFrom = structures.auth_pb2.User.CopyFrom
    FromString = staticmethod(structures.auth_pb2.User.FromString)
    HasField = structures.auth_pb2.User.HasField
    ListFields = structures.auth_pb2.User.ListFields
    MergeFrom = structures.auth_pb2.User.MergeFrom
    SerializeToString = structures.auth_pb2.User.SerializeToString
```

```python
# models.py

class User(BaseModel):
    __tablename__ = 'yappy__User'
    __repr_attrs__ = []

    name = sqlalchemy.Column(types.Text, primary_key=True)
    roles = relationship(
        'Roles',
        secondary='yappy__Roles__owners',
        back_populates='owners',
    )
    token = relationship(
        'Token',
        uselist=False,
        back_populates='user',
    )
    revisions = relationship(
        'Revision',
        back_populates='author',
    )

    @property
    def pk_values(self):
        return [
            self.name,
        ]

    @property
    def pk_names(self):
        return [
            'name',
        ]

    def to_protobuf(self):
        message = yappy_protoc.yappy.User()
        if self.name:
            message.name = self.name
        return message

    @classmethod
    def from_protobuf(cls, message):
        # noinspection PyDictCreation
        kwargs = {}
        kwargs['name'] = message.name
        return cls(**kwargs)
```
