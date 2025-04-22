# Reactive Subscriptions

## Structure

- `subscriptions-micro-core` - publishable library containing data model, very lightweight and may
  be used by other services freely
- `subscriptions-core` - local library containing main matching mechanism
- `subscriptions-storage` - library module containing DAO implementations
- `subscriptions-api` - deployable HTTP API for subscriptions CRUD
- `subscriptions-matcher` - deployable app for accepting documents (events) and matching them on
  subscriptions
- `subscriptions-notifier` - deployable app for accepting matched documents on subscriptions,
  aggregating notifications and delivering them
- `subscriptions-controller` - deployable app for running periodic tasks

## Local build

`sbt <project_name>/clean`

`sbt <project_name>/compile`

`sbt <project_name>/test`

where `project_name = {api | controller | matcher | notifier }`

## Deploy

Run the corresponding task
in [TC](https://t.vertis.yandex-team.ru/project/VerticalsBackend_Subscriptions?branch=%3Cdefault%3E&buildTypeTab=overview&mode=builds#all-projects)

## Integration with IntelliJ IDEA

To turn on scalastyle: copy `scalastyle_config.xml` to `.idea`.
