# ABC_DEVOPS_COUNT

Requires minimal number of DevOps in ABC service.

## Rationale
"Bus factor" for each service should be enough for the service to be maintainable even if one (or even two)
of the crucial developers are absent (holiday, illness, and etc.).

## Solution
You have to follow the following instructions:
1. Go to your ABC service page - `https://abc.yandex-team.ru/services/${service-slug}/duty/`, just replace service-slug with you service's slug.
1. Add people with DevOps role to the ABC service.

---
_[Source](https://a.yandex-team.ru/arc_vcs/maps/front/schedulers/guidelines/src/tests/abc/devops-scope.test.ts#L21-31)_
