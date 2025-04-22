## Setting up environment
Install %%alembic%% and %%yandex-passport-vault-client%%

Database credentials:
https://wiki.yandex-team.ru/users/orphean/pano-admin/

Copy-paste connection string to run commands as follows:
> host= port= dbname= user= password= alembic ...

## Making changes

1. Modify SQLAlchemy ORM at ../pylibs/db
   If new model was added, import it in ./env.py and in ../tools/create_db/main.py

2. Add version, change if needed
> alembic revision -m "baseline" --autogenerate

3. Modify SQLChemistry ORM at ../libs/db

4. Apply head version
> alembic upgrade head
