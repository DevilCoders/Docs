## Conflict Score binary tasks

This folder contains code of two binary tasks, [BROWSER_REPORT_PR_CONFLICT_SCORE](https://sandbox.yandex-team.ru/tasks?children=true&type=BROWSER_REPORT_PR_CONFLICT_SCORE&created=14_days) and [BROWSER_SEND_CONFLICT_SCORE_REPORT](https://sandbox.yandex-team.ru/tasks?children=true&type=BROWSER_SEND_CONFLICT_SCORE_REPORT&created=14_days).

### BROWSER_REPORT_PR_CONFLICT_SCORE

`BROWSER_REPORT_PR_CONFLICT_SCORE` is triggered by-commit by Teamcity build [Browser_Tests_ReportPrConflictScore](https://teamcity.browser.yandex-team.ru/buildConfiguration/Browser_Tests_ReportPrConflictScore?branch=&mode=builds#all-projects).

This binary task calculates conflict score change for current PR, then leaves a comment about it in BitBucket PR activity.

If conflict score change value is too high, the binary task sets a veto and summons an approver.

To learn more about conflict score metrics, see https://wiki.yandex-team.ru/browser/dev/infra/duty/cheatsheet/#izmenenieconflictscore.

### BROWSER_SEND_CONFLICT_SCORE_REPORT

`BROWSER_SEND_CONFLICT_SCORE_REPORT` is triggered once per week for `master` and `master-next` branches.

It is scheduled in Sandbox. ([master](https://sandbox.yandex-team.ru/scheduler/708035/view), [master-next](https://sandbox.yandex-team.ru/scheduler/708036/view) branches)

It collects conflict score change values from every PR merged into specified branch for the specified period.

Then it sends the aggregated report to specified emails.
