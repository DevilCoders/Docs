# Клиент для суммаризатора

Принимает данные в stdin, пишет в stdout.
Входные данные либо json proto [TSummarizerInput](https://a.yandex-team.ru/arc/trunk/arcadia/search/alice/serp_summarizer/runtime/proto/summarizer.proto?rev=6771580#L15), либо просто текст запроса построчно, если используется опция `--prod`.

Usage:
`echo 'были ли у арагорна права на трон средиземья' | ./serp_summarizer_client_cli --prod`

Опции:

* `--prod` – с флагом принимает на вход просто текст запроса, ходит в продакшн;
* `--pp` – удобный вывод для человека;
* `--host` – хост суммаризатора;
* `--async` – ходить в асинхронную ручку;
* `--j [X]` – количество потоков;
* `--do-fail` – падать на неудачный запрос.
