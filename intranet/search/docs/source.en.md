# Adding new indexation source

## Steps to follow to add a new source
- Decide whether the new source would be a part of vertical "Intranet" or not. If yes, you don't need to do anything. If no, you need to add a new service to https://ssm.n.yandex-team.ru. This form should be filled twice, once for testing environment (`prestable` tab) and once for production environment (`stable` tab). You should select "Logbroker (PQ)" as a data delivery method. Other parameters are to be specified with discussion with SaaS team.

- Add `endpoint api` setting for the source (`settings.app_settings.isearch.yaml` file, `api.<source_name>` path).

- Add scope into settings (`settings.app_settings.isearch.yaml` file, `scopes.<scope_name>` path). `scope_name` must have suffix `search`

- Create a class to query apis in `core/sources/<source_name>`.

- Add `Source` class inherited from `core.swarm.indexer.Indexer` or `core.swarm.api_indexer.PagedApiIndexer`, in `core/sources/<source_name>`.

- Source class must return an instace of `Snippet` class, which should be implemented in `core/snippets`. You need to put all the displayed fields inside the snippet class. By "displayed" we mean all the fields we need to display the snippet in the SERP.
- Source class must return the document body in the `do_create` method. The body of the document must contain all the needed *text* data. Important: if some of the fields are to be used by the search, but they should not make their way to passages, you should put them into a hidden zone `z_ns_hidden` (or in `!hidden` zone, zone with this name will be automatically renamed into a `z_{searchname}_hidden`). Passages are the parts of the document which will be highlighted in the SERP snippet. Important: you need to specify `z_ns_hidden` zone in the file `rtyserver.diff-{searchname}` in your SaaS service settings (for example, https://saas-mon.n.yandex-team.ru/service_info?service=intrasearch_so&ctype=stable).

- Add facets to the `emit_attrs` method and in settings at `scopes.<scope_name>.facets`.

- Add factors to the `emit_factors` method.

- You need to make four migrations at `core/migrations`: add `Revision`, `Service`, `permission` and grant full access for the new permission (examples `0007_stackoverflow_add_service_and_revision.py` и `0008_stackoverflow_permission.py`). All the four migrations could be in the single file.

- In order for marks to be working, you have to add one more migration (`0015_moebius_marks_and_suggestedanswer.py`) and include the name of the new vertical into the `choices` field. Also, you have to add this feature for the new vertical using the admin site (see the last pt in this instruction)

- You need to add a new setting for `SaaS` service (`settings/app_settings/isearch.yaml` at `api.saas.<saas_service_name>`). With a high propability `indexer` should inherit `api.saas_abstract.base.indexer`. To make in 100% clear you need to see at `logbroker_host` of the SaaS service. Also you maybe need to look at the settings of`SaaS push client`, which are at the file `settings/app_settings/default.yaml` in `saas_push_client`. `path` и `pruning` could be left blank.

- You need to add a new setting for search service (`settings/app_settings/isearch.yaml` at `searches.base.<search_service_name>`)

- You need to add a rule for the source (and his wizard, if any) in `abovemeta/decider/rules/isearch_rules.py`.

- You should add a cron task to reindex source in the `setting/celery/global_config/isearch.py` file.

- You need to add factors at `Saas` as described in `docs/factors.md`.

- You need to add revision at the [link](https://search-back.test.yandex-team.ru/_admin/sources/<source_name>/default/revisions?organization_id=).

- You need to set setting `"PruneAttrSort":"formula:pruning_rank"` in `rtyserver.diff` . It is need for pruning to start working. In the file `relev.conf-{servicename}` you need:
  1. Set dynamic factors in the `dynamic_factors`. You can copy that from `intrasearch_so`.
  2. List static factors we emit at `static_factors`. Factors should follow format `"STAT_{searchname}_{factorname}": {"index": index, "default_value": 0}`
  3. Add two keys at `formulas` part.
  4. The first key: `pruning_rank` contains one more key, `polynom`. It is a pruning polynom and it must be simple enough. You can compile the polynom from the source with the polynom converter: https://saas-mon.n.yandex-team.ru/polynom_converter?service={yoursaasservicename}. The simplest pruning polynom may look like that: `1*STAT_stackoverflow_updated`.
  5. Second key: `default`. It may be named differently, but the simplest way is to name it `default`. It is the ranging formula. In this part there may be two keys. One is named `matrixnet`, other is `polynom`. `matrixnet` key points to the machile-learned FML formula, for example: `"matrixnet": "fml-844944.info-intrasearch_so"`. To make it work you need not to forget to copy the formula from the fml. To do that, press the `fml-copy...` and choose at `Fml formula id` the number of the formula from the fml (for example, 844944). For the `File name` specify fml-{id}, for example fml-844944. After you press the button, the formula will be downloaded into your working directory, and the filename will be suffixed with `.info-{saasservicename}`. Name of that file you should put into `matrixnet` key. The second key is `polynom`, it allows to use  matrixnet formula as just one of the factors in the polynom. Important: to make it work, in `dynamic_factors` there must be key with the name `MatrixNet`. Polynom here is compiled with the same polynom generator as for pruning, but you should make it more tricky. For example, for StackOverflow it is `1*MatrixNet+0.3*STAT_stackoverflow_updated+0.5*STAT_stackoverflow_is_answered`.
  6. Don't forget to add formula at the admin. You need to do it twice: in testing https://search-back.test.yandex-team.ru/_admin/formula/viewer/ and in production https://search-back.yandex-team.ru/_admin/formula/viewer/. To do that you need to select your search and your SaaS service and put `default` in the "compiled polynom". That's all, all other fields should be blank/default.
  7. You need to deploy your changes in SaaS configs: https://saas-mon.n.yandex-team.ru/deploy?service=intrasearch_so&ctype=prestable (replace intrasearch_so with your service and the prestable/stable depending on testing/prod env). Uncheck the "only save" and press "Deploy".

- In order for marks to be working, you have to add the name of the new search into the `enable_marks` field **once your code is deployed**. Use this link https://search-back.test.yandex-team.ru/_admin/features/group/yandex/

## Possible errors and obstacles

- `SaaS push client` does not work.

You need to hook into it with `ya tool gdb`

```bash
supervisorctl stop saas_push
ya tool gdb /intrasearch/etc/bin/saas-push
run -c /intrasearch/etc/saas/saas_push.conf
```

Then read the error and understand what is wrong.

- There is no SERP.

Read errors by the [link](https://saas-mon.n.yandex-team.ru/export_errors?service=<saas_service_name>&ctype=prestable).

- Indexation does not stop.

Probably indexation raises exception we are unable to handle and which is not inherited from `RecoverableError` or `UnrecoverableError`.
Inheriting the exception from one of those should help.


## Useful links

- Get the [SERP](https://search.test.yandex-team.ru/<scope_name>?text=hello&plainjson=1) in JSON format.
- Look directly into the [answer](https://search-back.test.yandex-team.ru/_abovemeta/?text=hello&scope=<scope_name>) from the backed with the needed scope.
