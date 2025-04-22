# zoneinfo

zoneinfo service is responsible for core part of /3.0/zoneinfo client endpoint.
Core part is expected to be very stable, so there are special requirements for code.

## Components
- zoneinfo-core

## Architecture

### Dependency graph
![img](https://jing.yandex-team.ru/files/rgnlax/Снимок%20экрана%202020-06-11%20в%2017.30.28.png)

### Components
+ Handler
+ ViewModel
+ ZoneInfoCore
+ CoreComponents
+ Interservice entities

#### Handler
Codegenerated web request handler

#### ViewModel
Codegenerated web response model

#### ZoneInfoCore
The main component with core logic implementation
Controls dance of core components.

#### Core components
Very stable domain handlers.
Core component should have very small bunch of dependencies.
Every core component should be unit tested.

Example:
`ZoneSettingsRules`

Purpose: Build rules of taxi order in given zone

Dependencies: `TariffSettings`

#### Interservice entities
TariffSettings, coutries, config, etc.

## Work with l10n

Tanker translations are not under our control, 
so special attentions should be payed here.

Missing translations often lead to unwanted 5xx errors, 
if exception is not properly catched.

In zoneinfo you can find Optional/Required translations concept.

For more details see `helpers/translations.hpp`

#### Optional
Use optional translation for keys, that are not required for response.
If optional translation is None, its your choice how to manage it.
You can put empty string, or you can drop the whole subobject.

#### Required
Use required translation only when its absolutely required for response.
Missing of this key should be found as soon as possible, 
so 5xx error is the best option.

#### Example
```c++
#include <helpers/translations.hpp>
// namespace zoneinfo
auto tanker_key = MakeTankerKey("client_messages",  "branding_key");
auto branding_key = MakeOptionalTranslation(tanker_key);

// presenter
auto translator = MakeTranslator(translations);
auto result = translator->Translate(branding_key, locale);
if (!result) // drop item here
```

## Work with images
```c++
#include <helpers/images.hpp>
// namespace zoneinfo
auto image_tag = MakeImageTag("class_econom",  6);
auto image = MakeOptionalImage(image_tag);

// presenter
auto image_getter = MakeImageGetter(images, config);
auto result = image_getter->GetImage(image, app, size_hint);
if (!result) // drop item here
```
