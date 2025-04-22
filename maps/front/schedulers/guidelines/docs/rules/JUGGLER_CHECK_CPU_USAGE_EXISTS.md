# JUGGLER_CHECK_CPU_USAGE_EXISTS

Requires "cpu_usage" check.

## Rationale
CPU usages is a vital indicator for the service health. So, this check is obligatory for all services.

Also this check is used as a flag that passive alerts are pushed and work properly.

## Solution
1. Go to the your repository in terminal.
1. Check you have latest version of `@yandex-int/qtools` package.
1. Run the following command: `npx qtools alerts push`
1. If there are changes to be applied to the check configuration, the command will display the diff and will ask you to run it again with the --force flag to confirm. If asked - confirm your changes.

---
_[Source](https://a.yandex-team.ru/arc_vcs/maps/front/schedulers/guidelines/src/tests/juggler/required-checks.test.ts#L73-81)_
