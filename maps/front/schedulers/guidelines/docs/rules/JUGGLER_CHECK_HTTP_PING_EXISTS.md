# JUGGLER_CHECK_HTTP_PING_EXISTS

Requires `http-ping` juggler check.

## Rationale
The `/ping` endpoint of each service is used for determining the service's liveliness.
If the `/ping` endpoint doesn't return 200 status code, the service can be considered dead.
This endpoint is used by balancers (to turn off traffic payload to dead instances) and deploy (`readiness` status means that instance is ready for payload).
Also this check is used as a flag that active alerts are pushed and work properly.

## Solution
1. Go to the your repository in terminal.
1. Check you have latest version of `@yandex-int/qtools` package.
1. Run the following command: `npx qtools alerts push`
1. If there are changes to be applied to the check configuration, the command will display the diff and will ask you to run it again with the --force flag to confirm. If asked - confirm your changes.

---
_[Source](https://a.yandex-team.ru/arc_vcs/maps/front/schedulers/guidelines/src/tests/juggler/required-checks.test.ts#L48-56)_
