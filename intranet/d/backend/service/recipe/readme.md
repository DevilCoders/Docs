# Recipe to setup resource model backend in integration tests
This recipe launches stable YDB instance and resource model backend instance.
This recipe sets `RECIPE_HTTP_PORT` and `RECIPE_GRPC_PORT` environment variables on successful launch. Resource model backen listens on these ports.
Either `X-Ya-Uid` (passport uid of the user) or `X-Ya-Service-Id` (TVM id of the service) header must be set for endpoints requiring authentication.
By default there is a single user with maximum permissions, uid is 2120000000000001.
Also by default there are three ABC services with ids 1, 2 and 3.
No providers are present by default. When creating a new provider set grpcTlsOn property to false unless it's GRPC endpoint provides TLS.
To include the recipe just add
```
INCLUDE(${ARCADIA_ROOT}/intranet/d/backend/service/recipe/recipe.inc)
```
to ya.make.

