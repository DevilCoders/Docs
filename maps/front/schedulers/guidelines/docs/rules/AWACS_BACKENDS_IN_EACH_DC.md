# AWACS_BACKENDS_IN_EACH_DC

Awacs backends should be in each DC.

## Solution
1) Go to your awacs namespace.
2) Go to backends list.
3) Tap "Create Backend" button or "Copy Backends" button and create backends for missing DC.

{% note info %}

Target DC you can select in tab "Spec" in block "YP endpoint sets".

{% endnote %}

---
_[Source](https://a.yandex-team.ru/arc_vcs/maps/front/schedulers/guidelines/src/tests/awacs/backend.test.ts#L54-65)_
