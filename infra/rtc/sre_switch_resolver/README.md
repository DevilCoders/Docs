#Simple SRE switch definer
**Example of usage:**

> ./sre_switch_resolver $switch_name1 $switch_name2 ... $switch_nameN
> cat switches.txt | ./sre_switch_resolver

**Результат работы скрипта**

Результами работы скрипта будет лог вывода вида
> $DATE $TIME [INFO] category: $CATEGORY switches: $SWITCHES

где:
* $DATE - текущая звездная дата
* $TIME - текущее время
* $CATEGORY - одна из следующих категорий:
  * only_yt - свич в котором имеются только хосты YT *
  * only_yp - свич в котором имеются только хосты YP *
  * yp_yt - свич в котором имеются хосты YP и YT
  * only_gencfg_coh - свич в котором хосты cohabitation "генерилки"/Gencfg
  * only_true_gencfg - свич в котором только "true" хосты Gencfg
  * yp_gencfg_coh - свич в котором есть хосты YP и cohabitation "генерилки"/Gencfg
  * yt_gencfg_coh - свич в котором есть хосты YT и cohabitation "генерилки"/Gencfg
  * yt_yp_gencfg_coh - свич в котором есть хосты YT и YP и cohabitation "генерилки"/Gencfg
  * yt_true_gencfg - свич в котором есть хосты YT и "true" хосты Gencfg
  * yp_true_gencfg - свич в котором есть хосты YP и "true" хосты Gencfg
  * yt_yp_true_gencfg - свич в котором есть хосты YT и YP и "true" хосты Gencfg
  * others - свич в котором не rtc хосты
* $SWITCHES - лист свичей соответствующих категории


