# YDL
(yet another) timeline service.

[Documentation](https://wiki.yandex-team.ru/jandekspoisk/sepe/YaDeLorean/) |
[UI](https://github.yandex-team.ru/YAPPY/YDL-UI) |
[CI](https://sandbox.yandex-team.ru/tasks?type=BUILD_YDL)

### Installation
Checkout source code:

```bash
git clone git@github.yandex-team.ru:YAPPY/YDL.git
```

Create and activate virtualenv: 

```bash
virtualenv -p $(which python3.6) ENV
source ENV/bin/activate
```

Install requirements:

```bash
pip install -f wheel -i https://pypi.yandex-team.ru/simple -r requirements.txt
```

**Warning:** any settings configuration other than `ydl.settings.local` requires Postgres dev libraries to be installed.

### Running
```bash
python src/manage.py runserver --settings ydl.settings.dev
```

### Testing
```bash
python src/manage.py test --settings ydl.settings.build
```

### Using Yandex auth
If you want Yandex auth to work, make sure your backend can be accessed within **yandex-team.ru** zone.

### Settings loaded from env
| Variable                 | Description                                                         |
| ------------------------ | ------------------------------------------------------------------- |
| `ALLOWED_HOSTS`          | Comma-separated list of allowed hosts, use "*" to allow any host    |
| `YDL_SECRET_KEY`         | Django secret key.                                                  |
| `YDL_LOGGING_FILENAME`   | Filename for logging.                                               |
| `YDL_LOGGING_FORMAT`     | `{` styled logging format.                                          |
| `YDL_LOGGING_MODE`       | Logging mode (`stream`, `file_a`, `file_ra`, `file_w`, `file_rw`).  |
| `YDL_LOGGING_LEVEL`      | Logging level: (`DEBUG`, `INFO`, `WARNING`, `ERROR`).               |
| `YDL_VERSION_FILE`       | Version file.                                                       |
| `YDL_REVISION_FILE`      | Revision file.                                                      |
| `YDL_BUILD_ID_FILE`      | Build id file.                                                      |
| `YDL_DB_USER`            | PGaaS username.                                                     |
| `YDL_DB_PASSWORD`        | PGaaS password.                                                     |
| `YDL_DB_CERT_PATH`       | PGaaS certificate.                                                  |
| `YDL_NANNY_OAUTH`        | OAuth token for nanny.yandex-team.ru.                               |
| `YDL_DEV_NANNY_OAUTH`    | OAuth token for dev-nanny.yandex-team.ru.                           |

**Note:** No settings are required for local run. However, Nanny tokens are required for fetchers to run.

### CI

Any branch pushed to GitHub repository will be automatically built and tested by
[Sandbox](https://sandbox.yandex-team.ru/tasks?type=BUILD_YDL).
Release sandbox tasks after successful build to deploy.

**Attention:** `stable` sandbox releases are automatically deployed to production.
Migrations are not applied during release.
If you need to apply migrations,
do so before release and make sure currently deployed version can work with new database state.
