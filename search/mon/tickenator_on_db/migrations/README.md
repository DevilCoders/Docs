Alembic automated tool to generate and apply migrations.

Usage:
1. Build alembic:
run `ya make alembic` from `search/mon/tickenator_on_db`.
2. Create new migration:
    - specify DB_URL environment variable (use production url database url to compare current model definition and production DB schema).
    - run `./alembic.sh revision --autogenerate -m "<Migration name, (add new curator column, for example)>"` from `search/mon/warden`.
3. Check created migration:
Created migrations are located at `search/mon/tickenator_on_db/migrations/versions`. Name of current created migration will be at the output of alembic run.
Check that migration is correct and does not execute bad actions.
4. Finally
Everything is done, to apply migrations on any database run `./alembic.sh upgrade head` (migrations will be applyed on database specified in DB_URL environment variable).
