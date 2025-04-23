# ReConf-Juggler-RTC HOWTO

## How to contribute

If you unfamiliar with arcadia build ecosystem, read first
[ya](https://wiki.yandex-team.ru/yatool/) and
[ya test](https://wiki.yandex-team.ru/yatool/test/#testynapytest)

    # Get sources
    ya clone --no-junk ./arcadia && cd ./arcadia
    ya make -j0 --checkout infra/rtc/juggler/reconf
    cd infra/rtc/juggler/reconf

    # Run tests
    ya make -tA --checkout

    # Commit changes
    svn ci -m 'short and useful info (TICKET-000) REVIEW:new'

## How to canonize tests data

Note: make sure you have updated `infra/reconf` and `infra/reconf_juggler`
before canonization.

There are two things to canonize:

1. Input (resolved, external) data, such as wall-e projects, resolved hosts and
   so on. **OPTIONAL**: should be canonized when tests depends on changes in
   such data.

    `ya make -tA --test-param canonize-input=1`

2. Output (resulting) data. Should be canonized every time aggregates changed.

    `ya make -tA --test-param canonize-output=1`

Ensure you verified changes before you made a commit.

For basic concepts see [ReConf testing](../../../reconf/README.md#testing-results)

## How to diff aggregates

Quite often changes in canonized aggregates are too large and automatic diff
snippets provided by pytest just not enough. In this case external tool may be
used to observe full diff:

    ya make infra/reconf_juggler/tools/jdiff/bin
    cp -alL infra/reconf_juggler/tools/jdiff/bin/jdiff <dir_from_PATH>

Usage:

    ya make -tA --test-param canonize-output=1  # put changed files to disk
    svn diff --diff-cmd=jdiff tests/canondata/test_builder.test_default/output

## How to deploy aggregates to Juggler

When changes committed to VCS,
[testenv](https://a.yandex-team.ru/arc/trunk/arcadia/testenv/jobs/runtime_cloud/BuildJugglerAggregates.yaml)
will run sandbox [task](https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/projects/reconf/reconf_juggler)
to build all RTC aggregates and diff them to currently used.  
For deploy, sandbox task should be simply released (release status doesn't
matter).

Sandbox task report it's key stages to Startrek when issue id mentioned in
commit message and startrek token used in task has permission to comment
issues in the corresponding queue.

Commit history can be viewed in testenv [UI](https://beta-testenv.yandex-team.ru/project/reconf-juggler-rtc/job/RECONF_JUGGLER_RTC/history).

## How to build all aggregates manually

Builders have their own building hierarchy, first level is a root builder:

    ya make --checkout builders/bin/
    builders/bin/builder --target jsdk_dump > all.jsdk.json

as a result you have all aggregates built by per-project subbuilders.

## How to build aggregates for single project

Second level - per-project builders, may be runned separately to ease debug and
maintenance:

    cd builders/<project>/bin && ya make --checkout
    ./builder --target jsdk_dump > aggrs.json

such bulders may have their own subbuilders as well.

## How to validate generated aggregates

There is no automatic linters for now, but they are
[planned](https://st.yandex-team.ru/RUNTIMECLOUD-9289).

To be able to control changes manually, all aggregates built by
ReConf-Juggler-RTC are [canonized](#how-to-canonize-tests-data).  
This almost guarantee that all changes will be visible (diff) on tests run.

Be sure you verified changed canonized aggregates before you made a commit.

## How to verify aggregates structure

All builders by default may generate output in following forms (targets):

- `initial_data` - entities to build aggregates for
- `initial_tree` - desired tree, all aggregates will inherite this structure
- `checks_tree` - forest of aggregates, but not options built
- `checks_full` - same as above, but aggregates are filly build
- `jsdk_dump` - same as above, but in form acceptable by juggler-sdk

First shows projects to build aggregates for, next two helps when you tracing
how trees are built, fourth shows full options and gives an apportunity to diff
result to previously built one.

See also: [verify results](#how-to-diff-aggregates)

## How to upload aggregates to Juggler manually

**WARNING**: This method is for emergency cases only!  
\* At least until juggler-sdk implement safe deploy procedure. TODO: add st issue here.  
See [standard build and deploy flow](#how-to-deploy-aggregates-to-juggler)

**WARNING**: using `reconf-rtc` mark you will replace all RTC aggregates with
you own!

First, you need
[Oauth Token](https://oauth.yandex-team.ru/authorize?response_type=token&client_id=cd178dcdc31a4ed79f42467f2d89b0d0)

    virtualenv venv
    . venv/bin/activate
    pip install --index-url https://pypi.yandex-team.ru/simple juggler-sdk
    export JUGGLER_OAUTH_TOKEN=<token_from_link_above>
    cat all.jsdk.json | juggler-sdk load --mark reconf-rtc --dry-run

If all looks good - repeat last command without `--dry-run` opt.

## How to add new aggregate

First, you have to decide which [category](checks/README.md#categories)
new aggregate is belongs to, then add new [class](checks/README.md#classes)
to desired module.

Second thing: enlist new class in appropriate [CheckSets](checksets.py)

That's it. Now [build aggregates](#how-to-build-all-aggregates),
[verify results](#how-to-validate-generated-aggregates),
[canonize tests](#how-to-canonize-tests-data), [commit](#how-to-contribute) and
[deploy](#how-to-deploy-aggregates-to-juggler) to Juggler.

## How to add new aggregates builder

1. Copy `infra/reconf_juggler/examples/simple` dir to desired place
2. Fix paths in all `ya.make` files inside new directory, fix imports
   accordingly
3. Replace project specific code in `builder.py` with your own
4. Verify and [canonize aggregates](#how-to-canonize-tests-data)
5. Enlist new builder in [root builder](builders/builder.py)
6. Add test that new aggregates present in
   [root builder's output](builders/tests/test_builder.py)
7. Add new project to upper-level `ya.make` files
8. Commit changes to VCS

For more info about builder directory structure see
[builders reference](../../../reconf_juggler/BUILDERS.md).

## How to replace opt in all checks in CheckSet

Unlike single checks, which may simply override all they want, `CheckSet`
require replacements in each check it contain.  
This (and much more - any opt actually) can be done using `CheckOptFactory`,
see [ReConf-Juggler test](../../../reconf_juggler/tests/test_opt_factory.py)

## How to override options for hostman units checks

Aggregates are built automatically for each hostman unit. By default aggregates
have no alerts except solomon charts.  
There are two ways to disable aggregates build or redefine aggregates options:
1. Set per-directory defaults in `.reconf-juggler.defaults` in units directory
   or any parent directory (hierarchial opts merge), see [core units defaults](
   https://bb.yandex-team.ru/projects/RTCSALT/repos/core/browse/units.d/.reconf-juggler.defaults)
   for reference.
2. Set per-unit options in unit spec annotations (same format as for per-dir
   defaults, but placed as YAML text in `meta.annotations.reconf-juggler`), see
   [hostman reporter unit](https://bb.yandex-team.ru/projects/RTCSALT/repos/core/browse/units.d/yandex-hm-reporter.yaml)
   for reference.

## Feedback

Feel free to [make a ticket](https://st.yandex-team.ru/createTicket?type=1&priority=2&tags=juggler&queue=HOSTMAN)
if you spotted a bug or have a feature request.
