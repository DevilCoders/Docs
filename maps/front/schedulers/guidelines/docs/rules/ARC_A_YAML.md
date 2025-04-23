# ARC_A_YAML

Requires a real ABC service in the `a.yaml` of your repository.

## Rationale
The link to the repo is used by the DevOps automatic process to help the on-call engineer mitigate the problem.
Also it helps when you find a project in ABC to quickly jump to the code repository.

## Solution
Add ABC slug to the service's description:
1. Go to the arc folder of your project.
1. Add `service: {slug}` to `a.yaml`.
1. Click "Commit".

---
_[Source](https://a.yandex-team.ru/arc_vcs/maps/front/schedulers/guidelines/src/tests/arc/a-yaml.test.ts#L21-30)_
