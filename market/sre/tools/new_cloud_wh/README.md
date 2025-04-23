## Добавляет группы и хосты под новый облачный склад в кондуктор
~~~
optional arguments:
  -h, --help            show this help message and exit
  --city CITY           Город на Русском языке, в котором открывается склад
  --stage {stable,testing,unstable} 
                        Стэйдж
  --dark DARK           Это даркстор?
  --wh_num WH_NUM       Какой номер склада в этом городе по счету?
  --primary_location {vla,sas,man,iva}
                        На какой площадке основная нода?
  --secondary_location {vla,sas,man,iva}
                        На какой площадке резервная нода?
  --codes_file CODES_FILE
                        Файл с кодами
  --custom_city_code CUSTOM_CITY_CODE
                        Задать руками код города
~~~

- city - Город в кавычках на русском языке. Под него автоматически подберется city_code из файлика ./codes
- stage {stable,testing,unstable} - нужен для генерации групп и названия хостов
- dark - Не даркстор ли? Булев флаг. Если включен, сгенерится что-то типа wms-app-dark-ekb01v....
- wh_num - Номер склада в городе, нужен для нумерации виртуалок. По дефолту 01.
- primary_location, secondary_location {vla,sas,man,iva} - какая площадка будут основной, а какиая резервной.
- codes_file - расположение файлика с кодами в формате "ekb Екатеринбург"
- custom_city_code - можно указать кастомный трехбуквенный код города. Например "ekb". 


## Конфигурационный файл:
Для работы нужен файл ~/.conductor_client.ini следцющего содержания:
```
[conductor_client]
path = http://c.yandex-team.ru/api/v1
token = {Тут суперсекретный токен}
```
Токен можно сгенерить вот тут: https://oauth.yandex-team.ru/authorize?response_type=token&client_id=eb3c509c74b649cd8411ffc154543fe0
