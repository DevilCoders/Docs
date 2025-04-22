## Dumper
Инструмент для миграции mstand метрик


Создать новые серпсеты на основе имеющегося
```bash
./metrics_dumper init 31419520 > exp.json
```
Ждем....

Потом можно запустить дооценку mstand рассчетов которые были запущены на оригинальном серпсете
```bash
./metrics_dumper evaluate < exp.json
```
Можно запустить не все, а только те метрики что были посчитаны на серпсете и есть в аспекте
```bash
./metrics_dumper evaluate default mstand commercial proxima_spb_blender uno object_answer national spam < exp.json
```

Надо подождать пока она закончится (где-то час) - за этим лучше следить на странице сравнения по ссылке из команды `init`

После того как метрики расчитаны их можно сравнить
```bash
./metrics_dumper diff new control < exp.json
diff new control
```

Что бы понять кто за какие метрики отвечает можно воспользоваться командой
```bash
./metrics_dumper deprecated default mstand commercial proxima_spb_blender uno object_answer national spam
```
Тут будут ответственные за аспекты и owner'ы deprecated метрик

Найти запуски mstand можно так
```bash
./metrics_dumper mstandruns --days 30
```
