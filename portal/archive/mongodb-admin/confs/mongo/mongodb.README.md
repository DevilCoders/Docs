### Custom role for monitoring mongodb

use admin
db.runCommand(
   {
     dropRole: "monitoring",
     writeConcern: { w: "majority" }
   }
)
db.runCommand({ createRole: "monitoring",
  privileges: [
    { resource : { cluster : true }, actions: [ "serverStatus", "listDatabases"] },
    { resource : { db : "", collection : "" }, actions: [ "dbStats", "collStats" ] },
    { resource : { db : "", collection : "system.namespaces"}, actions: [ "collStats", "find"] },
    { resource : { db : "", collection : "system.indexes"}, actions: [ "collStats" ] },
    { resource : { db : "local", collection : "system.replset"}, actions: [ "collStats" ] },
    { resource : { db : "admin", collection : "system.version"}, actions: [ "collStats" ] },
    { resource : { db : "admin", collection : "system.users" }, actions: [ "collStats" ] },
    { resource : { db : "admin", collection : "system.roles" }, actions: [ "collStats" ] },
    { resource : { db : "admin", collection : "system.profile" }, actions: [ "collStats" ] },
    { resource : { db : "local", collection : "system.profile" }, actions: [ "collStats" ] },
    { resource : { db : "rss-storage", collection : "system.profile" }, actions: [ "collStats" ] },
    { resource : { db : "stocksdb", collection : "system.profile" }, actions: [ "collStats" ] },
    ],
  roles: [
    { role: "read", db: "admin" }
  ]
})
db.grantRolesToUser( "monUser", [ { role: "monitoring", db:"admin" } ] )

use admin
db.createUser(
 {
   user: "backup",
   pwd: "_PASSWORD_",
   roles:
   [
    {
      "role" : "dbAdminAnyDatabase",
      "db" : "admin"
    },
    {
      "role" : "backup",
      "db" : "admin"
    },
    {
      "role" : "restore",
      "db" : "admin"
    }
   ]
 }
)
