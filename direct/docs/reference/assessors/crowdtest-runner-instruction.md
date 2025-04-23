# Как работать с crowdtest runner в релизах  dna и uac

##### Общие инструкции
[Подключение асессоров к новому проекту](https://wiki.yandex-team.ru/users/ostroumov/asessory/podkljuchenie-novogo-proekta-k-testirovaniju-asessorami/?from=%2Fusers%2Fostroumov%2FPodkljuchenie-novogo-proekta-k-testirovaniju-asessorami%2F)  
[Запуск тестирования на асессорах через crowdtest runner](https://wiki.yandex-team.ru/search-interfaces/infra/crowdtest/create-launch/)

##### Репозиторий с конфигом и кодом
[Конфиги все тут](https://a.yandex-team.ru/arc_vcs/adv/frontend/services/webhooks/assessors)  
[Скрипт](https://a.yandex-team.ru/arc_vcs/adv/frontend/services/webhooks/server/routes/crowdtest.ts)  

##### Наши проекты в TestPalm
[UC](https://testpalm.yandex-team.ru/direct-frontend-crowd/)  
[DNA и Canvas](https://testpalm.yandex-team.ru/dna/)  
[ДК](https://testpalm.yandex-team.ru/directclient-assesors)  

##### Триггеры на запуск
[DNA](https://st.yandex-team.ru/admin/queue/DIRECT/triggers/30303)  

##### Процессы в Hitman
[UC](https://hitman.yandex-team.ru/projects/testing_direct/united_assessors_adapter_direct-frontend)  
[DNA и Canvas](https://hitman.yandex-team.ru/projects/testing_direct/united_assessors_adapter_direct_dna)  

##### Дырки
[1](https://puncher.yandex-team.ru/tasks?id=61080dd0c86c6d2512b626cb) и [2](https://puncher.yandex-team.ru/tasks?id=61080d95c86c6d2512b626ca)

### Чек-лист добавления нового проекта в скрипт (см. общие доки выше)

1. Настроить проект в Пальме
- добавить раннеры _United_ и _CrowdTest Runner_ с параметрами как в [проекте dna](https://testpalm.yandex-team.ru/dna/settings)  
 
 {% cut "скриншот" %}

   ![alt text](https://jing.yandex-team.ru/files/sonick/2022-03-16_11-14-15.png "скрин")

 {% endcut %}
 
- для _United_ в поле service должно быть название вашего сервиса как в Хитмане, но без части `united_assessors_adapter`  
 
 {% cut "скриншот 1" %}

   ![alt text](https://jing.yandex-team.ru/files/sonick/2022-03-16_11-17-25.png "скрин")  

 {% endcut %}
 
 {% cut "скриншот 2" %}

   ![alt text](https://jing.yandex-team.ru/files/sonick/2022-03-16_11-16-31.png "скрин")

 {% endcut %}
 
- раннер _CrowdTest Runner_ копируем без изменений  

2. Пробить дырки до Пальмы и Календаря (ссылки на дырки есть выше)
3. Добавить конфиг нового проекта и обновить скрипт (ссылка на конфиг есть выше)
4. Настроить процесс в Хитмане
- в настройках [проекта dna](https://hitman.yandex-team.ru/projects/testing_direct/united_assessors_adapter_direct_dna/?jobCreationTimeQuery=YEAR&jobPage=1&pageSize=20) в правом верхнем углу нажать на иконку "Скопировать процесс в буфер обмена"
- нажать создать проект в [в Хитмане](https://hitman.yandex-team.ru/projects/testing_direct/?jobCreationTimeQuery=MONTH&jobPage=1&pageSize=20) и ввести код %%united_assessors_adapter_название_проекта%% и вставить скопированные настройки, сохранить
5. Настроить триггер запуска скрипта в Трекере (ссылка на пример триггера есть выше)


## Запуск регрессии

{% note alert %}

Регрессия в релизах dna и uac запускается автоматически [нашим скриптом](https://a.yandex-team.ru/arc_vcs/adv/frontend/services/webhooks/server/routes/crowdtest.ts) с помощью [crowdtest runner](https://wiki.yandex-team.ru/search-interfaces/infra/crowdtest/create-launch/?from=%2Fsearch-interfaces%2Finfra%2Fassessors%2Fcreate-launch%2F) через TestPalm.  
[Триггер](https://st.yandex-team.ru/admin/queue/DIRECT/triggers/30303) запуска регрессии в очереди DIRECT срабатывает на условия:
- Тип тикета = **Release**
- Components = **App: dna** или **App: uac** 
- Status меняется на статус **Testing**

{% endnote %}

### Шаги запуска регрессии

1. **По умолчанию** для запуска берется **регулярная бронь**
2. Если по какой-то причине вы хотите запустить регрессию по **разовой брони**, то: 
- идем в [Hitman](https://hitman.yandex-team.ru/projects/testing_direct/united_assessors_adapter_direct_dna/?jobCreationTimeQuery=YEAR&jobPage=1&pageSize=20)
- открываем на редактирование переменную _booking_id_ (иконка карандаша)

 {% cut "скриншот" %}

   ![alt text](https://jing.yandex-team.ru/files/sonick/2022-03-16_10-59-01.png "скрин")

 {% endcut %}

- изменяем параметры   
тип: `Константа`  
значение: `номер вашей брони` из [бронировщика](https://booking.yandex-team.ru/#/)  

 {% cut "скриншот" %}

   ![alt text](https://jing.yandex-team.ru/files/sonick/2022-03-16_11-01-26.png "скрин")

 {% endcut %}

- **после запуска выставляем параметры обратно**, чтобы следующий запуск был в рамках регулярной брони!  
тип: `Groovy-функция`  
значение: `_.booking_id ?: null`  

3. **Как только релиз dna переходит в статус Testing вся регрессия запускается автоматически, поэтому все параметры брони должны быть корректно выставлены заранее!**

4. **Успешный запуск** 
- При успешном запуске робот RMP оставляет комментарий в релизный тикет со ссылкой на тикет в очереди DIRECTAS с запуском регрессии:  

 {% cut "скриншот" %}

   ![alt text](https://jing.yandex-team.ru/files/sonick/2022-03-16_10-35-17.png "скрин")

 {% endcut %}

- Дежурный релиз инженер ставит этот тикет на себя в Assignee, переводит его в Testing и ждет результаты выполнения регрессии асессорами

5. **Ошибки в запуске**
- Если при выполнении запуска появляются ошибки, то заводим баг и идем к staff:ayevttukh для оперативного решения проблемы

 {% cut "пример ошибки в запуске" %}

   ![alt text](https://jing.yandex-team.ru/files/sonick/2022-03-16_10-36-58.png "скрин")

 {% endcut %}

- Заходим на [релизную борду](https://st.yandex-team.ru/dashboard/50158) и смотрим в виджет "Регрессия для асессоров" создался ли тикет на регрессию (часто несмотря на ошибки тикеты создаются и задания запускаются)

 {% cut "пример ошибки в запуске" %}

   ![alt text](https://jing.yandex-team.ru/files/sonick/2022-03-16_10-47-21.png "скрин")

 {% endcut %}

- Если тикет создан, то идем в [Hitman](https://hitman.yandex-team.ru/projects/testing_direct/united_assessors_adapter_direct_dna/?jobCreationTimeQuery=YEAR&jobPage=1&pageSize=20) и убеждаемся, что задание запустилось без ошибок (в любом случае вам придет письмо на почту с результатами запуска) - в поле "Задания проекта" должно быть 3 свежих процесса с зеленым статусом. 
- Если все успешно, то переводим тикет DIRECTAS на регрессию в Testing и ждем результатов выполнения
- Если есть ошибки и тикет DIRECTAS не создан, то форсим решение бага со стороны [ayevttukh](https://staff.yandex-team.ru/ayevttukh)

### Если надо запустить асессоров вручную, а релизный тикет уже в статусе Testing
При переходе в статус Testing тикет на асессоров создается автоматически и занимает ближайшую регулярную бронь. Её можно двигать на пораньше/попозже и тогда никаких дополнительных действий делать не надо

Если бронь новая и хочется запустить на ней
- Надо сделать шаг 2 из предыдущего пункта по замене id брони
- В релизном тикете в поле "Run assessors" (добавить это поле в Стартреке) выставить значение "Обычный регресс"

 {% cut "скриншоты" %}

 ![alt text](https://jing.yandex-team.ru/files/shipovskikh/2022-04-15T09%3A01%3A25Z.3fd05a0.png "скрин")
 ![alt text](https://jing.yandex-team.ru/files/shipovskikh/2022-04-15T09%3A03%3A18Z.1b241d4.png "скрин")

 {% endcut %}

- Выставление значения "Обычный регресс" триггерит новый запуск асессоров (название триггера "[Re-Run] DNA Release Crowdtest Assessors"), робот РМП напишет комментарий в релизный тикет, чуть позже (секунд через 20) создастся новый тикет для прогона асессоров, старый можно закрыть
- После прогона асессоров надо id брони поменять обратно


## Добавление нового сьюта в регрессию

{% note alert %}

Все паки, которые запускаются в релизах, лежат в конфигах:
- [конфиг dna](https://a.yandex-team.ru/arc_vcs/adv/frontend/services/webhooks/assessors/dna-regress.json)  
- [конфиг uac](https://a.yandex-team.ru/arc_vcs/adv/frontend/services/webhooks/assessors/uac-full-regress.json)

{% endnote %}

1. Создаем новый сьют в TestPalm, копируем его id из урла
2. Добавляем в файл dna или uac новый сьют в конец списка

```
{
            "suite": "60a3d7c9fe51fe0011444b17", <----- номер вашего сьюта из TestPalm
            "control": "https://direct.yandex.ru/", <----- для uac скопировать из других конфигов сьютов
            "beta": "https://release.crowdtest.direct.yandex.ru/", <----- для uac скопировать из других конфигов сьютов
            "platform": "desktop", <----- для uac могут быть другие платформы, скопировать из других конфигов сьютов при необходимости
            "tags": ["dna_regress_resolve"],
            "browsers": ["Yandex.Browser", "FireFox"], <----- Браузеры для выполнения кейсов
            "hitman_title": "United", <----- не изменяем
            "testsuite_properties": {
                "hitman_booking_regular_id": "a4fca47c-9d6a-4fc0-b7d0-cc07f22d76b4", <----- регулярная бронь для запуска этого сьюта - либо новая, либо старая, но в нее надо будет добавить часы
                "special_condition": "Внимательно ознакомьтесь с инструкцией https://wiki.yandex-team.ru/eva/testing/projects/direct. Все расхождения результатов заводите в виде репортов", <----- для uac скопировать из других конфигов сьютов
                "tld_ignore": "yes", <----- не изменяем
                "env_ignore": "yes" <----- не изменяем
            }
        }
```

3. Создаем PR, проходим код ревью и мержим - в следующем релизе запустятся новые сьюты
