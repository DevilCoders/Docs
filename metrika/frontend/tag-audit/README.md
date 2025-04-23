# Tag.js performance audit infrastructure

Инструмент, позволяющий запустить Lighthouse аудит для заданного перечня сайтов с двумя версиями счётчика (продакшн и
экспериментальный с header x-metrika-exp=1 и is-tag-exp=1 в search string).
Выполняет thirdPartySummary и bootupTime аудиты LH.


## Run
1) Установить актуальную версию хрома [Мануал](https://geekflare.com/install-chromium-ubuntu-centos/)
2) ```nvm install v14.17.2```
3) ```npm i```
4) ``` RESULT_FILE_PATH='result.txt' TASKS_FILE_PATH='tiny.txt' AUDIT_ATTEMPTS_COUNT=2 CPU_SLOWDOWN_MULTIPLIER=4 WORKERS_COUNT=4 npm start```

Запуск в бэкграунде на QYP машине: ``` RESULT_FILE_PATH='result.txt' TASKS_FILE_PATH='domains.txt' WORKERS_COUNT=48 CPU_SLOWDOWN_MULTIPLIER=4 AUDIT_ATTEMPTS_COUNT=3 nohup npm start > out.txt & ```

## ENV_VARS

1) RESULT_FILE_PATH — файл, в который будет записан результат аудита

Формат записи аудита:
```
{
   "expReport":{
      "thirdPartySummary":{
         "mainThreadTime":981.6359999999969,
         "blockingTime":319.34799999999996,
         "transferSize":72175
      },
      "bootupTime":{
         "total":981.6359999999976,
         "scripting":909.0719999999976,
         "scriptParseCompile":9.756
      }
   },
   "prodReport":{
      "thirdPartySummary":{
         "mainThreadTime":1133.4879999999985,
         "blockingTime":360.904,
         "transferSize":72275
      },
      "bootupTime":{
         "total":1133.4879999999985,
         "scripting":923.1239999999984,
         "scriptParseCompile":9.78
      }
   },
   "task":{
      "url":"https://masterovit.ru/"
   }
}
```


2) TASKS_FILE_PATH — файл, содержащий перечень инпектируемых url (разделитель \n)

Пример:

```
https://kaliningrad.bonkover.ru/kovry-v-stile-provans/
https://sosnogorsk1.miltor.ru/domashnie-zhivotnie-i-zootovari/komnatnye-zhivotnye-pticy/popugai/volnistie-popugai/
https://project.lanbook.com/
http://photosklad.ucoz.ru/
http://vzwowz.ucoz.ru/blog/bild_pvp_pvp_razbojnika_rogi_dlja_bk_2_4_3/2012-02-14-56
https://fruitbot.ru/
https://zoogostinitsa-timofej.tiu.ru/
https://aprelevka.rosflower.ru/
https://gainstorm.io/
https://sp-pi.daily-inform.ru/landin
```

3) WORKERS_COUNT — кол-во процессов воркеров. Для 64 ядерной машины с 32ГБ ОЗУ рекомендуемое значение 48. Общее правило
   WORKERS_COUNT < CPU_CORES_COUNT  
                         
4) AUDIT_ATTEMPTS_COUNT — кол-во прогонов для каждой из версий (опциональный параметр)
   
5) CPU_SLOWDOWN_MULTIPLIER — множитель замедления CPU для эмуляции моб девайсов (опциональный параметр)
