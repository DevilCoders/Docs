# Debby Console is a web interface to create and manage debby scans.


## Development with docker compose
* Just build: `docker compose build`
* Just run: `docker compose up -d`
* Rebuild and run: `docker compose up --build -d debby-console`


## Deploy
1. `sudo make releasedev` or `sudo make releasestable`
2. Update image tag/version in stage config for preprod/dev or prod/stable: https://deploy.yandex-team.ru/stages/debby-stage


## Steps to add new engine
1. Add new engine to `setting.py` file to "ENGINES" section. Add new engine to "ENGINES" list. If you want to make it accessible from api - then add to "API_ENGINES" list.
2. Implement console-side handler for new engine. Add new file in `src/app/engines`. You can take as a basis other already implemented engines handlers.
3. Add new engine to `src/app/engines/__init__.py` file.

Example of adding support for yandexpay_iframe_checker engine: https://github.yandex-team.ru/security/debby_console/commit/9dc3c0e9d45247dff2a84aa13fa4cf3514743ff5


## Environment Variables
All variables are in `app/settings.py`
##### Secrets
* MOLLY_OAUTH_TOKEN - robot token to go to Molly
* DEBBY_TVM_TICKET - tvm server ticket when debugging not in qloud (cant go localhost:1/tickets and get ticket)
* DEBBY_HEC_TOKEN - Token to access splunk and send scan logs
* DEBBY_DB_URLS - List of full urls for all instances in json format: ["postgresql://user:pass@host:port/database", ...] **(default: ["postgresql://ivre_user:ivre_pass@localhost:5432/ivre_db"])**
##### ENVs
* DEBBY_DB_VERIFY_FULL - use sslmode=verify-full or not. **[default:'False']**
* DEBBY_SKIP_YAUTH - use blackbox authentication **[default:'False']**
* DEBBY_SITE - site where to redirect user after blackbox authentication **[default:'https://debby.sec.yandex-team.ru']**

# IMPORTANT NOTES
1. On new db you need to use: `python manage.py initdb`
2. Optionally you can fill it some tags and policies: `python manage.py filldb`
3. To reinitialize db use: `python mange.py refreshdb`

## ENVIRONMENTS

### Locally
* If you need local database run it: `docker/db$ sudo make run`. Url: `postgresql://ivre_user:ivre_pass@localhost:5432/ivre_db`
* If you want to use remote db, set DEBBY_DB_URL and DEBBY_DB_VERIFY_FULL.
##### W/O Docker
```
terminal1-src$ python manage.py runbeat
terminal2-src$ export DEBBY_HEC_TOKEN=XXXXX
terminal2-src$ export ...
terminal2-src$ python manage.py runworker
terminal3-src$ export FLASK_APP=app
terminal3-src$ export FLASK_ENV=development
terminal3-src$ export FLASK_DEBUG=1
terminal3-src$ flask run
```
###### Example with local db
```
terminal1-docker/db$ sudo make run
terminal2-src$ python manage.py runbeat
terminal3-src$ export DEBBY_HEC_TOKEN=XXXXXXXXXX_TEMP_INDEX_SPLUNK_XXXXXXXXXX
terminal3-src$ export ...
terminal3-src$ python manage.py runworker
terminal4-src$ export FLASK_APP=app
terminal4-src$ export FLASK_ENV=development
terminal4-src$ export FLASK_DEBUG=1
terminal4-src$ flask run
```
##### Docker
*Checkout Makefile and set envs:*
* DEBBY_DB_URL
* DEBBY_DB_VERIFY_FULL
* DEBBY_HEC_TOKEN
* MOLLY_OAUTH_TOKEN


## RUN TESTS
* Just run
`src$ python -m pytest`
* Show slowest tests
```
src$ python -m pytest --duration=0
src$ python -m pytest --duration=10
```

## How to create new table
1. Write ORM
2. import table and create it
```
from app.db.models import Base
from app.db.models import PortCache
from app.db.db import new_session
s = new_session()
c = s.connection()
engine = c.engine

PortCache.__table__.create(bind=engine, checkfirst=True)
```
3. Drop table
```
PortCache.__table__.drop(bind=engine, checkfirst=True)
```



