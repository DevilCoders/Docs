# @yandex-fleet/ui

The collection of React components specific to `@yandex-fleet` monorepo.

## Adding new components

This package is intended for reusable components that do not fall under the consept of a
_basic_ component. A component might be considered _basic_ if it meets the following
criterias:

- it is a general interface element (like `checkbox` or `button`)
- it does not depend on something app-specific like i18n or routing packages

If you are writing a component that is not _basic_ (or quite simple)
and it ~~can~~ should be re-used between different packages inside `@yandex-fleet` monorepo, you're on the right way.
Otherwise, please consider putting your component in `@yandex-fleet/yandex-go` package.

Please follow [same rules](../yandex-go/CONTRIBUTING.md) as described in `@yandex-fleet/yandex-go` when adding a component.
