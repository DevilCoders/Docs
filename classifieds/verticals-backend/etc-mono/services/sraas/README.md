## Projects description

Schema registry as a service

### Custom proto options

Now options are installed manually, so on any option change one should update schema-registry dependency and deploy a new version of sraas-api.
To work with extensions they should be registered in sraas client's extension registry: [example](../broker/core/src/main/scala/ru/yandex/vertis/broker/sraas/source/BrokerSraasSchemaCache.scala)
