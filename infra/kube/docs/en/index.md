## Инфраструктура гибридных облаков

According to world business growth Yandex uses different vendors for cloud creation
and cloud resource management. The processes od creation and management are different since
each vendor has its own features.

Nowdats it is accessible creation and management of following clouds:

* Yandex.Cloud
* Amazon Web Services (AWS)
* Microsoft Azure

In order to reduce differences in management [Crossplane](https://crossplane.io/) can be used.
It allows to create clouds in unified manner using resource templates.
Detailed documentation about resource templates and about ways to test resource management
using Crossplane is accessible by [link](https://a.yandex-team.ru/arc/trunk/arcadia/infra/kube).


