Loose signals (No Nearby Geometry)
===

| Key | Value |
| --- | --- |
| Sandbox scheduler | https://sandbox.yandex-team.ru/scheduler/85989 |
| Output tables | https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/jams/production/graph_quality/hypotheses/loose_signals/hypotheses |

#### Something broken?

Contact ([or create a ticket](https://st.yandex-team.ru/createTicket?queue=GEOQ)) [GEOQ](https://staff.yandex-team.ru/departments/yandex_content_geodev_3808/) ([Slack helpline channel](https://yndx-all.slack.com/archives/C01RN8Z27MX)).

Project tree
---
| Directory | Description |
| --- | --- |
[prepare](prepare) | Prepares hypotheses by running user signals through series of filters to determine signals that can't be matched to any valid road geometry on our road graph.
[upload](upload) | Given a table from the prepare stage, samples *n* hypotheses, formats descriptions and reports them to nmaps.
