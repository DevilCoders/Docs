build scripts
=============

The scripts automates actions described on https://wiki.yandex-team.ru/taxi/backend/release
so if you have any questions, consult that page.

Make sure that all scripts are executable (well, `common.sh` does not need to be such).

To build *custom package*, copy these files to taxi.mobile.dev.yandex.net (or another build server)
and run `custom` script:

```
    scp build_scripts/* taxi.mobile.dev.yandex.net:~/
    ssh taxi.mobile.dev.yandex.net
    ...
    (on taxi.mobile)
    ~/custom testing user1:feature/some-branch-name user2/feature/some-another-branch-name ...
```

Carefully read output and answer prompts asked. Most of times you will agree.
You will also need to enter your GPG passphrase.


To build new release, copy these files to working tree and issue `./release`.
The script will determine next release number and ask your confirmation.


To build a hotfix, copy these files to working tree and issue `./hotfix start <version>`.
