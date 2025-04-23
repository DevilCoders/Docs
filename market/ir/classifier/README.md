В репозитории classifier два публикуемых компонента:
* **classifier**,
* **classifier-trainer**.

Их сборку и выкладку нужно производить через релизную машину в ЦУМе:
https://tsum.yandex-team.ru/pipe/projects/ir/delivery-dashboard/classifier-arc.

Этой релизной машине соответствует пайплайн
https://tsum.yandex-team.ru/pipe/projects/ir/pipelines/classifier-arc.

Остальные компоненты не публикуются:
* **classifier-core** – общий модуль между classifier и classifier-trainer
* **classifier-nirvana** – набор консольных main-ов для отладки функционала, используемых в Nirvana. По результатам ревью этот проект исключен из общего ya.make
  Более подробные описания со ссылками на workflow в самих классах.

