### Установка и обновление

Установка:

`pip3 install -i https://pypi.yandex-team.ru/simple yandex_tp_api_client`

Обновление:

`pip3 install -i https://pypi.yandex-team.ru/simple yandex_tp_api_client --upgrade`

### Включение логирования

В файле, в котором используется клиент, нужно прописать:

```
import logging

logger = logging.getLogger('testpalm_logger')
logging.basicConfig(format=u'%(asctime)s [%(levelname)s] %(module)s: %(message)s', 
                    level=logging.INFO)
```

### Примеры использования:

#### Инициализация класса:

`client = TestPalmClient(auth=os.environ['OAUTH_TOKEN_TESTPALM'])`

#### Проекты

##### Получение проекта

```
client.get_project(project='mobilemail', include='title')
```

Обязательный параметр: 
- `project`

Необязательные параметры: 
- `include` (какие поля включить в результат)
- `exclude` (какие поля исключить из результата)

Параметры `include`, `exclude` не могут использоваться в запросе одновременно.

[Описание используемой ручки](https://testpalm-api.yandex-team.ru/#/Project/get_projects__projectId_)

##### Создание проекта

```
client.create_project(data=data)
```

Обязательный параметр: 
- `data`

[Описание используемой ручки](https://testpalm-api.yandex-team.ru/#/Project/post_projects)


##### Обновление настроек проекта

```
client.update_project(project='mobilemail', 
                      data=data)
```

Обязательные параметры:
- `project` 
- `data`

[Описание используемой ручки](https://testpalm-api.yandex-team.ru/#/Project/put_projects__projectId_)


##### Клонирование проекта

```
client.clone_project(project='mobmail_ios', 
                     new_project='tests_mobmail_ios', 
                     clone_testcases=False, 
                     title='Copy of mobmail_ios')
```

Обязательные параметры: 
- `project`
- `new_project`

Необязательные параметры: 
- `title` - название проекта. Значение по умолчанию - `Copy`
- `clone_testcases` - клонировать ли тесткейсы. Значение по умолчанию - `True`
- `clone_testruns` - клонировать ли тестраны. Значение по умолчанию - `True`
- `clone_versions` - клонировать ли версию. Значение по умолчанию - `True`

[Описание используемой ручки](https://testpalm-api.yandex-team.ru/#/Project/post_projects__projectId__clone__newProjectId_)

##### Удаление проекта

```
client.delete_project(project='mobmail_ios', 
                      permanent=True)
```

Обязательный параметр: 
- `project`

Необязательный параметр:
- `permanent` - удалить проект навсегда. Значение по умолчанию - `False`

[Описание используемой ручки](https://testpalm-api.yandex-team.ru/#/Project/delete_projects__projectId_)

#### Версии

##### Получение списка версий:

```
client.get_versions(project=Projects.mobilemail, 
                    statuses=[VersionStatus.created, VersionStatus.started], 
                    include='status,title')
```

Обязательный параметр: 
- `project`

Необязательные параметры: 
- `statuses` (отфильтровать версии по статусу)
- `title` (отфильтровать версии по заголовку)
- `include` (какие поля включить в результат)
- `exclude` (какие поля исключить из результата)

Параметры `include`, `exclude` не могут использоваться в запросе одновременно.


[Описание используемой ручки](https://testpalm-api.yandex-team.ru/#/Version/get_version__projectId_)

##### Получение конкретной версии по id:

```
client.get_version(project=Projects.mobilemail, 
                   version_id='AssessorsiOS3890part_speech_kit')
```

Обязательные параметры: 
- `project`
- `version_id`

Необязательные параметры: 
- `statuses` (отфильтровать версии по статусу)
- `title` (отфильтровать версии по заголовку) 
- `include` (какие поля включить в результат)
- `exclude` (какие поля исключить из результата)

Параметры `include`, `exclude` не могут использоваться в запросе одновременно.

[Описание используемой ручки](https://testpalm-api.yandex-team.ru/#/Version/get_version__projectId___versionId_)


##### Создание версии
```
client.create_version(project=Projects.mobilemail, 
                      data={'id': 'Название версии'})

```

Обязательные параметры: 
- `project`
- `data`

[Описание используемой ручки](https://testpalm-api.yandex-team.ru/#/Version/post_version__projectId_)


##### Добавление комментария к версии
```
client.add_comment_for_version(project=Projects.mobmail_ios, 
                               version_id='iOS4.1.0', 
                               comment='текст комментария')

```

Обязательные параметры: 
- `project`
- `version_id`
- `comment` - текст комментария

[Описание используемой ручки](https://testpalm-api.yandex-team.ru/#/Version/post_version__projectId___versionId__comments)


##### Обновление комментария к версии
```
client.update_version_comment(project=Projects.mobmail_ios, 
                              comment_id='5e457a6d97c07600261b28cb', 
                              comment='new comment')

```

Обязательные параметры: 
- `project`
- `comment_id`
- `comment` - новый текст комментария

[Описание используемой ручки](https://testpalm-api.yandex-team.ru/#/Version/patch_version__projectId__comments__commentId_)


#### Раны

##### Получение списка ранов:

```
client.get_testruns(project=Projects.mobilemail, 
                    limit=1, 
                    skip=2, 
                    include="status,createdBy,title,startedTime", 
                    expression=str({"type": Operators.eq, "key": Fields.status, "value": RunStatus.created}).replace("'", '"'))
```

Обязательный параметр: 
- `project`

Необязательные параметры: 
- `limit`
- `skip`
- `include`
- `exclude`
- `expression`

Параметры `include`, `exclude` не могут использоваться в запросе одновременно.

Про `expression` подробнее тут https://wiki.yandex-team.ru/testpalm/testpalmdoc/expression-filter/

[Описание используемой ручки](https://testpalm-api.yandex-team.ru/#/Testrun/get_testrun__projectId_)

##### Получение списка ранов сгруппированных по статусу:

```
client.get_testruns_by_status(project=Projects.mobilemail, 
                              include='id')
```

Обязательный параметр: 
- `project`

Необязательные параметры: 
- `version`
- `include`
- `exclude`
- `expression`

Параметры `include`, `exclude` не могут использоваться в запросе одновременно.

Про `expression` подробнее тут https://wiki.yandex-team.ru/testpalm/testpalmdoc/expression-filter/

[Описание используемой ручки](https://testpalm-api.yandex-team.ru/#/Testrun/get_testrun__projectId__by_status)

##### Получение конкретного рана по его id:

```
client.get_testrun(project=Projects.mobmail_ios, 
                   testrun_id='5e330d9346af8470fb828381', 
                   include="id,status,createdBy,title,startedTime")
```

Обязательные параметры: 
- `project`
- `testrun_id`

Необязательные параметры: 
- `include`
- `exclude` 

Параметры `include`, `exclude` не могут использоваться в запросе одновременно.

[Описание используемой ручки](https://testpalm-api.yandex-team.ru/#/Testrun/get_testrun__projectId___testrunId_)

##### Создание рана из сьютов

```
client.create_testrun_from_suite(project=Projects.mobmail_ios, 
                                 data=data)
```

[Пример данных](https://paste.yandex-team.ru/929700)

Обязательные параметры: 
- `project`
- `data`

##### Создание рана из кейсов
```
client.create_testrun_from_cases(project=Projects.mobmail_ios, 
                                 data=data)
```

[Пример данных](https://paste.yandex-team.ru/929695)

Обязательные параметры: 
- `project`
- `data`

##### Получение конкретного тесткейса из тестрана:

```
client.get_testcase_from_testrun(project=Projects.mobilemail, 
                                 testrun_id='5e25b76346af84170c999323', 
                                 case_id=6101)
```

Обязательные параметры: 
- `project`
- `testrun_id`
- `case_id`

Необязательные параметры: 
- `include`
- `exclude`

Параметры `include`, `exclude` не могут использоваться в запросе одновременно.

[Описание используемой ручки](https://testpalm-api.yandex-team.ru/#/Testrun/get_testrun__projectId___testrunId___testcaseId_)


##### Изменить статус тестрана на FINISHED

```
client.finish_testrun(project=Projects.mobmail_ios, 
                      testrun_id='5e25729e965c5d002cf71f35')

```

Обязательные параметры: 
- `project`
- `testrun_id`

[Описание используемой ручки](https://testpalm-api.yandex-team.ru/#/Testrun/post_testrun__projectId___testrunId__finish)

##### Получение комментариев к тестрану

```
client.get_testrun_comments(project=Projects.mobmail_ios, 
                            testrun_id='5e4412a331f0e30026376ae9')

```

Обязательные параметры: 
- `project`
- `testrun_id`

Необязательные параметры: 
- `include`
- `exclude`

Параметры `include`, `exclude` не могут использоваться в запросе одновременно.

[Описание используемой ручки](https://testpalm-api.yandex-team.ru/#/Testrun/get_testrun__projectId___testrunId__comments)


##### Добавление комментария к тестрану

```
client.add_testrun_comment(project=Projects.mobmail_ios, 
                           testrun_id='5e4412a331f0e30026376ae9',
                           comment='текст комментария')

```

Обязательные параметры: 
- `project`
- `testrun_id`
- `comment`

[Описание используемой ручки](https://testpalm-api.yandex-team.ru/#/Testrun/post_testrun__projectId___testrunId__comments)

##### Правка комментария к тестрану

```
client.update_testrun_comment(project=Projects.mobmail_ios, 
                              testrun_id='5e4412a331f0e30026376ae9', 
                              comment_id='5e4575302e58e40030399dff', 
                              comment='новый текст комментария')

```

Обязательные параметры: 
- `project`
- `testrun_id`
- `comment_id`
- `comment`

[Описание используемой ручки](https://testpalm-api.yandex-team.ru/#/Testrun/patch_testrun__projectId___testrunId__comments__commentId_)


##### Удаление комментария к тестрану

```
client.delete_testrun_comment(project=Projects.mobmail_ios, 
                              testrun_id='5e4412a331f0e30026376ae9', 
                              comment_id='5e4575302e58e40030399dff')

```

Обязательные параметры: 
- `project`
- `testrun_id`
- `comment_id`

[Описание используемой ручки](https://testpalm-api.yandex-team.ru/#/Testrun/delete_testrun__projectId___testrunId__comments__commentId_)


##### Добавление комментария к тесткейсу в тестране

```
client.add_comment_for_testcase_in_testrun(project=Projects.mobmail_ios,
                                           testrun_id='5e456d7c9fcbfa71d3130c9d',
                                           case_id=1494,
                                           comment='текст комментария')

```

Обязательные параметры: 
- `project`
- `testrun_id`
- `case_id`
- `comment`

[Описание используемой ручки](https://testpalm-api.yandex-team.ru/#/Testrun/delete_testrun__projectId___testrunId__comments__commentId_)

##### Получение комментариев к тесткейсу в тестране

```
client.get_testcase_comments_in_testrun(project=Projects.mobmail_ios,
                                        testrun_id='5e456d7c9fcbfa71d3130c9d',
                                        case_id=1494)

```

Обязательные параметры: 
- `project`
- `testrun_id`
- `case_id` или `case_uuid` - если указать `case_id`, то метод сам найдет `uuid` кейса внутри рана. 
Если в ране есть несколько одинаковых кейсов, нужно передавать `case_uuid` вместо `case_id`

Необязательные параметры: 
- `include`
- `exclude`

Параметры `include`, `exclude` не могут использоваться в запросе одновременно.

[Описание используемой ручки](https://testpalm-api.yandex-team.ru/#/Testrun/get_testrun__projectId___testrunId___testcaseId__comments)

##### Правка комментария к тесткейсу в тестране

```
client.update_testcase_comment_in_testrun(project=Projects.mobmail_ios,
                                          testrun_id='5e456d7c9fcbfa71d3130c9d',
                                          case_id=1494,
                                          comment_id='5e4a99ad5412f30027ae860f',
                                          new_comment='текст нового комментария')

```

Обязательные параметры: 
- `project`
- `testrun_id`
- `case_id` или `case_uuid` - если указать `case_id`, то метод сам найдет `uuid` кейса внутри рана. 
Если в ране есть несколько одинаковых кейсов, нужно передавать `case_uuid` вместо `case_id`
- `comment_id`
- `new_comment`

[Описание используемой ручки](https://testpalm-api.yandex-team.ru/#/Testrun/patch_testrun__projectId___testrunId___testcaseId__comments)


#### Кейсы

##### Получение кейсов

```
(client.get_testcases(project=Projects.mobilemail, 
                      limit=1, 
                      skip=2, 
                      include="status,createdBy,name",
                      expression=str({"type": Operators.eq, "key": Fields.status, "value": CaseStatus.archived}).replace("'", '"'))
```

Обязательный параметр: 
- `project`

Необязательные параметры: 
- `limit`
- `skip`
- `include`
- `exclude`
- `expression`
- `searchQuery`

[Описание используемой ручки](https://testpalm-api.yandex-team.ru/#/Testcase/get_testcases__projectId_)

##### Получение конкретного тесткейса по id

```
client.get_testcase(project=Projects.mobilemail, 
                    case_id=3, 
                    include='status,name')
```

Обязательный параметр: 
- `project`
- `case_id`

Необязательные параметры: 
- `include`
- `exclude`

Параметры `include`, `exclude` не могут использоваться в запросе одновременно.

[Описание используемой ручки](https://testpalm-api.yandex-team.ru/#/Testcase/get_testcases__projectId_)

##### Получение кейсов из сьюта
```
client.get_testcases_from_suite(project=Projects.mobmail_ios, 
                                suite_id='5dc58ccbf97f248809cd1995')
```

Обязательный параметр: 
- `project`
- `suite_id`

Необязательные параметры: 
- `include`
- `exclude`
- `limit`
- `skip`

Параметры `include`, `exclude` не могут использоваться в запросе одновременно.

[Описание используемой ручки](https://testpalm-api.yandex-team.ru/#/Testcase/get_testcases__projectId__suite__suiteId_)


##### Получение связей кейса с другими кейсами

```
client.get_case_links(project=Projects.mobmail_ios, 
                      case_id=1494)
```

Обязательный параметр: 
- `project`
- `case_id`

[Описание используемой ручки](https://testpalm-api.yandex-team.ru/#/Testcase/get_testcases_link__projectId___testcaseId_)


##### Создание кейса
```
client.create_testcase(project=Projects.mobmail_ios, 
                       data=data)
```

Обязательные параметры: 
- `project`
- `data`

[Описание используемой ручки](https://testpalm-api.yandex-team.ru/#/Testcase/post_testcases__projectId_)


##### Создание кейса
```
client.create_testcase(project=Projects.mobmail_ios, 
                       data=data)
```

Обязательные параметры: 
- `project`
- `data`

[Описание используемой ручки](https://testpalm-api.yandex-team.ru/#/Testcase/post_testcases__projectId_)

##### Создание нескольких кейсов
```
client.create_testcases(project=Projects.mobmail_ios, 
                        data=data)
```

Обязательные параметры: 
- `project`
- `data` - список кейсов

[Описание используемой ручки](https://testpalm-api.yandex-team.ru/#/Testcase/post_testcases__projectId__bulk)


##### Удаление кейсов
```
client.delete_testcases(project=Projects.mobmail_ios, 
                        case_ids=[6254], 
                        permanently=True)
```

Обязательные параметры: 
- `project`
- `case_ids` - список id кейсов

Необязательный параметр:
- `permanently` - удалить кейс совсем (нельзя восстановить). Значение по умолчанию - `False`

[Описание используемой ручки](https://testpalm-api.yandex-team.ru/#/Testcase/delete_testcases__projectId__bulk)


##### Обновление кейса

```
client.update_testcase(project=Projects.mobmail_ios, 
                       data={
                               "id": 732, 
                               "description": "test"
                            })
```

Обязательные параметры: 
- `project`
- `data`

[Описание используемой ручки](https://testpalm-api.yandex-team.ru/#/Testcase/patch_testcases__projectId_)


##### Обновление нескольких кейсов

```
client.update_testcases(project=Projects.mobmail_ios, 
                        data=[{
                                 "id": 732, 
                                 "description": "test"
                              }, {
                                 "id": 800, 
                                 "estimatedTime": 8000
                              }])
```

Обязательные параметры: 
- `project`
- `data` - список кейсов

[Описание используемой ручки](https://testpalm-api.yandex-team.ru/#/Testcase/patch_testcases__projectId__bulk)


##### Клонирование кейсов

```
client.clone_testcases(source_project=Projects.mobmail_ios, 
                       destination_project=Projects.mobilemail, 
                       case_ids=[1063])
```

Обязательные параметры: 
- `source_project` - проект, из которого клонируются кейсы
- `destination_project` - проект, в который клонируются кейсы
- `case_ids` - список id кейсов

[Описание используемой ручки](https://testpalm-api.yandex-team.ru/#/Testcase/post_testcases_clone__sourceProjectId___destinationProjectId_)

##### Получение статистики кейсов через метод get_testcases

```
client.get_testcases(project=self.__project, 
                      include='stats,id',
                      expression=str({
                                        "type": Operators.eq,
                                        "key": Fields.status,
                                        "value": CaseStatus.actual
                                     }).replace("'", '"'))
```


##### Обновление аттрибутов кейса

```
client.update_testcases_attribute_value(project=Projects.mobilemail, 
                                        case_ids=[1494, 1532],
                                        action=Action.add,
                                        attr_name='Tag',
                                        attr_values=['123', '234'])
```

Обновляет аттрибуты кейсов. Создает новый аттрибут, если его не существует. 
Добавляет новые значения аттрибута, если таких значений не было ранее. 

Обязательные параметры: 
- `project`
- `case_ids`
- `action`
- `attr_name`    (название аттрибута)
- `attr_values`  (список значений аттрибута)

##### Получение истории событий с кейсами

```
client.get_testcases_events_by_project(project=Projects.mobmail_ios, 
                                       limit=5)
```

Обязательный параметр: 
- `project`

Необязательные параметры: 
- `limit`
- `skip`
- `include`
- `exclude`
- `expression`

[Описание используемой ручки](https://testpalm-api.yandex-team.ru/#/Testcase/get_eventslog__projectId_)


##### Получение списка связей тесткейса с другими кейсами

```
client.get_testcase_links(project=Projects.mobilemail, 
                          case_id=1494)
```


Обязательные параметры: 
- `project`
- `case_id`

[Описание используемой ручки](https://testpalm-api.yandex-team.ru/#/Testcase/get_testcases_link__projectId___testcaseId_)

##### Создание связи тесткейса с другим тесткейсом

```
client.create_testcase_link(project=Projects.mobilemail, 
                            case_id=2,
                            linking_project=Projects.mobilemail, 
                            linking_case_id=4, 
                            link_type=LinkType.child)
```


Обязательные параметры: 
- `project`
- `case_id`
- `linking_project` - название проекта, в котором находится линкуемый кейс
- `linking_case_id` - id линкуемого кейса
- `link_type` - тип связи: `child`, `parent`, `related`

[Описание используемой ручки](https://testpalm-api.yandex-team.ru/#/Testcase/post_testcases_link__projectId___testcaseId_)


##### Удаление связи тесткейса с другим тесткейсом

```
client.delete_case_link(project=Projects.mobilemail, 
                        case_id=2, 
                        link_id='mobilemail3mobilemail4RELATED')
```

Обязательные параметры: 
- `project`
- `case_id`
- `link_id` - id связи. Можно получить через `client.get_testcase_links()`


[Описание используемой ручки](https://testpalm-api.yandex-team.ru/#/Testcase/delete_testcases_link__projectId___testcaseId___linkId_)


##### Удаление связи кейса с тикетом в трекере

```
client.delete_tracker_link(project=Projects.mobilemail, 
                           case_id=1494,
                           st_issue='MOBMAILIOS-468')
```


Обязательные параметры: 
- `project`
- `case_id`
- `st_issue`

Необязательный параметр:
- `tracker_id` - значение по умолчанию - `Startrek`


##### Получение комментариев к кейсу

```
client.get_testcase_comments(project=Projects.mobilemail, 
                             case_id=1)
```

Обязательные параметры: 
- `project`
- `case_id`

[Описание используемой ручки](https://testpalm-api.yandex-team.ru/#/Testcase/get_testcases__projectId___testcaseId__comments)


##### Добавление комментария к кейсу

```
client.add_comment_for_testcase(project=Projects.mobilemail, 
                                case_id=1, 
                                comment='коммент')
```

Обязательные параметры: 
- `project`
- `case_id`
- `comment` - текст комментария

[Описание используемой ручки](https://testpalm-api.yandex-team.ru/#/Testcase/post_testcases__projectId___testcaseId__comments)

##### Удаление комментария к кейсу

```
client.delete_testcase_comment(project=Projects.mobilemail, 
                               comment_id='5e45312081561300267885f6')
```

Обязательные параметры: 
- `project`
- `comment_id` - id комментария. Можно получить через `client.get_testcase_comments()`

[Описание используемой ручки](https://testpalm-api.yandex-team.ru/#/Testcase/delete_testcases__projectId__comments__commentId_)


##### Добавление  аттача к кейсу

```
client.add_testcase_attachment(project=Projects.mobilemail, 
                               case_id=2, 
                               path_to_attachment='1.jpeg')
```

Обязательные параметры: 
- `project`
- `case_id`
- `path_to_attachment` - путь до аттача в файловой системе

[Описание используемой ручки](https://testpalm-api.yandex-team.ru/#/Testcase/post_testcases__projectId___testcaseId__attachment)

##### Получение списка аттачей кейса

```
client.get_testcase_attachments(project=Projects.mobilemail, 
                                case_id=2)
```

Обязательные параметры: 
- `project`
- `case_id`

[Описание используемой ручки](https://testpalm-api.yandex-team.ru/#/Testcase/get_testcases__projectId___testcaseId__attachment__attachmentId_)

##### Скачивание аттача кейса

```
client.save_to_file_testcase_attachment(project=Projects.mobilemail, 
                                        case_id=2, 
                                        attachment_id='5e451f4a81561300267821e3')
```

Обязательные параметры: 
- `project`
- `case_id`
- `attachment_id` - id аттача. Можно получить через `client.get_testcase_attachments()`

Необязательный параметр:
- `path_to_dir` - путь к папке, в которой нужно сохранить файл. По умолчанию это текущая папка

[Описание используемой ручки](https://testpalm-api.yandex-team.ru/#/Testcase/get_testcases__projectId___testcaseId__attachment__attachmentId_)

##### Удаление аттача кейса

```
client.delete_testcase_attachment(project=Projects.mobilemail, 
                                  case_id=2, 
                                  attachment_id='5e451f4a81561300267821e3')
```

Обязательные параметры: 
- `project`
- `case_id`
- `attachment_id` - id аттача. Можно получить через `client.get_testcase_attachments()`

[Описание используемой ручки](https://testpalm-api.yandex-team.ru/#/Testcase/delete_testcases__projectId___testcaseId__attachment__attachmentId_)


#### Сьюты
##### Получение сьютов проекта
```
client.get_testsuites(project=Projects.mobilemail,
                      limit=10,
                      include='title,id,createdBy',
                      expression=str({
                          "type": Operators.eq, 
                          "key": Fields.created_by, 
                          "value": 'fanem'
                      }).replace("'", '"'))
```

Обязательный параметр: 
- `project`

Необязательные параметры: 
- `limit`
- `skip`
- `include`
- `exclude`
- `expression`
- `id`

Параметры `include`, `exclude` не могут использоваться в запросе одновременно.

[Описание используемой ручки](https://testpalm-api.yandex-team.ru/#/Testsuite/get_testsuite__projectId_)


##### Получение конкретного сьюта по id
```
client.get_testsuite(project=Projects.mobilemail,
                     testsuite_id='5d9f9bdcf97f247feef1d53f')
```

Обязательные параметры: 
- `project`
- `testsuite_id`

Необязательные параметры: 
- `include`
- `exclude`

Параметры `include`, `exclude` не могут использоваться в запросе одновременно.

[Описание используемой ручки](https://testpalm-api.yandex-team.ru/#/Testsuite/get_testsuite__projectId___testsuiteId_)


##### Создание сьюта
```
client.create_testsuite(project=Projects.mobilemail,
                        data=data)
```

Обязательные параметры: 
- `project`
- `data`


[Описание используемой ручки](https://testpalm-api.yandex-team.ru/#/Testsuite/post_testsuite__projectId_)


##### Обновление сьюта
```
client.update_testsuite(project=Projects.mobilemail,
                        data=data)
```

Обязательные параметры: 
- `project`
- `data`


[Описание используемой ручки](https://testpalm-api.yandex-team.ru/#/Testsuite/patch_testsuite__projectId_)


##### Обновление сьютов
```
client.update_testsuites(project=Projects.mobilemail,
                         data=data)
```

Обязательные параметры: 
- `project`
- `data`


[Описание используемой ручки](https://testpalm-api.yandex-team.ru/#/Testsuite/patch_testsuite__projectId__bulk)


#### Тестпланы
##### Получение тестпланов проекта
```
client.get_testplans(project=Projects.mobmail_ios)
```

Обязательный параметр: 
- `project`

Необязательные параметры: 
- `include`
- `exclude`

Параметры `include`, `exclude` не могут использоваться в запросе одновременно.

[Описание используемой ручки](https://testpalm-api.yandex-team.ru/#/Testplan/get_testplan__projectId_)

##### Получение конкретного тестплана по id
```
client.get_testplan(project=Projects.mobmail_ios,
                    testplan_id='5a09d11a9793a460f785abe4')
```

Обязательные параметры: 
- `project`
- `testplan_id`

Необязательные параметры: 
- `include`
- `exclude`

Параметры `include`, `exclude` не могут использоваться в запросе одновременно.

[Описание используемой ручки](https://testpalm-api.yandex-team.ru/#/Testplan/get_testplan__projectId___testplanId_)

##### Создание тестплана
```
client.create_testplan(project=Projects.mobmail_ios,
                       data=data)
```

Обязательные параметры: 
- `project`
- `data`


[Описание используемой ручки](https://testpalm-api.yandex-team.ru/#/Testplan/post_testplan__projectId_)

##### Обновление тестплана
```
client.update_testplan(project=Projects.mobmail_ios,
                       data=data)
```

Обязательные параметры: 
- `project`
- `data`


[Описание используемой ручки](https://testpalm-api.yandex-team.ru/#/Testplan/patch_testplan__projectId_)

##### Удаление тестплана
```
client.delete_testplan(project=Projects.mobmail_ios,
                       testplan_id='5a09d11a9793a460f785abe4')
```

Обязательные параметры: 
- `project`
- `testplan_id`

[Описание используемой ручки](https://testpalm-api.yandex-team.ru/#/Testplan/delete_testplan__projectId___testplanId_)


#### Shared steps
##### Получение шаренных степов проекта
```
client.get_shared_steps(project=Projects.mobmail_ios, 
                        include='step,expect,id')
```

Обязательный параметр: 
- `project`

Необязательные параметры: 
- `include`
- `exclude`
- `expression`

Параметры `include`, `exclude` не могут использоваться в запросе одновременно.

Про `expression` подробнее тут https://wiki.yandex-team.ru/testpalm/testpalmdoc/expression-filter/

[Описание используемой ручки](https://testpalm-api.yandex-team.ru/#/Sharedstep/get_step__projectId_)

##### Получение конкретного степа по id
```
client.get_shared_step(project=Projects.mobmail_ios,
                       step_id='58e5f8fd8895504e7941acb6', 
                       include='step,expect,id')
```

Обязательные параметры: 
- `project`
- `step_id`

Необязательные параметры: 
- `include`
- `exclude`
- `expression`

Параметры `include`, `exclude` не могут использоваться в запросе одновременно.

Про `expression` подробнее тут https://wiki.yandex-team.ru/testpalm/testpalmdoc/expression-filter/

[Описание используемой ручки](https://testpalm-api.yandex-team.ru/#/Sharedstep/get_step__projectId_)

##### Обновление шаренного степа
```
client.update_shared_step(project=Projects.mobmail_ios,
                          data=data)
```

Обязательныe параметры: 
- `project`
- `data`

[Описание используемой ручки](https://testpalm-api.yandex-team.ru/#/Sharedstep/patch_step__projectId_)

##### Удаление шаренного степа
```
client.delete_shared_step(project=Projects.mobmail_ios, 
                          step_id='5e4abc1db8ee9900275d1e51')
```

Обязательныe параметры: 
- `project`
- `step_id`

[Описание используемой ручки](https://testpalm-api.yandex-team.ru/#/Sharedstep/delete_step__projectId___stepId_)


#### Organization
##### Получение организации по id
```
client.get_organization(organization_id='id')
```

Обязательные параметры: 
- `organization_id`

Необязательные параметры: 
- `include`
- `exclude`

Параметры `include`, `exclude` не могут использоваться в запросе одновременно.

[Описание используемой ручки](https://testpalm-api.yandex-team.ru/#/Organization/get_organizations__organizationId_)


##### Создание организации
```
client.create_organization(data={
                                    'id': 'mobmail',
                                    'title': 'Mobile mail',
                                    'permittedGroups': [
                                        {
                                            'name': 'Мобильная Почта', 
                                            'id': '228'
                                        }
                                    ]
                                 }))
```

Обязательные параметры: 
- `data`

[Описание используемой ручки](https://testpalm-api.yandex-team.ru/#/Organization/post_organizations)

##### Обновление организации
```
client.update_organization(organization_id='id',
                           data=data)
```

Обязательные параметры: 
- `organization_id`
- `data`

[Описание используемой ручки](https://testpalm-api.yandex-team.ru/#/Organization/patch_organizations__organizationId_)


#### Automation group
##### Получение Automation group по id
```
client.get_automation_group(project=Projects.mobmail_ios, 
                            automation_id='id')
```

Обязательные параметры: 
- `project`
- `automation_id`

[Описание используемой ручки](https://testpalm-api.yandex-team.ru/#/AutomationGroup/get_automationgroup__projectId___id_)


##### Создание Automation group
```
client.create_automation_group(project=Projects.mobmail_ios, 
                               data=data)
```

Обязательные параметры: 
- `project`
- `automation_id`

[Описание используемой ручки](https://testpalm-api.yandex-team.ru/#/AutomationGroup/post_automationgroup__projectId_)


#### Order

```
client.set_order(project=Projects.mobmail_ios, 
                 testcase_ids=123)
```

Обязательные параметры: 
- `project`
- `testcase_ids`

[Описание используемой ручки](https://testpalm-api.yandex-team.ru/#/Order/post_order__projectId_)


#### Audit
```
client.get_definition_audit(project=Projects.mobmail_ios)
```

Обязательные параметры: 
- `project`

Необязательные параметры: 
- `include`
- `exclude`

Параметры `include`, `exclude` не могут использоваться в запросе одновременно.

[Описание используемой ручки](https://testpalm-api.yandex-team.ru/#/Audit/get_audit__projectId__definition)

#### Runner
```
client.get_runner_config_format(project=Projects.mobmail_ios)
```

Необязательные параметры: 
- `include`
- `exclude`

Параметры `include`, `exclude` не могут использоваться в запросе одновременно.

[Описание используемой ручки](https://testpalm-api.yandex-team.ru/#/Runner/get_runner_all)
