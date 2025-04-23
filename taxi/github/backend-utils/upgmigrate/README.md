# PG migrate for microservices

The PostgreSQL migration tools derive from https://github.com/yandex/pgmigrate utility, but they were modified according to the needs of microservices. The main difference from the original pgmigrate is that it stores schema version table not in `public` schema, but in an arbitrary schema that is passed via command-line arguments or is specified in the config file. Also, a default schema can be specified in config file or command-line arguments, so the same sql script can be run in different schemas in the same database for 'logical' sharding.

## cluster-migrate

`cluster-migrate` is a tool for applying database migrations to PostgreSQL clusters using connection information from `secdist`. The tool will apply migrations to all 'physical' shards listed in the `secdist` file. Deployment to 'logical' or 'virtual' shards (different schemas in the same physical database) is also supported.

### Configuration of shard-migrate

The configuration file is in yaml format and can contain the following:

```yaml
# Path to the secdist file, this is the default value
secdist: /etc/yandex/taxi-secdist/taxi.json
# alias of database in the secdist file
dbalias: mydb
# configuration of logical shards, see below
logical-shards:
    - [schema0, schema1, schema2]
# configuration for migrating a schema in each logical shard
per-shard-config: migrations.yaml
# configruation for migrating the common schema
common-schema-config: common-schema.yaml
```

#### Logical shards

Logical or virtual sharding is storing the same structure of tables in different schemas within a single physical database, so that a schema can be later moved to a different physical instance. The `cluster-migrate` utility supports applying migration scripts to multiple schemas within a database given that the SQL script doesn't reference a schema directly, for example, our migration script creates a table:

```sql
create table my_table (
    id bigserial primary key
);
```

When logical shards are configured as, say, `schema0`, `schema1` and `schema1` for physical shard 0, the script executed at the physical instance will be similar to the following:

```sql
-- schema0
create table schema0.my_table (
    id bigserial primary key
);

-- schema1
create table schema1.my_table (
    id bigserial primary key
);

-- schema1
create table schema1.my_table (
    id bigserial primary key
);
```

For those cases where the schema's name is required, e.g. for granting, the tool provides substituting the `{current_schema}` variable with the actual name of current schema in the text of the query.

```sql
grant usage on {current_schema} to taxiro;
```

To configure logical shards in a physical cluster, the yaml configuration for the database should contain `logical-shards` parameter. It **MUST** be a yaml array of arrays of schema names, the top level array size **MUST** match the number of physical shards for the alias in `secdist` file. For each physical instance an arbitrary list of schema names can be specified. The names of 'logical' shards will be used as parameters for `information-schema` and `use-schema`.

```yaml
#...
logical-shards:
    - [schema0, schema1, schema2]
    - [db1, db2, db3]
#...
```

#### Common schema

When there are multiple logical shards (aka schemas with the same structure) in a physical instance, a problem with user datatypes arises. When created in different schemas with the same definition the user types will have the similar definition, but they will actually be different incomatible types which will prevent cross-schema selects, updates et al. Also it will complicate data type mapping for clients with strict static type system. To overcome this nuisance one can create datatypes in a separate 'shared' schema and reference those types explicitly in logical shard schema objects.

```sql
-- common schema
create type common.point as (
    x real,
    y real
);

-- script for sharded table
create table my_table (
    location common.point
);

```

The script for creating the common schema should be run once, so the migration scripts for the common schema should be kept separate from scripts for logical shards, as they may be run multiple times on the same database with diffferent schema settings. Common schema migration is the same as migration of shard schemas, but it is applied before the migration of other schemas. One can keep directories for both common schema and sharded schemas in the same root directory and share grant scripts for all schemas.

#### Possible scenarios

##### The simpliest scenario, single physical cluster, no logical shards

In the simpliest and most common scenario there is a single PGaaS cluster. The only advantage of `cluster-migrate` tool over `shard-migrate` is that it uses secdist for connection strings, for configuring `shard-migrate` see below.

**Directory layout**
```bash
your_alias              # root directory
├── grants              # use this dir to set special callbacks for grants
│   ├── taxiro.sql
├── migrations          # shard migrations dir
│   ├── V0001__description.sql
│   ├── V0002__description.sql
│   ...
│   ├── V000n__description.sql
├── migrations.yaml     # shard-migrate shard configuration
├── cluster.yaml        # configuration for the cluster-migrate tool
```

**cluster.yaml**
```yaml
# Path to the secdist file, this is the default value
secdist: /etc/yandex/taxi-secdist/taxi.json
# alias of database in the secdist file
dbalias: mydb
# configuration for migrating a schema, migrations.yaml is the default value, may be omitted
per-shard-config: migrations.yaml
```

There is no use to specify `conn` here, it will be substitued from secdist.

**migrations.yaml**
```yaml
information-schema: my_schema
migrations-dir: migrations # this is the default value, can be omitted
callbacks:
    afterAll:
        - grants
```

##### Multiple physical clusters, no logical sharding

There is no difference from a single physical cluster, the same migrations will be run on multiple physical instances stated in secdist.

##### Logical sharding, no common schema

What is needed to be added here is the configuration of logical shard per physical instance. This configuration goes to the `cluster.yaml` configuration file. The number of elements in the `logical-shards` array **MUST** match the number of physical clusters in the `secdist` file.

```yaml
#...
logical-shards:
    - [schema0, schema1, schema2]
    - [db1, db2, db3]
#...
```

##### Logical sharding, common schema

Common schema is migrated exactly the same way as other schemas are, the only trick is to keep it's migration scripts together with other database schema. The common schema will require a separate yaml configuration, which should state the schema name and the directory containing the common schema migration scripts. The cluster yaml configuration will also require some tweak.

**Directory layout**
```bash
your_alias              # root directory
├── common              # common schema migrations dir
│   ├── V0001__description_common.sql
│   ├── V0002__description_common.sql
│   ...
│   ├── V000n__description_common.sql
├── grants              # use this dir to set special callbacks for grants
│   ├── taxiro.sql
├── migrations          # shard migrations dir
│   ├── V0001__description.sql
│   ├── V0002__description.sql
│   ...
│   ├── V000n__description.sql
├── common.yaml         # shard-migrate configuration for common schema
├── migrations.yaml     # shard-migrate shard configuration
├── cluster.yaml        # configuration for the cluster-migrate tool
```

**common.yaml**
```yaml
information-schema: common
use-schema: common          # defaults to the value stated in information-schema
migrations-dir: common      # the scripts must be kept in a separate directory
callbacks:
    afterAll:
        - grants
```

**cluster.yaml**
```yaml
# Path to the secdist file, this is the default value
secdist: /etc/yandex/taxi-secdist/taxi.json
# alias of database in the secdist file
dbalias: mydb
# configuration for migrating the common schema
common-schema-config: common.yaml
# configuration for migrating a schema, migrations.yaml is the default value, may be omitted
per-shard-config: migrations.yaml
```

**migrations.yaml** the same as without the common schema.


## shard-migrate

### Configuration for shard-migrate

The configuration file is in yaml format and can contain the following:

```yaml
conn: 'postgres connection string'
migrations-dir: 'directory with migration files, relative to this file, by default "migrations"'
information-schema: 'schema to store the shard-migrate `schema_version` table, by default "public"'
use-schema: 'schema to be used as a default. Will be created if it doesn\'t exist,'
            ' if not specified - the value `information-schema` is set to'
session: 'session setup string'
callbacks: # Directories containig scripts that are run each migration
    beforeAll: # Directories containing scripts that are run before all scripts
        - directory
        - directory
    beforeEach: # Directories containing scripts that are run before each script
        - directory
        - directory
    afterEach: # Directories containing scripts that are run after each script
        - directory
        - directory
    afterAll: # Directories containing scripts that are run after all scripts
        - directory
        - directory
```

All options in the config file can be overriden in the command line. Additionally there are the following command-line options:

```bash
--base-dir Root directory containing the configuration file and migration directories.
--config-file Name of the YAML configuration file. By default `migrations.yml`.
--target Number of version to migrate to. A number or `latest`
```

The full list of command-line options is available by running `shard-migrate.py -h`

### shard-migrate commands

The `shard-migrate` utility is intended to apply migration scripts to a single 'logical' shard in a single physical database. Available commands are `migrate`, `info`, `baseline` and `clean`.

#### info

Output information about available migrations.

```bash
shard-migrate.py info
```

Possible output can be as follows:

```json
{
    "1": {
        "installed_by": "foo",
        "description": "Initial schema foo",
        "version": 1,
        "transactional": true,
        "installed_on": "2019-07-10 14:10:55",
        "type": "auto"
    },
    "2": {
        "installed_by": "foo",
        "description": "Add baz column to foo",
        "version": 2,
        "transactional": true,
        "installed_on": "2019-07-10 14:10:59",
        "type": "auto"
    },
    "3": {
        "installed_by": null,
        "installed_on": null,
        "version": 3,
        "transactional": false,
        "description": "NONTRANSACTIONAL Add index on baz column",
        "type": "auto"
    }
}
```

The versions applied are marked by timestamps they were install and by the database user who run the migration.

#### migrate

Migrate schema version to the specified version. When bumping the version for more than one, the scripts will be applied one by one. 

```bash
shard-migrate.py migrate -t 1      # first version
shard-migrate.py migrate -t latest # latest available version
```

#### baseline

If you already have a database with schema on some certain version, you can run the baseline command to mark that the database already contains the required schema.

```bash
shard-migrate.py baseline -b 2     # mark the database contains schema with version 2
```

#### clean

Remove schema version information

```bash
shard-migrate.py clean
```

### More advanced scenarios

To apply the same migrations to a number of schemes in one go, the `shard-migrate` can be used as follows:

```bash
for i in `seq 0 3`; do
    shard-migrate.py -t latest migrate -i my_schema_$i
done
```

This command will apply all migration scripts to schemas `my_schema_0`, `my_schema_1`, `my_schema_2` and `my_schema_3`.

For the SQL commands to work correctly, the commands shouldn't reference database objects with schema-qualified names. The objects in current schema will be used. Where a schema name is required, e.g. in grant statements, the schema name can be referenced as `{current_schema}`.

#### UTF-8 Migrations

In most cases you should avoid non-ascii characters in your migrations. So PGmigrate will complain about them with:
```
pgmigrate.MalformedStatement: Non ascii symbols in file
```

But sometimes there is no way to avoid migration with UTF-8 (imagine a case with inserting some initial data in your database). You could insert modeline in migration file to disable non-ascii characters check:
```
/* pgmigrate-encoding: utf-8 */
```

#### Session setup

Sometimes you need to set some session options before migrate (e.g. isolation level). It is possible with `-s` option or `session` in config. For example to set `serializable` isolation level and lock timeout to 30 seconds one could do something like this:
```
shard-migrate.py -s "SET SESSION CHARACTERISTICS AS TRANSACTION ISOLATION LEVEL SERIALIZABLE" \
    -s "SET lock_timeout = '30s'" ...
```

#### Terminating blocking pids

On heavy loaded production environments running some migrations could block queries by application backends. Unfortunately if migration is blocked by some other query it could lead to really slow database queries. For example lock queue like this:
```
<lots of app backends>
<pgmigrate>
<stale backend in idle in transaction>
```
makes database almost unavailable for at least `idle_in_transaction_timeout`. To mitigate such issues there is `-l <interval>` option in pgmigrate which starts separate thread running `pg_terminate_backend(pid)` for each pid blocking any of pgmigrate conn pids every `interval` seconds. Of course pgmigrate should be able to terminate other pids so migration user should be the app user or have `pg_signal_backend` grant. To terminate superuser (e.g. `postgres`) pids one could run pgmigrate with superuser.

Note: this feature relays on `pg_blocking_pids()` function available since PostgreSQL 9.6.

