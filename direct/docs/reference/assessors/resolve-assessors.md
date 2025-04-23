# Тестирование задач асессорами в релизах Директа

## Инструкция релиз-инженера

1. Проверить, что собрался релиз dna  
   Если релиз не собрался, то нужно снять бронь под запуск [в Бронировщике](https://booking.yandex-team.ru/#/)  
  
   {% cut "Как снять бронь" %}  
   - переходим в [Хитман](https://hitman.yandex-team.ru/projects/testing_direct/direct_resolve_start/?jobCreationTimeQuery=YEAR&jobPage=1&pageSize=20) и останавливаем процесс - нажимаем на крестик возле запущенного процесса  
   ![alt text](https://jing.yandex-team.ru/files/sonch/browser_TafmwDEf2G.png "скрин остановки процесса")  
   - переходим в [Бронировщик]](https://booking.yandex-team.ru/#/ Бронировщик), находим бронь на сегодняшний релиз, нажимаем на красный ID и в открывшимся попапе нажимаем корзинку  
   ![alt text](https://jing.yandex-team.ru/files/sonch/browser_zqaFuqQAq5.png "скрин удаления брони")    

   {% endcut %} 
  
2. Проверить, что **[фильтр с тикетами](https://st.yandex-team.ru/issues/399629)** не пустой и в него попали тикеты с тегом `Resolve_QA` и тегами браузеров  
   Если фильтр пустой, то нужно снять бронь под запуск [в Бронировщике](https://booking.yandex-team.ru/#/). Как это сделать описано в п.1    
  
3. Запустить задание асессорам на тестирование резолвов
  
## Как запустить задание

1. **Скопировать id брони** из [Бронировщика](https://booking.yandex-team.ru/#/). Бронь с названием "Тестирование багов в релизе Директа" на день релиза

   {% cut "Как скопировать ID в Бронировщике" %}  

   - Навести на красный ID брони  
   ![alt text](https://jing.yandex-team.ru/files/sonick/2021-03-17_14-30-20.png "скрин id брони")  
   - В открывшемся попапе **кликнуть по желтому полю ID в правом верхнем углу** - ID скопируется, перейти к следующему шагу  
   ![alt text](https://jing.yandex-team.ru/files/sonick/2021-03-17_14-31-00.png "скрин id брони")  
     
   {% endcut %} 

2. **Изменить id брони** в [Хитмане](https://hitman.yandex-team.ru/projects/testing_direct/direct_resolve_start/?jobCreationTimeQuery=YEAR&jobPage=1&pageSize=20)
   - Найти в Хитмане параметр `booking_id` и нажать карандаш

    {% cut "скрин id брони в Хитмане" %}  
    
    ![alt text](https://jing.yandex-team.ru/files/sonch/browser_3yj5xVkbgC.png "скрин id брони в Хитмане")  
    
    {% endcut %} 
    
    - В поле `Значение` вставляем скопированный в Бронировщике ID и жмем Редактировать

    {% cut "скрин изменения брони" %}  
    
    ![alt text](https://jing.yandex-team.ru/files/sonch/browser_GKTYWiz6Mz.png "скрин изменения брони")  
    
    {% endcut %} 

3. **Запустить процесс** в [Хитмане](https://hitman.yandex-team.ru/projects/testing_direct/direct_resolve_start/?jobCreationTimeQuery=YEAR&jobPage=1&pageSize=20)  
   В блоке "Триггеры" нажать "Запустить сейчас
   
   {% cut "скрин запуска задания" %}  
   
   ![alt text](https://jing.yandex-team.ru/files/sonch/browser_gYqWfTnO6z.png "скрин запуска задания")  
   
   {% endcut %} 

4. В блоке задач проекта появится процесс. Cледить за выполнением работы асессоров можно по статусу этого процесса  

   {% cut "Как найти процесс" %}  
   
   ![alt text](https://jing.yandex-team.ru/files/sonch/browser_2f0LHg3aeQ.png "скрин запущенного процесса")  
   
   {% endcut %} 

5. После завершения тестирования резолвов асессорами, релиз-инженер проходится по всем тикетам из **[фильтра](https://st.yandex-team.ru/issues/399629)** и смотрит на комментарии от асессоров, проставляет компоненту `Tested apps` и разбирает баги, если они были найдены.
