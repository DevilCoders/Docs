## Updater

#### How  to run this in 2022

```
manage.sh
+export TVM_CLIENT_SECRET=`ya vault get version sec-01eeaw0ptzmkd2he6cqrnkjnqg -o client_secret`
+export UPDATER_DB_URI="postgresql+psycopg2://@/updater?host=/var/run/postgresql"
+cd `dirname $0`

ya make && ./manage.sh db current --directory ~/dev/arc/arcadia/yaphone/newpdater/migrations

./manage.sh db revision --directory ~/dev/arc/arcadia/yaphone/newpdater/migrations --autogenerate -m "Add targeting_string field"
./manage.sh db upgrade --directory ~/dev/arc/arcadia/yaphone/newpdater/migrations
```

#### New code

Please, see `prebuilt` module as an example.
To create a new module:
1. Add a new directory for a new feature to `src/`: `newpdater/src/prebuilt`
2. If you need to use some data from databases and perform data related actions, create a `repository.py`
3. Add a `service.py` if you need to handle some logic or to use another serivce's API
4. Add an `__init__.py` file if you need to initialize some components, required for a module
5. Add a `routes.py` file to register blueprints and views
6. Register routers in `src/core/routes.py`:

    ```python
   from yaphone.newpdater.src.prebuilt.routes import api as prebuilt_route

   def init_app(app):
       app.register_blueprint(prebuilt_route)
   ```
6. Add sources to `ya.make` file
7. Add a corresponding `tests/` directory.

   For new modules, use the new tests structure, see [Tests Wiki](https://wiki.yandex-team.ru/yandexmobile/advisor/Tests/)

#### Launch

For development purposes one can use the `mana` script.
It can be more convenient to move it to ~/bin:

`cp $ARC_ROOT/yaphone/utils/manascript/mana ~/bin/mana`

It will read the `mana.conf` file and launch every command as well.

*To build and launch using `manage.py`:*
```bash
./mana manage [params]
# e.g.
./mana manage shell
```

*To build and launch using `gunicorn.py`:*
```bash
./mana start [params]
# e.g.
./mana start --config=./etc/gunicorn/config.dev.py
```

*Just launch a previous build with `manage.py`:*
```bash
./mana [params]
# e.g.
./mana shell
```

*Build package:*
```bash
./mana build
```

*Build docker:*
```bash
./mana docker
```

*Build and run docker:*
```bash
./mana rundocker
```

This will build a server **without** usage of `deploy/gunicorn/config.py`!

*Make migrations*

First check the current migration of the base:
```bash
./mana db current
```
If the result is empty use ```stamp``` to set it. To make and apply new migration:
```bash
./mana db migrate --rev-id 1234 -m "Migrating this"
./mana db upgrade
```

#### Test

[Updater Protocol](https://wiki.yandex-team.ru/yandexmobile/advisor/protocol/updater/v2/)

[App Store Protocol](https://wiki.yandex-team.ru/tv-android/app-store/)

To see updater's outputs, one can use Insomnia app and import updater's workspace, see [info/](info/) directory.

To run tests one can run

```bash
./mana test
```

This will run `ya make -tt` with additional flags, added in `mana.conf`
