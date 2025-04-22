Manoeuvres
===

| Key | Value |
| --- | --- |
| Sandbox scheduler | https://sandbox.yandex-team.ru/scheduler/106594 | 
| Nirvana graph | https://nirvana.yandex-team.ru/flow/e76f8371-126a-49c2-b046-20f227d978be/ |
| Output tables | https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/jams/production/graph_quality/hypotheses/manoeuvres |

#### Something broken?

Contact ([or create a ticket](https://st.yandex-team.ru/createTicket?queue=GEOQ)) [GEOQ](https://staff.yandex-team.ru/departments/yandex_content_geodev_3808/) ([Slack helpline channel](https://yndx-all.slack.com/archives/C01RN8Z27MX)).

Project tree
---
| Directory | Description |
--- | ---
[prepare_dataset_1](prepare_dataset_1) | 1st stage. Deals all the work with finding manoeuvres and counting user statistics on YT.
[prepare_dataset_2](prepare_dataset_2) | 2nd stage. Given a table from the 1st stage, appends corresponding images to each row and stores resulting dataset in a sandbox resource. Should be ran on Sandbox©. Also starts 3rd stage via Nirvana API.
[pytorch](pytorch) | 3rd stage. Trains a neural network to predict the annotation for the manoeuvre. Currently is running with Nirvana Python DL. Uploads estimates to YT.
[upload](upload) | 4th stage. Uploads hypotheses to nmaps.
