## Скрипты для удобной работы с большими неформатированным JSONами в экспериментальных флагах

Получает экспериментальные флаги и преобразует их в форматированный JSON.
Совершает обратное преобразование форматированного JSONа в нeформатированный вид и отправляет в ITS

**Запуск**
```bash
ya make
./gd_edit
```

**HowTo**
1. Получить актуальные флаги
2. Отредактировать файл руками
3. Отправить файл с помощью gd_edit 

```bash
./gd_edit get -a <nanny_oauth> --flags <flagname1>,<flagname2>,... -e <env> -f <filename> --  Получить актуальные экспериментальные флаги окружения <env> и сохранить в <filename>
./gd_edit push -a <nanny_oauth> --dry-mode -f <filename>  --  проверить, что JSON в файле <filename> валидный без попытки отправить в ITS
./gd_edit push -a <nanny_oauth> -f <filename> -e <env>  --  отправить данные из файла <filename> в окружение <env>; структура JSON должна быть аналогичной graceful_degradation_formatted
```
Флаги `-f, --flags, -e` необязательны. Дефолтные значения:
```bash
-f  --  graceful_degradation_formatted
-e  --  testing
--flags  --  graceful_degradation_rules,graceful_degradation_monitoring_conf
```

Получить токен: https://nanny.yandex-team.ru/ui/#/oauth

# Ахтунг! Гиффани не узнает о ваших проделках
