# ABC_CALENDAR_DUTY_HAS_ON_CALL

Requires duty calendar with slug `on-call`.

## Rationale
This duty schedule slug is specified in our alerts notifications and is used for phone escalation.

## Solution
Make sure that one of your duty calendars in the ABC service has the slug named `on-call`.
If `qtools` tool is used, just run `qtools alerts push` command which will create a duty schedule with slug `on-call`.

If you don't use `qtools` and your duty schedule has different slug, then remove the current schedule and create a new one with approprriate slug, named `on-call`.

---
_[Source](https://a.yandex-team.ru/arc_vcs/maps/front/schedulers/guidelines/src/tests/abc/calendar-duty.test.ts#L47-53)_
