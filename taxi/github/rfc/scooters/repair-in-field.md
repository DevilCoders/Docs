# Полевой ремонт

## Бизнес задача
Сделать полевой ремонт постоянным повторяющимся процессом.

### Общий алгоритм
![](static/ops-repairs/field_repair_base.png)
1. Самокат ломается
2. На самокат навешиваются тэги о том, что самокат сломан. В случае критичной поломки (сломана подножка, сломано крыло и пр.), самокат блокируется сразу. Если некритично, то самокат остаётся доступен для аренды.
3. Создаётся миссия для полевого ремонтника на большой машине на объезд сломанных самокатов.
4. Ремоник подъезжает к каждому сакмокату и диагностирует его. Если есть возможность отремонтировать, то самокат ремонтируется и становится доступным для аренды. Иначе ремонтник забирает самокат с собой на склад для складского ремонта.
5. В конце миссии ремонтник возвращается на склад. Выгружает все самокаты, которые он не смог починить. Эти самокаты будут отремонтированы в рамках складского ремонта

На первом этапе, будем обходиться одним тэгом broken.
В будущем для каждой поломки у нас будет свой тэг, так мы сможем разделить критичные и некритичные поломки, и в зависимости от этого, блокировтаь самокат для аренды сразу или нет.

---
### Реализация
#### 1. Создание миссии на полевой ремонт
1. STQ ```scooters-fetcher``` из сервиса scooters-ops получает все самокаты, на которых:
   * есть тэг ```broken```
   * нет тэгов от других миссий (перезарядка, релокация, ремонт)
   * нет ```need_warehouse_repair``` (означает, что самокат не получилось отремонтировать в поле, и ремонтник забрал его на склад)

2. Для каждого самоката создаётся драфт ```field-repair```, где указывеется id самоката.

3. При подготовке драфта ничего не проверяем и не навешиваем тэги.

4. Диспатч получает драфты через сущетсвующую ручку. Получает список лавок, которые являются складами, и регионы полевого ремонта для этого склада. Составляет миссию из сломанных самокатов
   * исполнитель на большой машине
   * начало и конец - на складе.
   * точка - самокат. Работа на точке - field_repair_job c одним самокатом
      ```
        {
          'type': 'field_repair',
          'typed_extra': {
              vehicle_id: <vehicle_id>
          }
        }
      ```
   * (Миссия максимально похожа на миссию по перезарядке, но на первой и последней точке не надо получать и сдавать что-либо. Приём самокатов на склад будет релизован через мувера, коотрый будет сканировать все прибывшие самокаты)

5. Миссия отправляется на подготовку в scooters-ops. Там нужно корректно обработать новый тип джобы ```field_repair_job```.
   * Проверяем запрещающие тэги
   * Проверяем, что самокаты не находится в аренде
   * На самокат блокирующий навешивается тэг ```field_repair_in_progress```

6. Ремонтник берет миссию и разъезжает по точкам

7. При окончании работ на точке будет такая валидация для нового типа работ:
   - На самокате либо не должно быть тэга ```broken``` (самокат починили)
   - Либо на самокате два тэга есть ```broken``` и ```need_warehouse_repair``` (самокат не получилось починить, ремонтник забирает его с собой на склад)

---
#### 2. Ремонт самоката через бота
![](static/ops-repairs/field_repair_bot_flow.png)
1. Ремонтник выбирает в боте *Полевой ремонт*. Если в боте нет информации, о том, в каком регионе работает ремонтник, то просим ввести его координаты, где он находится.
По координатам определяем регион (moscow, spb, krasnodar) и сохраняем в таблицу бота. Определение региона по коориднатам уже реализовано в ручке ```/scooters-misc/v1/areas```

2. Ремонтник сканирует самокат, проводит диагностику.
При нажатии ремонтником кнопки *Начать ремонт*, бот дёргает ручку ```/scooters-ops-repair/repair/start``` и передаёт в неё vehicle_id, performer_id, тип - field_repair и регион.
   * Дополнительно можно сохранить в историю ремонта координаты, где находился самокат перед началом ремонта
3. Самокат ремонтируется так же как и в скадском флоу
4. Если самокат получилось успешно отремонтировать, то ремонтник нажимает на кнопку *Завершить ремонт*. С самоката снимается тэг ```broken``` и он снова доступен для аренды.
2. Иначе, ремонтник нажимает на кнопку *Забрать самокат на склад*.
В этот момент дёргается ручка сервиса ```/scooters-ops-repair/repair/stop-and-pickup```. В ручке происходят проверки на то, что все работы по ремонту заверешены, на самокат навешивается тэг ```need_warehouse_repair```. Ремонт завершается со статусом ```failed-with-pickup```.
3. Ремонтник забиарет самокат с собой на склад.


#### 3. Флоу миссии в новом ПРО
 - В процессе обсуждения

---
### Вопросы
1. Как добиться того, чтобы самокаты, которые сейчас находятся на складе с тэгом broken не попадали в миссии? (На первом этапе точно будут такие. Позже они отсеятся засчёт флоу мувера, так как при поступлении самоката на склад, на самокат будет навешиваться тэг склада).
  * На первом этапе можно будет сделать зону полевого ремонта такую, чтобы склад не попадал в неё (nice!)
2.


---
### Задачи:
1. Новый тип драфтов field-repair
    * ```
      {
         'draft_id': draft_id,
         'type': 'field_repair',
         'typed_extra': {
            'vehicle_id': vehicle_id
          },
      }
      ```
2. Новый тип джоб field-repair-job. Внутри будут похожи на джобы для перезарядки
    * ```
        {
          'type': 'field_repair',
          'typed_extra': {
              vehicle_id: <vehicle_id>
          }
        }
      ```
    * Добавить валидацию заврешения работ на точке миссии
3. Добавить в выгрузку лавок информацию о складах
    * Добавить поле ```features```, в котором будем для каждой лавки хранить массив фичей. Для скалада там будет лежать ```repair_warehouse```.
    * Для каждого склада создать полигон - зона полевого ремонта для ремонтников с данного склада. Для таких полигонов указать ```area_tag = warehouse_repair_field_on_car_zone```. Положить эти регионы в ```allowed_from_polygons```


4. Доработки со стороны диспатча - обработка нового типа драфтов, создание миссий

5. Новый флоу в боте:
    * Запрос координат у пользователя, определение **регион**а по ним, сохранение в базу
    * Кнопки *Полевой ремонт* и *Завершить ремонт и забрать самокат на склад* и обработчики для них

6. Изменить ручку начала ремонта. В параметрах обязательно должны быть vehicle_id и performer_id. И либо (depot_id + тип:warehouse), либо (region + тип:field). Добавить тип в сущность ремонта и в базу.
    * **Понять, как хранить в базе region и depot_id**, при условии, что для depot_id уже есть отдельная колонка

7. Добавить новую ручку для заверешения полевого ремонта с последующим забиранием самоката на склад. Внутри ручки такие же проверки как в обычной ручке заверешения ремонта, дополнительно надо навесить тэг ```need_warehouse_repair```, не снимать тэг ```broken``` и конечный статус ремонта будет ```failed_with_pickup```

8. Проработать в ПРО флоу миссии объезда самокатов в рамках полевого ремонта

9. Описать всё на вики. Добавить инструкцию по добавлению нового склада
