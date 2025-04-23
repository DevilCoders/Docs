# StaffStandart
Скрипт для создания тикетов на тестирование и текстов для раскатки  ы ST+ для созданий версий и ранов в TP

### Установка зависимостей
`pip3 install -i https://pypi.yandex-team.ru/simple yandex_tp_api_client`

`pip3 install -i https://pypi.yandex-team.ru/simple/ startrek_client`

### Входные данные

Перед каждым запуском скрипта проверьте корректность следующих данных в файле variable.json:
* версия приложений для тестирования `version_app`
* идентификатор версии для тестирования `id_version`
* проверить корректность борда и фильтров (обновить запросы в фильтрах в стартреке  на соответствующую версию тестирования)

Для работы скрипта необходимо заполнить следующие поля:

####  Поля, которые нужно заполнить один раз перед первым использованием скрипта

* `AUTH_ST` - токен для авторизации в StarTrack (для его получения порйдите по ссылке https://oauth.yandex-team.ru/authorize?response_type=token&client_id=5f671d781aca402ab7460fde4050267b)

* `AUTH_TP` - токен для авторизации в TestPalm (для его получения пройдите по ссылке https://testpalm.yandex-team.ru/internal/profile)

* `requester` - ваш логин в Yandex

* `beta` - Принимает значение `True`\ `False` в зависимости от того, нужно ли создавать тикет для текстов для беты

* `create_version_autotest` - Принимает значение `True`\ `False` в зависимости от того, нужно ли создавать версию для автотестов в TestPalm

####  Поля, которые нужно заполнять каждый раз перед  использованием скрипта

* `version_app` - версия тестируемого релиза 

* `dashboard` - ссылка на dashboard для тестирования версии

* `all_ticket` - фильтр всех тикетов за фикшеных в проверяемом релизе (пример фильтра: `Queue: MOBILEMAIL AND Components: Android AND "Fix Version": "Android 4.3.1"`)

* `backlog_bug` - фильтр всех багов из бэклога зафикшеных в проверяемом релизе (пример фильтра: `Queue: MOBILEMAIL and Components: iOS AND ("Fix Version": "iOS 3.65" ) and Type: Bug AND "Affected Version": ! "iOS 3.65"`  )

* `backlog_task` - фильтр всех тасков из бэклога зафикшеных в проверяемом релизе (пример фильтра: `Queue: MOBILEMAIL and Components: iOS and "Affected Version": ! "iOS 3.65" AND "Fix Version": "iOS 3.65" and (Type: Task OR Type: "Technical Task" OR Type: Improvement )` )

* `found_bugs` - фильтр все  багов, найденных в процессе тестирования (пример фильтра: `Queue: MOBILEMAIL AND Components: Android AND "Affected Version": "Android 4.3.1"`)

* `release_type` - Тип релиза. Может принимать значение: Feature, Technical, Hotfix, Out of turn

* `release_ticket` - Если скрипт запускатеся для создания тикетов на тексты, тестирвоание АМ, реакта отдельно от того, чтобы создать сам тикет на тестирование и версию в пальме, то в данном параметре необходимо указать тикет мна тестирования версии. Если все указанные тикеты создаются весте с тикетом на тестирование, это параметр можно оставить прежним или пустым.

* `text` -  информация для создания тикетов на тексты в очереди редакторов EDIT. Для каждого тикета должен быть создан массив следующего вида:
    ```
    {
      "summary":"[Beta] Текст для релиза мобильной почты",  //Summary для создаваемого тикета
      "deadline":"9.01.2019 13:00",                         // Дедлайн выполнение задачи. Будет прокинут в Описание тикета
      "description":[                                       // Массивом строк указать, что нового в версии
        "При добавлении фото/картинки при написании письма открывается не просто папка с картинками, а стандартная галерея",
        "При тапе на Имя папки в топ-баре - список писем пролистывается к началу",
        "Возможность выбора: группировать письма или нет (если поставить сейчас бету сборку с Google Play, то можно увидеть что есть папки Входящие/Расслки/Социальные сети. Теперь будет возможность выбора, включить или выключить эту функцию)",
        "баг фиксы"]
    }
    ```

* `translate` -  информация для создания тикетов на перевод текста в очереди перевощдчиков TANKER. Должна быть указана следующая информация:
    ```
    {
      "summary":"[Mail] - Translate - EN, TR, UK - Перевод What's New для Яндекс.Почта",    //Summary для создаваемого тикета
      "language":"EN, TR, UK",          //Языки на которые делаются переводы 
      "deadline":"9.01.2019 13:00",     // Дедлайн выполнение задачи. Будет прокинут в Описание тикета
      "description":[                   // Текст для перевода разбитый на массив строк
        "Отгремели праздничные салюты, закончились салаты, Яндекс.Почта готовится сменить наряд на деловой:",
        "— Для добавления к письму изображения теперь используется стандартная галерея — должно быть удобнее, чем папка с картинками, как раньше;",
        "— Чтобы вернуться из глубины списка к новым письмам, больше не нужно долго листать наверх, достаточно нажать на название папки;",
        "— Конечно, поубавилось ошибок. Спасибо, что сообщаете нам о них."
        ]
  }
  ```

####  Пример заполнения variable.json 

* Android:
    ```
        {
          "AUTH_ST": "AQAD-*****",
          "AUTH_TP": "2862feea-*****",
          "AUTH_YT": "AQAD-*****",
          "requester": "arovkova",
          "queue": "MOBILEMAIL",
        
          "testpalm_project": "mobmail_android",
          "platform": "Android",
          "beta": true,
        
          "testpalm":"https://testpalm.yandex-team.ru/mobmail_android/version",
          "suites":[
            { "key":"55dd99dee4b0c375e766e328", "enviroment":"Android 5.0.x Smart", "run": "[White] [Beta] Acceptance"},
            { "key":"55dd99dee4b0c375e766e328", "enviroment":"Android 8.x.x Smart", "run": "[Dark] [Prod] Acceptance"},
            { "key":"55d1cff7e4b05f8489e1e96f", "enviroment":"Android 7.x.x Smart", "run": "Acceptance w/o Autotest"},
            { "key":"582503e7889550027e067f12", "enviroment":"", "run": "Pre-release cases"},
            { "key":"5553a4dfe4b042686d1478ab", "enviroment":"", "run": "Ответственному за релиз"},
            { "key":"59525012c612333cf178347b", "enviroment":"", "run": "Not_asessors"}
            ],
        
          "dashboard": "https://st.yandex-team.ru/dashboard/22946",
          "all_ticket": "Queue: MOBILEMAIL and Components: Android and Sprint: \"[version]\"",
          "backlog_bug": "Queue: MOBILEMAIL and Components: Android AND (Sprint: [version]  OR \"Fix Version\": \"Android [version]\" ) and Type: Bug AND \"Affected Version\": ! \"Android [version]\" ",
          "backlog_task": "Queue: MOBILEMAIL and Components: Android and \"Affected Version\": ! \"Android [version]\" AND (Sprint: [version]  OR \"Fix Version\": \"Android [version]\" ) and Type: Task",
          "found_bugs": "Queue: \"Yandex Mobile Mail\" and Components: Android and \"Affected Version\": \"Android [version]\"",
        
          "create_version_autotest":true,
          "version_app": "0.14.1",
          "release_type": "Feature",
        
          "release_ticket":"MOBILEMAIL-13298",
        
          "text":[
            {
              "summary":"[Beta] Текст для релиза мобильной почты",
              "deadline":"9.01.2019 13:00",
              "description":[
                "При добавлении фото/картинки при написании письма открывается не просто папка с картинками, а стандартная галерея",
                "При тапе на Имя папки в топ-баре - список писем пролистывается к началу",
                "Возможность выбора: группировать письма или нет (если поставить сейчас бету сборку с Google Play, то можно увидеть что есть папки Входящие/Расслки/Социальные сети. Теперь будет возможность выбора, включить или выключить эту функцию)",
                "баг фиксы"]
            },
            {
              "summary":"[Prod] Текст для релиза мобильной почты",
              "deadline":"9.01.2019 13:00",
              "description":[
                "При добавлении фото/картинки при написании письма открывается не просто папка с картинками, а стандартная галерея",
                "При тапе на Имя папки в топ-баре - список писем пролистывается к началу",
                "баг фиксы"]
            }
          ],
          "translate":{
              "summary":"[Mail] - Translate - EN, TR, UK - Перевод What's New для Яндекс.Почта",
              "language":"EN, TR, UK",
              "deadline":"9.01.2019 13:00",
              "description":[
                "Отгремели праздничные салюты, закончились салаты, Яндекс.Почта готовится сменить наряд на деловой:",
                "— Для добавления к письму изображения теперь используется стандартная галерея — должно быть удобнее, чем папка с картинками, как раньше;",
                "— Чтобы вернуться из глубины списка к новым письмам, больше не нужно долго листать наверх, достаточно нажать на название папки;",
                "— Конечно, поубавилось ошибок. Спасибо, что сообщаете нам о них."
                ]
          }
        }
     ```
* iOS:
    ```
      {
          "AUTH_ST": "OAuth AQAD-**",
          "AUTH_TP": "2862feea-36ae-41ec-ae7b-**",
          "AUTH_YT": "AQAD-qJSJznBAAAA-**",
          "requester": "arovkova",
          
          "testpalm_project": "mobmail_ios",
          "platform": "iOS",
          "beta": false,
        
          "external_mail":[
            "Google",
            "MailRu",
            "Outlook"
          ],
        
          "suites":[
            { "key":"56f4d486c6123373421ddfd5", "enviroment":"iOS 12", "run": "Acceptance Yandex"},
            { "key":"59c37d55ac9801d3a4c58a26", "enviroment":"iOS 12", "run": "miniAcceptance [Dark theme + mobile network] "},
            { "key":"59c37d55ac9801d3a4c58a26", "enviroment":"iOS 11", "run": "miniAcceptance [Light theme + wi-fi]"},
            { "key":"59c37d55ac9801d3a4c58a26", "enviroment":"iOS 10", "run": "miniAcceptance [Experiments + wi-fi]"},
            { "key":"5706265c8895507aa3070067", "enviroment":"", "run": "[iPhone] Business_Logic w/o One_device tag"},
            { "key":"56f52d6dc6123373421df5f9", "enviroment":"", "run": "[iPad] Business_Logic w/o One_device tag"},
            { "key":"56fa3b7e889550743662539f", "enviroment":"", "run": "Ответственному за релиз"},
            { "key":"5704dae7c6123304e8e7d666", "enviroment":"", "run": "Update cases"},
            { "key":"5b689715798633106cd2025d", "enviroment":"", "run": "Specific mobile cases"},
            { "key":"5b689715798633106cd2025d", "enviroment":"", "run": "60min_Platform Specific"},
            { "key":"5b695a702afa3ad3c150f974", "enviroment":"", "run": "60min_BL_not assessors"}
          ],
        
          "testpalm":"https://testpalm.yandex-team.ru/mobmail_ios/version",
        
          "dashboard": "https://st.yandex-team.ru/dashboard/22946",
          "all_ticket": "Queue: MOBILEMAIL and Components: iOS and Sprint: \"[version]\"",
          "backlog_bug": "Queue: MOBILEMAIL and Components: iOS AND (Sprint: [version]  OR \"Fix Version\": \"iOS [version]\" ) and Type: Bug AND \"Affected Version\": ! \"iOS [version]\" ",
          "backlog_task": "Queue: MOBILEMAIL and Components: iOS and \"Affected Version\": ! \"iOS [version]\" AND (Sprint: [version]  OR \"Fix Version\": \"iOS [version]\" ) and Type: Task",
          "found_bugs": "Queue: \"Yandex Mobile Mail\" and Components: iOS and \"Affected Version\": \"iOS [version]\"",
        
          "create_version_autotest":false,
          "version_app": "1.6",
          "release_type": "Feature",
        
          "release_ticket":"MOBILEMAIL-12960",
        
          "text":[
            {
              "summary":"[Beta] Текст для релиза мобильной почты",
              "deadline":"9.01.2019 13:00",
              "description":[
                "При добавлении фото/картинки при написании письма открывается не просто папка с картинками, а стандартная галерея",
                "При тапе на Имя папки в топ-баре - список писем пролистывается к началу",
                "Возможность выбора: группировать письма или нет (если поставить сейчас бету сборку с Google Play, то можно увидеть что есть папки Входящие/Расслки/Социальные сети. Теперь будет возможность выбора, включить или выключить эту функцию)",
                "баг фиксы"]
            }
          ],
          "translate":{
              "summary":"[Mail] - Translate - EN, TR - Перевод What's New для Яндекс.Почта",
              "language":"EN, TR",
              "deadline":"9.01.2019 13:00",
              "description":[
                "Отгремели праздничные салюты, закончились салаты, Яндекс.Почта готовится сменить наряд на деловой:",
                "— Для добавления к письму изображения теперь используется стандартная галерея — должно быть удобнее, чем папка с картинками, как раньше;",
                "— Чтобы вернуться из глубины списка к новым письмам, больше не нужно долго листать наверх, достаточно нажать на название папки;",
                "— Конечно, поубавилось ошибок. Спасибо, что сообщаете нам о них."
                ]
          }
        }
    ```

### Работа скрипта

1. Запускаем скрипт  `python3 StaffStandart.py` и попадаем в меню выбора сценариев работы скрипта
      ```
      arovkova-osx:Create_tickets_and_version arovkova$ python3 StaffStandart.py
        2019-01-15 18:04:52.748581
                Hi!
                This is script for create tickets for version!
                Let's go! ;)
            2019-01-15 18:04:52.748649   Please, choose scenario for running script:
                     0) Create version in StartTrack;
                     1) Create ticket for testing and version in TestPalm;
                     2) Create ticket for text in our queue;
                     3) Create ticket for testing AM;
                     4) Create ticket for testing React;
                     5) Create ticket for text in EDIT queue;
                     6) Create ticket for translate text
                     7) Exit

                    Scenario (enter numbers by spaces): 
      ```
2. Данный скрипт умеет:
    * Создавать версию в StarTrack
    * Создавать тикет на тестирование и версию в TestPalm
    * Создавать тикет на тексты, тикет на тестирование АМ/React в нашей очереди
    * Создавать тикеты на тексты в очереди редакторов
    * Создавать тикет на перевод текстов в очереди Переводчиков.
3.  В предложенном поле через пробел, запятую, тире... вводим цифры сценариев в данном запуске и нажимаем Enter:
    
    `Scenario (enter numbers by spaces):  4 1 3`
4. Если Создаем тикет на тестирование то будет выведеня ряд вопросов на утверждение:
    * Вывод иноформации про версии тестируемого билда и его ID в StarTrack и подтверждение, что информация корректна:
        ```
        Check input data for create tickets and versions:
        App version = 0.17.0
        Is data correct? (tap 'Enter' for continue; 'No' for break)
        ```
        
     * Уточнение про тип релиза. Изначальное значение берется из файла variable.json, то тут есть возможность изменить, написав необходимый тип:
        ``` 
        Release type is "Feature". Is it correct? (tap 'Enter' for continue; enter release type [Feature, Technical, Hotfix, Out of turn] for change: 
        ```
5. Последсодание тикета на тестирование, его ключ выводится в консоль, и его модно сразу занести в поле `release_ticket` в файле variable.json

      `2019-01-15 18:04:55.783026   Ticket for testing was created in Startrek:  MOBILEMAIL-12985`
 6. Все остальные сценарии не требуют дополнительных действий.
