# Sync assessors
## General information
| Key | Value |
|---|---|
| Nirvana | https://nirvana.yandex-team.ru/flow/841254eb-3a44-4aa6-9164-43af151575cc/ |
| Reaction | https://reactor.yandex-team.ru/browse/resolve?path=/maps/front/maps/infra/maps-assessors-sync |

## Documentation
We want to give permissions to assessors via our own ABC services and don't user the general one (https://abc.yandex-team.ru/services/test_assr/). It can be done by adding ABC-service to another. It's not implemented yet (https://st.yandex-team.ru/ABC-6466); so, this scheduler saves the day.

It uses the following algo:
1. Get all members of [Assessors ABC service](See https://a.yandex-team.ru/arc_vcs/maps/front/schedulers/maps-assessors-sync) with the role `functional_tester`.
2. Get all members of our ABC services.
3. All assessors from `Assessors ABC service` add to our ABC services with role `consultant`.

Finally, we have two roles in our ABC services: `functional_tester` for our QA team and `consultant` for assessors. It makes it possible to give different permissions for each scope.

Adding/removing members from ABC services are done via https://staff.yandex-team.ru/zomb-podrick. So, make sure that you add it to destination ABC service as a manager.
