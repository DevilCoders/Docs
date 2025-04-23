# Ya Courier Analytics Backend

## Useful links

* [Service README](https://a.yandex-team.ru/arc_vcs/maps/b2bgeo/ya_courier/analytics_backend/README.md)
* [Export analytics tool README](https://a.yandex-team.ru/arc_vcs/maps/b2bgeo/ya_courier/backend/tools/export_analytics/README.md)

## Projects

* [2021-Q4 План-факт анализ](https://st.yandex-team.ru/BBGEO-4968)

## System design

Ya Courier Analytics Backend service has it's own DB.
We fill this DB via export analytics tool that is managed by sedem and ran by [scheduler](https://sandbox.yandex-team.ru/scheduler/698645/view)
Than we use this data to:
* Provide data by date range filter, needed for frontend charts, `/api/v1/analytics/companies/{company_id}/plan-fact/`.
* Provide data by version, needed for external customers to export data and see what is changed since last export, `/api/v1/analytics/companies/{company_id}/plan-fact/versioned/`.
* Create excel reports by date range filter, needed for frontend excel generation.

Diagram:
@startuml
component analytics_backend
component "auth_service(YCB)" as auth
node export_analytics
cloud S3
database CourierDB
database AnalyticsDB

export_analytics <.. CourierDB : monitoring data
export_analytics ..> AnalyticsDB : aggregated data
note left of export_analytics
  Sandbox-task
  runs every day
end note


analytics_backend --> AnalyticsDB : use data
analytics_backend --> AnalyticsDB : manage excel-reports
analytics_backend -> auth : authorize requests
analytics_backend --> S3 : store excel-reports
@enduml

### Service design

#### Components

It is divided into following components/folders:
* `bin` - pycare binary with all routes.
* `bin/tests` - tests for the whole binary, they are synchronous.
* `test_lib` - common lib for all tests, contains basic data to put into the database.
* `tests/mypy` - type-checker for lib folder.
* `tests/postgres_ut` - tests for infra components that interact with the database.
* `lib/resources` - basic implementation of routes logic, called only from `bin`.
* `lib/background_tasks` - basic implementation of background tasks that are forked from the main binary.
* `lib/plan_fact` - plan fact logic that is common and doesn't depend on infrastructure.
* `lib/reports/common` - components that are needed to implement any report system, contains interfaces that are needed for this to work.
* `lib/reports/plan_fact` - excel-specifics to format plan-fact excel-report with all needed data.
* `lib/db` - database schema and implementation of getters to load all needed plan-fact data.
* `lib/infra` - implementation of interfaces that are interacting with all external components like S3, Auth-Service, DB.

Every folder has it's own ya.make. Dependencies are managed by ya.make PEERDIRs.
All dependencies shall be directed from infrastructure to the logic.

You can see that all dependencies are directed down:
@startuml
package bin {}
package background_tasks {}

package db {}
package infra {}
package resources {}

package plan_fact {}
package reports {}

bin -> background_tasks : forks
background_tasks --> infra : setups
bin --> infra : setups

infra -> db : setups
bin --> resources : HTTP calls

infra --|> reports : implements interfaces
db --|> plan_fact : implements interfaces

resources --> plan_fact : uses
resources --> reports : uses

background_tasks -> reports : polls/generates

@enduml

#### Excel generation

We use forked processes to do all background work and generate excel-reports for us.

Why DB queue is chosen?
We considered using SQS for queue, but you can see that all functions except mark_inactive_tasks
would have been the same if that was the case, so for us it's not really viable to use separate queue.
SQS is good as an alternative to APIs for messaging between services. When you do the queue inside the
service and you need to maintain correct status and keep visibility of the task in the DB, it's not that good.

In future we can replace DB-based implementation with SQS/DB mixup, because we already have hidden our implementation behind an interface.
But right now we decided to use DB-based solution.


### Export analytics tool

#### Components

It is divided into following components/folders:
* `bin` - minimal binary implementation
* `task` - sandbox task managed by sedem
* `lib/plan_fact` - plan fact aggregation logic, also has interface that it needs to load the data from courier database
* `lib/courier_db` - implementation of the interface to load data from courier database, all interaction with YCB db is there
* `lib/analytics_db` - implementation of analytics database methods, just stores all aggregated data into the DB
* `lib/db_common` - some utils that are common for both databases

Every folder has it's own ya.make. Dependencies are managed by ya.make PEERDIRs.
All dependencies shall be directed from infrastructure to the logic.

You can see that all dependencies are directed down:
@startuml
object "bin/task" as executables

package plan_fact {
  object CourierStorageInterface
  object AnalyticsStorageInterface
  object Entities
  object export
}

package infra {

package analytics_db {
  object AnalyticsDb
}

package courier_db {
  object CourierDb
}
}

executables --> AnalyticsDb : setups
executables --> CourierDb : setups
executables --> export

CourierDb --|> CourierStorageInterface : implements
AnalyticsDb --|> AnalyticsStorageInterface : implements
AnalyticsDb --> Entities : uses
@enduml

#### Some implementation points

* Every object has:
    * id - just unique primary key.
    * version - version when this object was updated, it shalln't be returned to the user as date, but as some arbitrary string.
    * start_version - version when this object was created.
    * deleted - is this object deleted or not, we do not delete objects that were deleted in YCB, we just mark them as deleted.
* When object is deleted in some version and user comes with older version where this object exists, we shall somehow show the user that this object became deleted.
* (not-implemented) Version shall be updated only for changed routes, but it's route-based, so, if the node is changed, the whole route is changed as well.
* Routes are loaded based on `Route.date` field without considering real route start and finish
* Plan fact entities described here are structured in a way that is convenient for this tool only, it'll probably be better if analytics service, that uses this data, implements their own structural approach.

#### Some restrictions of the tool

* It follows very easy way of matching plan and fact nodes: we can just match them to the first order in both lists. So, some routes will have wrong matching.
* Note that in general this tool gets some info from YCB calculated data and some data it calculates itself, so there can be a mismatch in case of incorrect/changed data.


### Auth Service

This service is needed to authorize requests from analytics_backend, because analytics_backend itself doesn't know anything about users.

How to use it:
* pass cookies or OAuth token;
* request what is available to the current user in some subtree;
* filter response or deny request based on what objects are available.

Right now only companies are supported, and it's done not via tree search, but via our usual YCB-database.

More info is available at [the wiki page](https://wiki.yandex-team.ru/users/matrohin/auth-service/)

#### Example

Auth service state for YCB scenario:

@startuml
node "company:6" as c6
node "depot:123" as d6_123
node "shared_company:6:7" as s6_7
node "zone:3" as z6_3

actor alice
actor bob


d6_123 <-- c6 : parent
s6_7 <-- c6 : parent
z6_3 <-- c6 : parent

alice -> c6 : admin
alice -.-> c6 : permission:write
alice -.-> c6 : permission:read

bob -> c6 : manager
bob -> s6_7 : logistician
bob -.-> s6_7 : permission:read
bob -> z6_3 : editor
bob -.-> z6_3 : permission:read
bob -.-> z6_3 : permission:write
@enduml


Example of usage:

```
# Alice asks:
/api/v1/internal/auth/objects/search?permission=read&root_type=company&root_id=6

# Alice receives:
[
    {
        type: "company",
        id: "6"
    }
]
```
