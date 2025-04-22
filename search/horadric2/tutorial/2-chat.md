# Чат
В этой секции туториала мы попробуем реализовать чат –
сервис, позволяющий сздавать/удалять группы и обмениваться сообщениями в них:

```bash
curl -X POST \
     -d '{"id": "test"}' \
     -H 'Content-Type: application/json' \
     http://localhost:8888/api/tutorial.Chat/listMessages
```
```json
{
    "messages": [
        {
            "groupId" "test",
            "author": "roboslone",
            "time": 1590579762.983872,
            "text": "Hello, Horadric!"
        }
    ]
}
```

Узнаем про аутентификацию/авторизацию в horadric-based-сервисах и попробуем написать UI.

## Описываем протоколы
Как и в случае с [Echo](https://a.yandex-team.ru/arc/trunk/arcadia/search/horadric2/tutorial/1-echo.md) заводим проект `horadric/chat`.

```protobuf
// horadric/chat/proto/data.proto

syntax = "proto3";

package tutorial;


message Message {
    string group_id = 1;
    string author = 2;
    double time = 3;
    string text = 4;
}

message MessageList {
    repeated Message messages = 1;
}

message Group {
    string id = 1;
    repeated string participants = 2;
}

message GroupList {
    repeated Group groups = 1;
}
```

```protobuf
// horadric/chat/proto/service.proto

syntax = "proto3";

package tutorial;

import "google/protobuf/empty.proto";
import "horadric/chat/proto/data.proto";


service Chat {
    rpc createGroup (Group) returns (Group);
    rpc getGroup (Group) returns (Group);
    rpc updateGroup (Group) returns (Group);
    rpc deleteGroup (Group) returns (google.protobuf.Empty);
    rpc listGroups (google.protobuf.Empty) returns (GroupList);

    rpc sendMessage (Message) returns (MessageList);  // в ответ на отправленное сообщение отдаем последние сообщения в группе – экономим запросы с UI
    rpc listMessages (Group) returns (MessageList);
}
```

Пока все должно быть понятно.
Однако такие протоколы позволяют создавать группы и слать сообщения без аутентификации.

Заставим наш сервис отвечать `StatusCode.UNAUTHENTICATED` (HTTP 401) на такие запросы:
```protobuf
// horadric/chat/proto/service.proto

import "search/horadric2/proto/extensions/rpc.proto";

// ...

service Chat {
    // ...

    rpc createGroup (Group) returns (Group) {
        option (h.rpc.auth_required) = true;
    };

    rpc sendMessage (SendMessageRequest) returns (MessageList) {
        option (h.rpc.auth_required) = true;
    };
}
```

## База данных
Сообщения нужно где-то хранить, в данном туториале мы будем использовать PostgreSQL.
Осторожно, [реклама](https://wiki.yandex-team.ru/MDB/)!

Настройку БД в контексте этого туториала рассматривать не будем, будем считать, что у нас уже есть база.
Сразу запишем connstring в переменную окружения – оттуда ее прочитает наш сервис:
```bash
export DB_URL='postgresql://horadric:secret@localhost:5432/tutorial'
```

> А как же **production**?
>
> Да в общем-то ровно так же. Connstring можно хранить в [секретнице](https://yav.yandex-team.ru/),
> а оттуда его может забрать [Nanny](https://nanny.yandex-team.ru) или [Deploy](https://deploy.yandex-team.ru).

## Интеграция с PostgreSQL
Для того чтобы сохранять наши сообщения и группы в БД расширим протокол:
```protobuf
// horadric/chat/proto/data.proto

import "search/horadric2/proto/extensions/db.proto";

// ...

message Message {
    // добавляем индексы по Message.group_id и Message.time
    string group_id = 1 [(h.db.index) = true];
    double time = 2 [(h.db.index) = true];

    // ...

    // добавляем сообщениям ID и генерируем его на стороне БД (UUID)
    string id = 5 [(h.db.primary_key) = true, (h.db.generated_type) = uuid];
}

message Group {
    // для групп в качестве PK используем Group.id
    string id = 1 [(h.db.primary_key) = true];
}
```

Не забываем сделать `PEERDIR`:
```make
# horadric/chat/bin/ya.make

PEERDIR(
    ...
    search/horadric2/proto
)
```

Теперь Horadric должен сгенерировать SQLAlchemy-модели для нашего проекта.
Для этого добавим Cairn Stone "Alchemy":
```yaml
# horadric/chat/inifuss.scroll

# ...

cairnStones:
    - name: alchemy
    # ...
```

Не забываем добавить их в `PEERDIR`:
```make
PEERDIR(
    ...
    horadric/chat/sqla
)
```

## Создаем таблички
Можно ручками. А можно и не ручками:
```python
from search.martylib.db_utils import prepare_db

from horadric.chat.sqla.tutorial.model import *

prepare_db()
```

Этот код нужно вызывать в контексте проекта, чтобы интерпретатор нашел сгенерированные модели.

Импорт моделей там тоже неслучайно – без него `prepare_db` не узнает об их существовании.

Что произойдет:
- `prepare_db` найдет все модели, до которых сможет добраться
- подключится к PostgreSQL по connstring указанному в `DB_URL`
- для каждой модели создаст таблицу, если ее еще не существует
- для каждого `enum` создаст тип, если его еще не существует

> **ВАЖНО**
>
> Horadric не умеет в миграции (по крайней мере пока).
> Изменения в моделях придется доносить до базы руками (можно конечно дропнуть все изменившиеся таблицы и снова позвать `prepare_db`, что **приведет к потере данных**).

А создавать вот так руками каждый раз? Ну конечно нет.
`prepare_db` – безопасная операция, она не удалит ваши данные и не изменит существующие таблицы/типы.
Ее можно выполнять на старте бинарника.

## А бинарника-то у нас и нет
Ничего, сейчас замутим.

```python
# horadric/chat/bin/main.py

from search.martylib.core.date_utils import now
from search.martylib.core.storage import Storage
from search.martylib.db_utils import prepare_db, session_scope, to_protobuf
from search.martylib.modules import Daemon, ServerModule, ServiceModule
from search.martylib.protobuf_utils.repeated import replace_in_repeated

from horadric.chat.proto import data_pb2
from horadric.chat.services.tutorial import ChatInterface
from horadric.chat.sqla.tutorial import model


class Chat(ChatInterface):
    pass


class ChatModule(ServiceModule):
    @classmethod
    def get_service(cls):
        return Chat()


class Server(ServerModule):
    @classmethod
    def get_server(cls):
        return get_grpc_server(f'[::]:{cls.args.port}', services=())

    @classmethod
    def setup(cls):
        prepare_db()  # Перед каждым запуском создаем недостающие таблицы/типы в БД.


def parse_args():
    parser = argparse.ArgumentParser()
    parser.add_argument('-p', '--port', type=int, default=50051)
    parser.add_argument('modules', nargs='*', default=['Server', 'ChatModule'])
    return parser.parse_args()


def main():
    configure_binlog('tutorial')
    Daemon(args=parse_args()).run()
```

Дальше рассмотрим имплементацию сервиса:
```python
class Chat(ChatInterface):
    # Отсюда будем доставать результат аутентификации.
    storage = Storage()

    # Соблюдаем PEP8, поэтому имя хендлера в snake_case.
    def create_group(self, request, context):
        # Не доверяем пользовательскому вводу:
        if not request.id:
            raise ValueError('`id` is required')
        if len(request.id) > 255:
            raise ValueError('`id` is too long (255 characters max)')

        # Начинаем транзакцию.
        with session_scope() as session:
            # Проверяем, что такой группы еще нет.
            if session.query(
                session.query(model.Group)
                .filter(model.Group.id == request.id)
                .exists()
            ).scalar():
                raise ValueError('group already exists')
                
            # Добавляем автора запроса в группу.
            request.participants.append(self.storage.thread_local.auth_info.login)

            # Удаляем дубликаты и сортируем.
            replace_in_repeated(
                request.participants,
                sorted(set(request.participants)),
            )

            # Сохраняем группу в базе.
            group = session.merge(to_model(request))

            # Возвращаем ответ.
            return group.to_protobuf()
```

Важно понимать, что у нас нет concurrency control:
при обработке двух одновременных запросов в разные инстансы `exists()` вернет `False` обоим.

Один из вариантов решения – распределенные блокировки, про которые можно почитать вот [тут](https://a.yandex-team.ru/arc/trunk/arcadia/search/martylib/raft).

Продолжаем, добавим метод для получения сообщений:
```python
def list_messages(self, request, context):
    if not request.id:
        return data_pb2.MessageList()

    with session_scope() as session:
        return data_pb2.MessageList(objects=map(
            to_protobuf,
            (
                session.query(model.Message)
                .filter(model.Message.group_id == request.id)
                .order_by(model.Message.time.desc())
                .limit(20)
                .all()
            )
        ))
```

Существование группы не проверяется, если ее не будет – вернем пустой список. Для туториала покатит :]

Теперь научимся принимать сообщения:
```python
def send_message(self, request, context):
    if not request.group_id:
        raise ValueError('`group_id` is required')

    # Все еще не доверяем.
    request.time = now().timestamp()
    request.author = self.storage.thread_local.auth_info.login    

    with session_scope() as session:
        session.merge(to_model(request))

        # А в ответ отдаем последние 20 сообщений из той же группы.
        # Ниже копипаста, ее, конечно, стоит унести в отдельный метод/функцию.
        return data_pb2.MessageList(objects=map(
            to_protobuf,
            (
                session.query(model.Message)
                .filter(model.Message.group_id == request.id)
                .order_by(model.Message.time.desc())
                .limit(20)
                .all()
            )
        ))
```

В таком же духе реализуем остальные методы и запускаемся:
```bash
ya make bin && ./bin/chat
```

## UI
TBA