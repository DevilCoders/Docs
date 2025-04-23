# @yandex-fleet/i18n

Set of locale-sensitive formatters and i18n configuration for fleet-web monorepo.

## TL;DR <!-- omit in toc -->

Internationalization is based on the [i18next](https://www.i18next.com/) framework.

Translations are stored in [Tanker](https://tanker.yandex-team.ru/?project=fleet).

---

## Table of Contents <!-- omit in toc -->

- [@yandex-fleet/i18n](#yandex-fleeti18n)
  - [Setup](#setup)
  - [Usage](#usage)
  - [Package structure](#package-structure)
  - [Main concepts](#main-concepts)
    - [Tanker](#tanker)
    - [Language switching](#language-switching)
    - [Adding a new keyset](#adding-a-new-keyset)
    - [Plurals](#plurals)
      - [Mapping from `Tanker` plurals to `i18next`](#mapping-from-tanker-plurals-to-i18next)
      - [Comparison of plural forms for languages supported by `fleet-web` monorepo](#comparison-of-plural-forms-for-languages-supported-by-fleet-web-monorepo)
    - [Formatters](#formatters)
      - [formatUnit](#formatunit)

## Setup

Get your Tanker token at <https://nda.ya.ru/3SjQY7> and set is as an environment variable in `.env.local`

```shell
TANKER_TOKEN=...
```

To pull translations from Tanker, run:

```shell
yarn pull <keyset>
```

or if you are at the monorepo's root:

```shell
yarn i18n:pull <keyset>
```

or, to pull all keysets

```shell
yarn i18n:pull --all
```

> NOTE: only keysets and keys mentioned in [keysets.ts](src/keysets.ts) module will be pulled.

To get keys that need translations in Tanker:

```shell
yarn i18n:untranslated <lang>
```

Example

```shell
yarn i18n:untranslated ru en
```

or, to get all langs

```shell
yarn i18n:untranslated
```

The result will be saved to the directory "need_translate".

## Usage

```tsx
import React from "react";
import { useTranslation } from "@yandex-fleet/i18n";

const MyComponent = () => {
  const { t } = useTranslation("i18nKeyset");
  const translated = t("i18nKey");

  return <h1>{translated}</h1>;
};

export default MyComponent;
```

## Package structure

| Name            | Description                                               |
| --------------- | --------------------------------------------------------- |
| src/format\*/\* | Locale-sensitive formatters                               |
| src/keysets.ts  | Config with all keysets and keys used across the monorepo |
| src/i18next.ts  | `i18next` config                                          |
| src/pull.ts     | Script for pulling translations from `Tanker`             |
| src/\*          | Other source files including helper hooks, etc            |
| translations/\* | Translations pulled from `Tanker`                         |

## Main concepts

### Tanker

[Fleet Web Tanker project](https://tanker.yandex-team.ru/?project=fleet)

[Tanker Quickstart](https://doc.yandex-team.ru/Tanker/general-info/concepts/quickstart.html)

### Language switching

[Language switching](../ui/src/components/Menu/LangSwitcher/LangSwitcher.tsx)
is based on `i18n.changeLanguage()` method.

### Adding a new keyset

Add a new keyset with keys to [keysets](src/keysets.ts) config.
You can see existing keysets in our
[Tanker project](https://tanker.yandex-team.ru/?project=fleet).

```ts
// src/keysets.ts

const keysets: Record<string, Set<string>> = {
  new_keyset: new Set(["first_key", "second_key"]),
};
```

> Do not forget to pull newly created keyset from `Tanker` with `yarn pull`

### Plurals

`Tanker` [supports](https://doc.yandex-team.ru/Tanker/tech-dscr/concepts/tr_keys.html#static-keys)
storing translations for plural forms under single key.
It provides four fields inside a single key to define a plural:
`none`, `one`, `some` and `many`. In the Web GUI, these fields are marked with
`0`, `1`, `2`, `5` labels correspondingly.

> Unfortunately, it seems that available fields do not cover all possible
> cases. For example, [Arabic](https://unicode-org.github.io/cldr-staging/charts/37/supplemental/language_plural_rules.html#ar) language has 5 plural forms, which could not be handled by three
> forms available in `Tanker`. Furthermore, it seems that plural fields in `Tanker` are designed
> mostly for the [Russian](https://unicode-org.github.io/cldr-staging/charts/37/supplemental/language_plural_rules.html#ru) language, which may not be suitable for other languages.

When exported to JSON, plural keys in a keyset are stored as arrays.
`i18next` framework does not support keys in the form of array.
Only string keys are supported and plurals are handled [by appending a suffix
to a key](https://www.i18next.com/translation-function/plurals).
For languages with single plural form, a plural key [must have a suffix](https://www.i18next.com/translation-function/plurals#singular-plural) `_plural`.
For languages with multiple plurals, [keys should be prefixed](https://www.i18next.com/translation-function/plurals#languages-with-multiple-plurals) with a digit corresponding
to a category from the [Language Plural Rules](https://unicode-org.github.io/cldr-staging/charts/37/supplemental/language_plural_rules.html) table.

For example, the [Ukrainian](https://unicode-org.github.io/cldr-staging/charts/37/supplemental/language_plural_rules.html#uk) language has one singular form and two plural forms:
`one`, `few` and `many`, so the plural keys should be named as follows:

```json
{
  "key_0": "1 день",
  "key_1": "2 дні",
  "key_2": "5 днів"
}
```

#### Mapping from `Tanker` plurals to `i18next`

To make translations from `Tanker` compatible with `i18next`,
plural keys are transformed from array in accordance with the following
rules:

> NOTE: such mapping seems to be inconsistent with the meaning of `Tanker`
> plural fields (e.g. fourth field means `none` in `Tanker`), so these rules
> are not final and may change in the future.

- If an array has only one item, this item is treated as simple, non-plural
  translation and is stored under an unchanged key.
- If an array has two items, the first item is stored under an unchanged key and
  is considered as a singular form by `i18next`, and the second item is
  stored under a key with `_plural` suffix added.
- If an array has from three to four items, each value from this array is stored
  under a key with a suffix `_{n}`, where `n` is an index of a value in the array.
- If an array has more than four items, an exception is thrown.

Example:

```json
{ "key": ["foo"] } -> { "key": "foo" }
{ "key": ["foo", "bar"] } -> { "key": "foo", "key_plural": "bar" }
{ "key": ["foo", "bar", "baz"] } -> { "key_0": "foo", "key_1": "bar", "key_2": "baz" }
{ "key": ["1", "2", "3", "4", "5"] } -> exception!
```

For languages with single plural form, `Tanker` plural may be filled either
for all fields, or only for `one` and `some` fields, like:

| Tanker plural field | Value                       |
| ------------------- | --------------------------- |
| none                | {{count}} events (optional) |
| one                 | {{count}} event             |
| some                | {{count}} events            |
| many                | {{count}} events (optional) |

In both cases, this will result to `["event", "events"]`
array being exported (if `all-forms` option is not set).

#### Comparison of plural forms for languages supported by `fleet-web` monorepo

| Language         | Plural forms                     |
| ---------------- | -------------------------------- |
| Russian (RU)     | one, few, many, other            |
| English (EN)     | one, other                       |
| Ukrainian (UK)   | one, few, many, other            |
| Arabic (AR)      | zero, one, two, few, many, other |
| Azerbaijani (AZ) | one, other                       |
| Estonian (ET)    | one, other                       |
| Persian (FA)     | one, other                       |
| Finnish (FI)     | one, other                       |
| French (FR)      | one, other                       |
| Hebrew (HE)      | one, two, many, other            |
| Armenian (HY)    | one, other                       |
| Georgian (KA)    | one, other                       |
| Kazakh (KK)      | one, other                       |
| Lithuanian (LT)  | one, few, many, other            |
| Latvian (LV)     | zero, one, other                 |
| Romanian (RO)    | one, few, other                  |
| Serbian (SR)     | one, few, other                  |
| Tajik (TG)       | n/a                              |
| Uzbek (UZ)       | one, other                       |

As we can see from the table above, it seems that only Arabic language
can't be supported by `Tanker` and our
[mapping rules](#mapping-from-tanker-plurals-to-i18next).

### Formatters

We're using native [Intl](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Intl)
API for locale-sensitive formatters development where possible.

#### formatUnit

As `Intl.NumberFormat` with `style: 'unit'` is not widely supported by the supported browsers,
the [polyfill](https://formatjs.io/docs/polyfills/intl-numberformat/) must be used.

Locales for this polyfill are loaded dynamically by `i18next` alongside with translations.
To achieve this, custom `request` function is used for `i18next-http-backend` plugin.

When adding a new language to the `fleet-web`, do not forget to load the corresponding locale for
this language in `loadIntlNumberFormatPolyfill` function at [formatUnit/formatUnit.ts](src/formatUnit/formatUnit.ts)
