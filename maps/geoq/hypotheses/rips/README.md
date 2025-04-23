Rips
===

| Key | Value |
| --- | --- |
| Sandbox scheduler | https://sandbox.yandex-team.ru/scheduler/100173 |
| Output tables | https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/jams/production/graph_quality/hypotheses/rips_2/hypotheses |

#### Something broken?

Contact ([or create a ticket](https://st.yandex-team.ru/createTicket?queue=GEOQ)) [GEOQ](https://staff.yandex-team.ru/departments/yandex_content_geodev_3808/) ([Slack helpline channel](https://yndx-all.slack.com/archives/C01RN8Z27MX)).

Project tree
---
| Directory | Description |
| --- | --- |
[prepare](prepare) | Prepares hypotheses by matching user tracks and analyzing (running series of filters) unmatched ones. 
[upload](upload) | Given a table from the prepare stage, samples *n* hypotheses, formats descriptions and reports them to nmaps.
