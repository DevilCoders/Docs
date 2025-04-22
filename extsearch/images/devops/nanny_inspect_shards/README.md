Скрипт для поиска шардов которые не могут заприпейриться/активироваться, tasckgroup и job берутся из урла джобы в няне.
Пример урла:
https://nanny.yandex-team.ru/ui/#/alemate/taskgroups/search-0071977565/tasks/job-0000000001

Не может запререйриться
./nanny_inspect_shards.py --token <nanny_token> --taskgroup 0071977565 --job 0000000001  --target-state startable

Не может переключиться
./nanny_inspect_shards.py --token <nanny_token> --taskgroup 0071977565 --job 0000000001  --target-state started

