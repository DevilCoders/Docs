# Разметка и оформление тикетов

Тикет, независимо от своего типа (баг, задача, улучшение), должен быть правильно оформлен и понятен для всех коллег

Ниже указан пример оформления багов, однако, для заведения улучшений и обычных тасок можно руководствоваться данным правилами

## Основные правила разметки

1. если **баг продовый**, сразу расставлять теги приоритизации
2. если **баг был найден в рамках тестирования проекта/фичи**, но решили выкатиться с ним в прод - необходимо переделать разметку (поменять теги, добавить приоритизацию, сменить стадию)
3. если у бага **сменилась область с фронта на бэк (и наоборот)** - сразу актуализировать это измение в разметке
4. **следить за весом бага** и актуализировать его при необходимости


## Оформление багов на бэкенд


[Пример тикета на бэкенд](https://st.yandex-team.ru/CHEMODAN-81227)


|           Поле           | Описание                                                                                                                                              |
|:------------------------:|:------------------------------------------------------------------------------------------------------------------------------------------------------|
|          Тайтл           | Наименование тикета должно быть коротким и отражать суть проблемы                                                                                     |
|         Описание         | В описании максимально подробно описываем проблему. Обязательно прикладываем `uid`, `org_id`, `время`, `окружение` и любую другую полезную информацию |
| Последовательность шагов | Указываем последовательность шагов, которая привела к проблеме                                                                                        |
|   Ожидаемый результат    | Указываем правильное поведение, которое ожидалось получить                                                                                            |
|         Компоненты         | Указываем компонент `Disk Backend`                         |
| Метод обнаружения дефектов | Указываем правильный тип - кто обнаружил баг?              |
|           Стадия           | Указываем окружение - где найдена проблема?                |

В тикет можно также допольнительно призывать дежурного, если баг на проде или ответственного разработчика за фичу, если баг найден в рамках тестирования проекта/фичи


### Оформление багов на фронтенд

[Пример тикета на фронтенд](https://st.yandex-team.ru/CHEMODAN-81156)


|           Поле           | Описание                                                                                                                                                   |
|:------------------------:|:-----------------------------------------------------------------------------------------------------------------------------------------------------------|
|          Тайтл           | Наименование тикета должно быть коротким и отражать суть проблемы                                                                                          |
|         Описание         | В описании максимально подробно описываем проблему                                                                                                         |
| Последовательность шагов | Указываем последовательность шагов, которая привела к проблеме                                                                                             |
|   Ожидаемый результат    | Указываем правильное поведение, которое ожидалось получить                                                                                                 |
|  Фактический результат   | Указываем поведение, которое возникло при выполнении указанной последовательности шагов                                                                    |
|    Ключевые артефакты    | Прикладываем любую полезную к анализу информацию: видео, скриншоты, ошибки консоли, запросы и тд                                                           |
|      Компоненты       | Указываем компонент `Disk Backend` + компонент приложения, в котором проблема                      |
|         Теги          | Указываем `inProd`, если проблема на проде + не забываем про теги приоритизации (только если прод) |
|        Стадия         | Указываем окружение - где найдена проблема?                                                        |                                                                                                                             |



### Клонирование асессорских тикетов в очередь CHEMODAN

Отдельно стоит отметить, что асессорские тикеты стоит приводить к человекочитаемому виду при клонировании в нашу очередь

Это стоит делать потому, что тикеты в нашей очереди часть информации из тикета уже теряет свою актуальность (например, логин асессора или его окружение)

**При клонировании тикета обязательно форматируем его по описанным выше правилам**
