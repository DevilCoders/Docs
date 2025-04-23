# scandex
The (**sca**)la i(**ndex**)ing engine

**WARNING!** This project is still under construction

**scandex** is a framework that aims to build and use typesafe immutable indexed database.

### Philosophy

- **Safety and soundness over flexibility** Queries, runtime databases and index builders are tied to a same singleton schema with field singletons. You can only build queries that are consistent for this schema on compile-time.
- **Query speed over mutability** scandex indexes are immutable data structures, so for updating your dataset you need to build and replace the whole partition in memory. On the bright side, it means that it's much easier to scale your application. Also, immutable data structures are easier for runtime speed optimization because you don't need to deal with mutation of data.
- **Code generation over boilerplate** Currently, scandex uses protobuf messages designated with options to infer the schema and generate code for it. Well, it's not a requirement, so you may write all of it by hand, if you want to. There are plans to extend code generation support to custom datatypes as well.

### Architecture
Basically, you can imagine scandex database as a single column-oriented table of documents. Each document may (or may not) contain fields that would be used to build column index. Each document have an immutable id that can be used to access specfic document fields.

### Typed schema
_Schema_ is a singleton object that holds fields definition for specific database. Each field is a singleton case object that extends field prototype that parametrized with data type of field and schema type it belongs to.

### Field prototypes
_Field_ may be one of listed type:
- **Storage** field only holds relation between document id and document data. It cannot be used for queries, but it is very useful for retrieving data assotiated with the document. Stored values may be also transparently compressed on serialization and deserialization.
- **Filter** field extends storage with equality operations like **=** and **IN**. Filter fields may contain multiple values for a single document.
- **Range** fields extends filter with range queries like **<**, **<=**, **>=** **>**, **BETWEEN**. Range fields cannot hold more than one value for every document.

### Composite database
Query performance and size of dataset may be balanced using sharding of data. Different shards may be used for parallel query execution or even for distributed queries. Shards can be updated in memory separately as long as sharding strategy is not changed.

### Deploy
1. Update `ThisBuild / version` in `build.sbt`.
2. Commit these changes.
3. ```sbt clean compile package publish```
4. Check if new version made it to `artifactory`.  
[snapshot example 0.1.1-SNAPSHOT](http://artifactory.yandex.net/artifactory/yandex_vertis_snapshots/com/yandex/scandex-core_2.13/0.1.1-SNAPSHOT/)  
[release example 0.1.1](http://artifactory.yandex.net/artifactory/yandex_vertis_releases/com/yandex/scandex-core_2.13/0.1.1/)
