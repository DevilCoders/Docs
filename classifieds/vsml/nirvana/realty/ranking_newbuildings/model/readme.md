## Описание
Здесь представлен минимально доработанное рабочее описание графа [VSML-1007](https://nirvana.yandex-team.ru/flow/56161f5e-c610-44c2-827b-80b1470c1852). 
Сырая версия описания получена с помощью `vh3 import`:
```bash
vh3 import -f https://nirvana.yandex-team.ru/flow/56161f5e-c610-44c2-827b-80b1470c1852
```

## Подготовка
Для создания графа нужно:
1. Установить vh3 (см раздел доки [Установка](https://docs.yandex-team.ru/vh3/quickstart#ustanovka))
2. Добавить OAuth-токен для Nirvana
3. Рекомендуется также прописать квоту и workflow_id (где будет создаваться очередной граф) в ~/.vh3/profile.yaml
4. Прописать yt_token, yt_pool и mr_account в профиле ~/.vh3/profile.yaml

Последние два этапа хорошо описаны в разделе доки [Подготовка](https://docs.yandex-team.ru/vh3/usage/cli#podgotovka)


## Сборка графа
Для создания графа в своем воркфлоу (указанном в ~/.vh3/profile.yaml) нужно воспользоваться командой `vh3 draft`:
```bash
cd ~/your_path/arcadia/classifieds/vsml/nirvana/realty/ranking_newbuildings/model
vh3 draft workflow.vsml_1007
```
Для запуска
```bash
vh3 run workflow.vsml_1007
```
или
```bash
python3.9 workflow.py
```
