# Authentication and authorization

## Links

* [Authentication and Authorization, info about keycloak](https://wiki.yandex-team.ru/b2bgeo/dev/aws/authentification-and-authorization)
* [Схема авторизации в Keycloak, authorization flow, a bit outdated](https://wiki.yandex-team.ru/b2bgeo/dev/aws/authentification-and-authorization/sxema-avtorizacii-v-keycloak)
* [Auth service, initial design of authentication/authorization service](https://wiki.yandex-team.ru/b2bgeo/dev/aws/authentification-and-authorization/auth-service/)


## Projects

* [Обеспечить работу планирования через UI в AWS](https://st.yandex-team.ru/BBGEO-13417)
* [C2S Authorization in AWS](https://st.yandex-team.ru/BBGEO-13674)
* [Сервис аутентификации в AWS](https://st.yandex-team.ru/BBGEO-13549)


## Authorization high-level design

On a high-level there are following components in our system:
* keycloak ([auth.routeq.com](https://auth.routeq.com/)) - authenticates users from external social networks, manages access and refresh tokens.
* auth-proxy ([api.routeq.com](https://api.routeq.com/)) - API Gateway to all our services.
* identity - provides JWT with companies, roles, etc to use in all other services based on:
    * JWT from keycloak with login/uid information, used in frontend
    * apikey, used to access an API from another server
* other services - use JWT from identity to authorize user requests.
* "User" and "Company" - C2S and S2S authentification correspondingly.

There are 3 types of authorization tokens:
* apikey+signature (or just apikey if company is in [the list](https://us-east-2.console.aws.amazon.com/secretsmanager/secret?name=authorization%2Fapikeys-not-to-check&region=us-east-2) - S2S authorization, effectively it's an admin in some company.
* k-jwt - JWT from keycloak, user can get it by logging into the social network (e.g. google), lives for a long time, can be refreshed via refresh-token.
* i-jwt - JWT from identity, never shown to a user, i-jwt is only applicable for a short time to process one HTTP request to our system.

{% include [Components](_includes/components.wsd) %}

### C2S (client-to-server) auth

All C2S interaction with our API is managed via keycloak JWT tokens.

{% include [C2S](_includes/c2s_auth.wsd) %}


### S2S (server-to-server) auth

All S2S interaction with our API is managed via apikey+signature. Signature is checked on auth-proxy component.

{% include [S2S](_includes/s2s_auth.wsd) %}

## Common components

Note that common components are kind of all over the place right now and we need to move them to appropriate places later.

To provide such auth-workflow for all services we've developed common components to use in all client-services:
* Authorization libraries for client-services:
    * [auth](https://a.yandex-team.ru/arcadia/maps/b2bgeo/identity/libs/auth) - `identity` yacare parameter and common authorization utils.
    * [py_auth](https://a.yandex-team.ru/arcadia/maps/b2bgeo/libs/py_auth) - `IdentityResource`-s and authorization decorators.
* Payloads - payloads of different JWT (keycloak or identity):
    * [identity-payloads](https://a.yandex-team.ru/arcadia/maps/b2bgeo/identity/libs/payloads) - `Identity` payload can be either User or Company that is accepted in a client-service from i-jwt.
    * [keycloak-payloads](https://a.yandex-team.ru/arcadia/maps/b2bgeo/libs/jwt-lua/lib/keycloak_user.h) - `KeycloakUser` from k-jwt is used in tests and in identity service.
* JWT parsing (probably should not be used directly, consider using auth libraries above):
    * [jwt](https://a.yandex-team.ru/arcadia/maps/b2bgeo/libs/jwt) - main library for JWT issuing and verifying.
    * [jwt/py](https://a.yandex-team.ru/arcadia/maps/b2bgeo/libs/jwt/py) - port of jwt library for python.
    * [jwt-lua](https://a.yandex-team.ru/arcadia/maps/b2bgeo/libs/jwt-lua) - port of jwt library for lua.


## Identity

### Structure
* `bin` - the binary implementation.
    * `tests` - binary tests, note that all tests are run against memory and DB storages via parametrized fixtures.
* `common` - common utlities and exceptions.
* `db` - implementations of DB and memory storages, they can be used interchangeably.
* `resources` - identity API endpoints.
    * `common` - common yacare utilities
    * `tokens` - API of getting tokens from apikey or keycloak JWT.
    * `companies/users` - normal API for companies and users, accepts i-jwt.
* `tests` - unit-tests.
* `tokens` - token creation logic.

### Database

![DB schema](_includes/db_schema.svg "DB schema")

Migrations are managed via pgmigrate, [see more info here](https://a.yandex-team.ru/arc_vcs/maps/b2bgeo/identity/db/README.md).
