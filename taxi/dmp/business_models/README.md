# business_models
## Установка библиотеки
`python2.7 -m pip install --user -i https://pypi.yandex-team.ru/simple business_models --upgrade`</br>
`python3.7 -m pip install --user -i https://pypi.yandex-team.ru/simple business_models --upgrade`</br>
Если устанавливаете впервые, то в конце уберите `--upgrade`

Для корректной работы библиотеки с модулями `hahn` и `greenplum`, нужно в корневую папку добавить файл `mylib_config.json` вида:</br>
`{"yt_token": "AQAD-***",
"gp_token": "AQAD-***"}`</br>
Cоздать такой файл можно командой:</br>
`echo '{"yt_token": "AQAD-***", "gp_token": "AQAD-***"}' > ~/mylib_config.json; chmod 700 ~/mylib_config.json`

## О чем это?
Сюда попадают всякие вещи, упрощающие работу аналитика: от простых в духе "сходить в YT, не думая о токенах", и до "собрать большую и сложную модель прогнозирования".

Если у вас появится желание что-то самостоятельно дописать в библиотеку, то присылайте пулреквесты, мы будем очень рады! Если мы долго не смотрим, то можно написать, например, мне (rotax@yandex-team.ru или в телеграм - ksuabr). Всех внесших вклад в развитие библиотеки ждет [ачивка](https://staff.yandex-team.ru/achievements/achievement/1756)!

Также у нас есть [FAQ](https://wiki.yandex-team.ru/taxi/analytics/businessmodeling/#faqchastyeproblemyiixreshenie), [чат поддержки](https://t.me/joinchat/D71WeBGgGHfvWFEvLEadhQ) и можно ставить на нас [тикеты](https://nda.ya.ru/t/3cSTj87D3Vw54w), чтобы появились какие-то улучшения или исправились баги. Подробнее про команду и то, что мы делаем, можно почитать [wiki](https://wiki.yandex-team.ru/taxi/analytics/businessmodeling/).

## Основные примеры использования библиотеки
Все примеры собираются в папке <a href="https://github.yandex-team.ru/rotax/business_models/tree/master/common_scripts">common_scripts</a>. Если у вас есть какой-то полезный пример, то можете его добавлять.

`Все примеры имеют свойство устаревать. Так как обратная совместимость не всегда гарантируется, при возникновении ошибок во время исполнения кода изучайте документацию (через ?, help или функцию describe, например)`
  - [Основной пример работы с библиотекой](https://a.yandex-team.ru/projects/business_models/code/taxi/dmp/business_models/common_scripts/Overview%20business_models.ipynb?dir=taxi%2Fdmp%2Fbusiness_models)
  - <a href="https://a.yandex-team.ru/projects/business_models/code/taxi/dmp/business_models/common_scripts/Models%20main%20example.ipynb?dir=taxi%2Fdmp%2Fbusiness_models">Основной пример работы с моделями</a>
  - <a href="https://a.yandex-team.ru/projects/business_models/code/taxi/dmp/business_models/common_scripts/Greenplum.ipynb?dir=taxi%2Fdmp%2Fbusiness_models">Модуль greenplum</a>
  - <a href="https://a.yandex-team.ru/projects/business_models/code/taxi/dmp/business_models/common_scripts/Hahn.ipynb?dir=taxi%2Fdmp%2Fbusiness_models">Модуль hahn</a>
  - [Бэкапы в hahn](https://a.yandex-team.ru/projects/business_models/code/taxi/dmp/business_models/common_scripts/Hahn%20backups.ipynb?dir=taxi%2Fdmp%2Fbusiness_models)
  - [Работа с гуглдоками (модуль gdocs)](https://a.yandex-team.ru/projects/business_models/code/taxi/dmp/business_models/common_scripts/Google%20Sheets.ipynb?dir=taxi%2Fdmp%2Fbusiness_models)
  - [Работа со стартреком (модуль startrek)](https://a.yandex-team.ru/projects/business_models/code/taxi/dmp/business_models/common_scripts/Startrek%20example.ipynb?dir=taxi%2Fdmp%2Fbusiness_models)
  - [Telegram-боты](https://a.yandex-team.ru/projects/business_models/code/taxi/dmp/business_models/common_scripts/Telegram%20bots.ipynb?dir=taxi%2Fdmp%2Fbusiness_models)
  - [Использование класса Handler для ловли ошибок и нотификации](https://a.yandex-team.ru/projects/business_models/code/taxi/dmp/business_models/common_scripts/Handler.ipynb?dir=taxi%2Fdmp%2Fbusiness_models)
  - <a href="https://a.yandex-team.ru/projects/business_models/code/taxi/dmp/business_models/common_scripts/CoverterExample.ipynb?dir=taxi%2Fdmp%2Fbusiness_models">Конвертация данных: между скейлами и регионами</a>
  - <a href="https://a.yandex-team.ru/projects/business_models/code/taxi/dmp/business_models/common_scripts/Cohorts.ipynb?dir=taxi%2Fdmp%2Fbusiness_models">Расчет когорт, простых и сложных</a>
  - [Работа с Clickhouse](https://a.yandex-team.ru/projects/business_models/code/taxi/dmp/business_models/common_scripts/Clickhouse.ipynb?dir=taxi%2Fdmp%2Fbusiness_models)
  - [Работа с сервисами интранета (IDM, Wiki и т.п.)](https://a.yandex-team.ru/projects/business_models/code/taxi/dmp/business_models/common_scripts/Intranet.ipynb?dir=taxi%2Fdmp%2Fbusiness_models)
  - [Работа с токенами через ConfigHolder](https://a.yandex-team.ru/projects/business_models/code/taxi/dmp/business_models/common_scripts/Manage%20tokens%20ConfigHolder.ipynb?dir=taxi%2Fdmp%2Fbusiness_models)
  - [Пример использования модели баланса](https://a.yandex-team.ru/projects/business_models/code/taxi/dmp/business_models/common_scripts/Elasticity%20Using%20Sample.ipynb?dir=taxi%2Fdmp%2Fbusiness_models)
  - [Поиск похожих городов](https://a.yandex-team.ru/projects/business_models/code/taxi/dmp/business_models/common_scripts/Similar%20regions%20searching.ipynb?dir=taxi%2Fdmp%2Fbusiness_models)

## Структура репозитория
Библиотека разбита на логические части:
  - `accuracy` - функции для скоринга абстрактных моделей (сравнение реальных и расчитанных данных)
  - `cohorts` - класс для работы с плоскими когортами (построить ретеншен, ltv, когортную матрицу и проч.)
  - `common_scripts` - для обмена скриптами, использующими модуль (там же всякие полезные примеры использования)
  - `cron` - скрипты, регулярно исполняемые роботом **robot-taxi-models**
  - `models` - модели бизнеса
  - `planning` - инструмент планирования бюджета
  - `plot` - отрисовка графиков по абстрактным входным данным
  - `queries` - расчет и чтение данных (YT)
  - `tests` - тесты для функций и классов во всей библиотеке (всегда будем рады, если вы напишете парочку)
  - `train` - обучалка модели (вход - любая модель, данные; выход - обученная модель)

## Development
[Доска](https://st.yandex-team.ru/dashboard/27035) в стартреке с бэклогом задач.

Тикеты с багами и пожеланиями можно создавать через шаблоны:
 - [основной шаблон для багов](https://st.yandex-team.ru/settings/templates/issues?name=Баги%20и%20хотелки%20в%20business_models&owner=1120000000066976&queue=TAXIANALYTICS)
 - [шаблон про библиотеку](https://st.yandex-team.ru/settings/templates/issues?name=Библиотека%20business_models&owner=1120000000066976&queue=TAXIANALYTICS)
 - [шаблон про code, без лишних наблюдателей](https://st.yandex-team.ru/settings/templates/issues?name=DEV%20business_models&owner=1120000000066976&queue=TAXIANALYTICS)

## Релизы
Библиотеку можно установить через pip с помощью команды:
`pip2 install --user -i https://pypi.yandex-team.ru/simple business_models`

**Список версий (от последней к первой)**
Все описания спрятаны под кат. В коде репозитория указана последняя существующая версия, но она по содержанию может отличаться от описания. Все изменения будут вноситься в следующую версию.

<details>
<summary><u>Версия 2.1.3.4</u></summary>
    <ul>
    <li>[config_holder] В ConfigHolder пофикшена проблема с бесконечной рекурсией при поиске секретов в секретнице</li>
    </ul>
</details>
</br>


<details>
<summary><u>Версия 2.1.3.3</u></summary>
    <ul>
    <li>Datalens: добавили ретраи запросов к API и sleep между несколькими запросами подряд</li>
    <li>Datalens: ошибка на одном из скриншотов не будет влиять на остальные</li>
    </ul>
</details>
</br>


<details>
<summary><u>Версия 2.1.3.2</u></summary>
    <ul>
    <li>[config_holder] В ConfigHolder пофикшена проблема с бесконечной рекурсией при передаче yav_secret_ids</li>
    </ul>
</details>
</br>


<details>
<summary><u>Версия 2.1.3.1</u></summary>
    <ul>
    <li>[datalens] фикс бага со скриншотами графиков с множественным выбором в параметрах </li>
    <li> [plot] фикс бага с отрисовкой персентиля в plot_dataframe_hist </li>
    </ul>
</details>
</br>


<details>
<summary><u>Версия 2.1.3</u></summary>
    <ul>
    <li>[intranet] появился модуль datalens для сохранения скриншотов графиков из DataLens в файлы. Есть интеграция
    с отправкой этих файлов в телеграм.</li>
    </ul>
</details>
</br>


<details>
<summary><u>Версия 2.1.2</u></summary>
    <ul>
    <li>Появился модуль с трансформациями данных и первая трансформация period_snapshot для GP</li>
    <li>Заменили подключение к GP на gpdb-master.taxi.yandex.net</li>
    <li>Убрали зависимость от yson-bindings</li>
    <li>[ConfigHolder] Теперь будет создаваться дефолтный объект bm_config, на котором будут сидеть все дефолтные объекты (hahn, greenplum и т.п.)</li>
    <li>[ConfigHolder] У конфиг холдера можно сменить путь до конфигов. При этом токен для секретницы уже будет прочитан и не будет меняться. Это приводит к тому, что все токены теперь берутся только из публичного конфига</li>
    <li>[botolib] Убрала костыльные использования юникода</li>
    <li>[basic] В data_from_file вместо костылей теперь используется os.path для определения расширения файла</li>
    <li>[databases] HahnDataLoader не падает на yql-запросах, если до этого был использован chyt</li>
    </ul>
</details>
</br>


<details>
<summary><u>Версия 2.1.1.2</u></summary>
    <ul>
    <li>[<b>databases</b>] <b>Greenplum.dump</b> снова работает (до этого коннект слишком рано протухал)</li>
<li>[<b>log</b>] В <b>Handler</b> можно передать чат, в который уходят нотификации бота: <b>bot_chat</b></li>
    </ul>
</details>
</br>


<details>
<summary><u>Версия 2.1.1.1</u></summary>
    <ul>
    <li>[<b>ConfigHolder</b>] Отсутствующие <b>dwh_settings</b> не роняют поиск токенов</li>
    </ul>
</details>
</br>


<details>
<summary><u>Версия 2.1.1</u></summary>
    <ul>
    <li>[<b>ConfigHolder</b>] Хотфикс: <b>ConfigHolder</b> не будет падать при поиске токенов в отсутсвующих файлах</li>
    </ul>
</details>
</br>


<details>
<summary><u>Версия 2.1</u></summary>
    <ul>
    <li>[<b>config_holder</b>] Теперь секреты можно хранить целиком в секретнице, а на машинке оставить только токен от секретницы и ссылку на основной секрет + в целом случился небольшой рефакторинг <b>ConfigHolder</b></li>
<li>[<b>util</b>] <b>data_from_file</b> умеет читать <b>yaml</b>'ики</li>
<li>[<b>databases</b>] В <b>HahnDataLoader</b> можно передать конкретную клику для <b>CHYT</b> через параметр <b>chyt_clique</b></li>
<li>[<b>databases</b>] Перестали поддерживать аргумент <b>syntax_version</b> в <b>HahnDataLoader</b></li>
<li>[<b>gdocs</b>] Добавлена возможность авторизации через сервисный аккаунт: параметр <b>service_account_json_key_path</b></li>
<li>[<b>greenplum</b>] Теперь соеднение будет создаваться перед каждой попыткой использования соединения и закрываться сразу после использования</li>
    </ul>
</details>
</br>


<details>
<summary><u>Версия 2.0.66.1</u></summary>
    <ul>
    <li>[<b>databases</b>] В <b>hahn</b> справлен баг c передачей <b>database</b> при использовании <b>CHYT</b></li>
    </ul>
</details>
</br>


<details>
<summary><u>Версия 2.0.66</u></summary>
    <ul>
    <li>[<b>gdocs</b>] поддержка кастомного объекта <b>httplib</b>2<b>.Http</b> в <b>GoogleDocs</b></li>
    </ul>
</details>
</br>


<details>
<summary><u>Версия 2.0.65</u></summary>
    <ul>
    <li>[<b>greenplum</b>] Проверка наличия авторизации в GP будет происходить через запрос <b>select</b> 1</li>
<li>[<b>databases</b>] В <b>hahn</b> теперь можно делать запросы через <b>CHYT</b></li>
<li>[<b>optimize</b>] В модуль добавлена совместимость с 3 питоном</li>
    </ul>
</details>
</br>


<details>
<summary><u>Версия 2.0.64</u></summary>
    <ul>
    <li>[<b>greenplum</b>] Убрали <b>ensure_authorized</b> (после падения запрос не будет пытаться перевыполниться без переавторизации)</li>
<li>[<b>greenplum</b>] Поправили порядок декораторов, теперь при ретрае выполнения запроса будет переподключение к GP</li>
    </ul>
</details>
</br>


<details>
<summary><u>Версия 2.0.63.2</u></summary>
    <ul>
    <li>[<b>util.dataframes</b>]  <b>fill_missing_cohorts</b> теперь всегда оставляет последней точкой максимум из последней когорты и последней даты, чтобы заполнять когорты, выпавшие на текущей неделе</li>
    </ul>
</details>
</br>


<details>
<summary><u>Версия 2.0.63.1</u></summary>
    <ul>
    <li>[<b>queries</b>] Из иерархии убран США</li>
<li>[<b>queries</b>] Добавлен Берген в города, которые мы не проверяем</li>
    </ul>
</details>
</br>


<details>
<summary><u>Версия 2.0.63</u></summary>
    <ul>
    <li>[<b>queries</b>] Добавлены запросы на чтение данных для прогнозов для валидации запуска перед началом расчетов</li>
<li>[<b>queries</b>] Исправлены баги в поиске таблиц из конфига: теперь учитывается <b>database</b> и наличие алиасов названий таблиц</li>
<li>[<b>queries</b>] Добавлен запрос для реплицирования таблиц с GP  в тестах</li>
    </ul>
</details>
</br>


<details>
<summary><u>Версия 2.0.62.2</u></summary>
    <ul>
    <li>[<b>databases</b>] Переход на запись датафреймов в <b>greenplum</b> через функцию <b>psql_insert_copy</b></li>
    </ul>
</details>
</br>


<details>
<summary><u>Версия 2.0.62.1</u></summary>
    <ul>
    <li>[<b>databases</b>] Поправили баг, создающий доп. коннекшн для <b>greenplum</b></li>
    </ul>
</details>
</br>


<details>
<summary><u>Версия 2.0.62</u></summary>
    <ul>
    <li> [<b>greenplum</b>] Оптимизировано количество создаваемых коннектов к GP
    </ul>
</details>
</br>


<details>
<summary><u>Версия 2.0.61.1</u></summary>
    <ul>
    <li>[<b>util.dataframe</b>] Функция <b>fill_missing_dates</b> теперь умеет дополнять не только квадратные когортные данные
    </ul>
</details>
</br>


<details>
<summary><u>Версия 2.0.61</u></summary>
    <ul>
<li>[<b>queries</b>] В <b>reader</b> изменен метод <b>read_dwh_object</b>: фильтрация по скейлу просиходит автоматически при выставлении флага, добавилась возможность передавать кастомные название колонок с временем и географией</li>
<li>[<b>convert</b>] <b>HierarchyConverter</b> теперь подставляет 0 для всех регионов, которые не нашлись в пропорциях</li>
<li>[<b>util.dates</b>] Добавился <b>SCALE_NAMES</b> - словарик с переводом названий скейлов</li>
    </ul>
</details>
</br>


<details>
<summary><u>Версия 2.0.60.5</u></summary>
    <ul>
    <li>[<b>intranet</b>] Исправлен баг с <b>format</b> в <b>idm</b></li>
    <li>[<b>queries</b>] В <b>reader</b> добавлен метод read_dwh_object для чтения когорт и часовых точек от ДВХ</li>
    </ul>
</details>
</br>


<details>
<summary><u>Версия 2.0.60.4</u></summary>
    <ul>
    <li>[<b>intranet</b>] Из кода удалены f-строки для совместимости со вторым питоном</li>
    </ul>
</details>
</br>


<details>
<summary><u>Версия 2.0.60.3</u></summary>
    <ul>

    </ul>
</details>
</br>


<details>
<summary><u>Версия 2.0.60.2</u></summary>
    <ul>

    </ul>
</details>
</br>


<details>
<summary><u>Версия 2.0.60.1</u></summary>
    <ul>
    <li>[<b>config_holder</b>] Изолированы импорты в <b>valuit_client</b></li>
    <li>В зависимости библиотеки добавлены <b>yandex-passport-vault-client</b> и <b>pathlib</b></li>
    </ul>
</details>
</br>


<details>
<summary><u>Версия 2.0.60</u></summary>
    <ul>
    <li>[<b>config_holder</b>] Добавлена поддержка токенов из секретницы</li>
<li>[<b>gdocs</b>] исправлен способ создания файла с токеном, теперь он будет работать и для <b>MacOS</b></li>
<li>[<b>queries</b>] В <b>reader</b> появился метод <b>read_dwh_object</b> для чтения когорт и часовых точек от ДВХ</li>
<li>[<b>intranet</b>] В <b>IDM</b> добавлены методы: клонирования ролей, вывод разницы в активных (выданных) ролях, вывод узлов без ролей</li>
    </ul>
</details>
</br>


</br>
<details>
<summary>Более старые версии</summary>
<details>
<summary><u>Версия 2.0.59</u></summary>
    <ul>
    <li>[<b>greenplum</b>] добавила ретраи при подключении к <b>GP.</b> Должно помочь уменьшить число падений из-за ограничения числа коннектов</li>
    </ul>
</details>
</br>


<details>
<summary><u>Версия 2.0.58</u></summary>
    <ul>
<li>[<b>greenplum</b>] Функция <b>drop_or_truncate_table</b> теперь может возвращать текст запроса. А также внутрь создания функции для обновления таблицы добавлен логин запускающего пользователя</li>
    </ul>
</details>
</br>


<details>
<summary><u>Версия 2.0.57.1</u></summary>
    <ul>
<li>[<b>gdocs</b>] В <b>run_by_update</b> можно указывать поведение, после возникновения ошибки (нужно пробовать снова запустить метод или нет)</li>
    </ul>
</details>
</br>


<details>
<summary><u>Версия 2.0.57</u></summary>
    <ul>
    <li>[<b>hahn</b>] Заменил <b>pandas.datetime</b> на <b>datetime</b>, чтобы избавиться от <b>FutureWarning</b></li>
    <li>[<b>util.log</b>]  <b>Handler</b> обзавелся атрибутом  <b>sent_message</b>, куда он сохраняет итоговую ошибку, которую логирует
    </ul>
</details>
</br>


<details>
<summary><u>Версия 2.0.56</u></summary>
    <ul>
    <li>[<b>queries</b>] МО и ЛО объединены для расчета данных в прогнозе</li>
    </ul>
</details>
</br>


<details>
<summary><u>Версия 2.0.55</u></summary>
    <ul>
    <li>[<b>databases</b>] В <b>hahn.write</b> можно передать в <b>types</b> только часть колонок, с которыми возникают проблемы, а не все-все</li>
<li>[<b>databases</b>] В <b>hahn</b> заменили провайдер <b>yt_native</b> на yt</li>
    </ul>
</details>
</br>


<details>
<summary><u>Версия 2.0.54</u></summary>
    <ul>
    <li>[<b>intranet</b>] Поправлены потенциальные баги на 2 питоне</li>
<li>[<b>gdocs</b>] в гуглдоках появилась возможность создавать новые <b>spreadsheets</b> и выдавать на них доступы</li>
    </ul>
</details>
</br>


<details>
<summary><u>Версия 2.0.53</u></summary>
    <ul>
    <li>[<b>plot</b>] Цвет <b>None</b> больше никогда не будет передаваться в отрисовку</li>
<li>[<b>greenplum</b>] в <b>dump</b> явно разделены дополнительные аргументы для <b>pandas</b> и <b>hahn.</b> Теперь можно поменять <b>date_conversion_mask</b>, например</li>
<li>[<b>intranet</b>] <b>StartrekWrapper</b> вынесен в отдельный модуль</li>
<li>[<b>convert</b>] В <b>HierarchyConverter</b> исправлен баг, при котором в итоговых данных оставались кастомные регионы из неконвертированных данных</li>
<li>[<b>models</b>] починили работу с <b>date_to</b> и <b>last_fact_date</b> для случая нескольких вызовов <b>fit</b> у модели</li>
<li>[<b>databases</b>] В <b>greenplum</b> появился метод, который создает таблицу в случае ее отсутствия и инсертит в нее, если та существует</li>
<li>[<b>intranet</b>] добавлены классы для взаимодействия с <b>Wiki</b>, <b>IDM</b>, <b>ABC</b> и поиском по интранету</li>
    </ul>
</details>
</br>


<details>
<summary><u>Версия 2.0.52</u></summary>
    <ul>
    <li>[<b>queries</b>] избавились от <b>user_phone</b></li>
    </ul>
</details>
</br>


<details>
<summary><u>Версия 2.0.51.3</u></summary>
    <ul>
    <li>[<b>util</b>] Исправлен баг, из-за которого <b>data_from_file</b> запоминал навсегда все аргументы чтения (например, <b>sheet_name</b> при чтении гуглдоков)</li>
<li>[<b>models.retention</b>] Изменена обработка <b>nan</b> в <b>multiple_retention</b></li>
    </ul>
</details>
</br>


<details>
<summary><u>Версия 2.0.51.2</u></summary>
    <ul>
    <li>[<b>queries.views</b>] Созданы запросы с <b>view</b> для отчетов по моделям и скорингу</li>
<li>[<b>graph.configuration</b>]  Значения в словарях из <b>predicted_values</b> могут сами быть словарями с переданным внутри порядком запуска</li>
<li>[<b>cron.forecast</b>] Появился метод, который пересчитывает <b>supply_change</b> в историю с разными <b>date_to</b></li>
    </ul>
</details>
</br>


<details>
<summary><u>Версия 2.0.51.1</u></summary>
    <ul>
    <li>[<b>greenplum</b>] При заливке с <b>columns_order</b>='<b>auto</b>' маскировалась ошибка, когда пытаются залить данные с доп колонкой. Теперь будет явное исключение</li>
<li>[<b>models.cluster_model</b>] Исправлена ошибка c <b>value_name</b> в <b>verbose_test</b></li>
<li>[<b>plot</b>] Отрисовка гистограм через <b>plot_object</b> не будет падать в 3 питоне</li>
<li>[<b>models.retention.multiple_retention</b>] Исправлена работа с прямоугольными матрицами</li>
    </ul>
</details>
</br>


<details>
<summary><u>Версия 2.0.51</u></summary>
    <ul>
    <li>[<b>greenplum</b>] При заливке с <b>columns_order</b>='<b>auto</b>' маскировалась ошибка, когда пытаются залить данные с доп колонкой. Теперь будет явное исключение</li>
    <li>[<b>queries</b>] Исправлена ошибка в подсчете деманд сессий</li>
    </ul>
</details>
</br>


<details>
<summary><u>Версия 2.0.50</u></summary>
    <ul>
    <li>[<b>tests.graph_score_tests</b>] Тест скоринга больше не будет слать сообщение через бота</li>
<li>[<b>queries.runner</b>] <b>write_table_by_path</b> теперь может не падать, если ему передали <b>sub_path</b></li>
<li>[<b>models.model_attributes</b>] Исправлены баги в <b>VerboseParameters</b></li>
<li>[<b>models.retention.multiple_retention</b>] Скорректирована обработка прямоугольных матриц</li>
<li>[<b>graph.configurator</b>] Появился метод <b>write_tables</b>, который заливает <b>VerboseParameters</b> моделей</li>
    </ul>
</details>
</br>


<details>
<summary><u>Версия 2.0.49</u></summary>
    <ul>
<li>[<b>databases.database_sql</b>] Больше не будет возникать ошибка с <b>autocommit</b> при записи на greenplum</li>
<li>[<b>all</b>] Небольшие города из зарубежки добавлены объединены в группы в <b>custom_regions</b></li>
    </ul>
</details>
</br>


<details>
<summary><u>Версия 2.0.48.3</u></summary>
    <ul>
<li>[<b>models.retention</b>] Исправлен баг с хардкодом в <b>ndots_predict</b> в <b>MultipleRetention</b></li>
    </ul>
</details>
</br>


<details>
<summary><u>Версия 2.0.48.2 (содержит баги)</u></summary>
    <ul>
<li>[<b>models.retention</b>] Исправлена проблема с <b>MultipleRetention</b>, из-за которой модели работали гораздо дольше</li>
    </ul>
</details>
</br>


<details>
<summary><u>Версия 2.0.48.1</u></summary>
    <ul>
<li>[<b>queries.reader</b>] Появился метод _add_relative_date_filter, позволяющий добавлять фильтры по дате</li>
<li>[<b>models.model</b>] Появился метод <b>_plot_or_save</b>, который либо рисует графики для моделей, либо возвращает данные для их отрисовки. Все методы отрисовки моделей вызывают внутри себя именно <b>_plot_or_save</b></li>
<li>[<b>models</b>] Переписаны методы отрисовки моделей для совместимости с <b>plot_or_save</b></li>
<li>[<b>plot</b>] <b>plot_forecast</b> теперь умеет рисовать факт и прогноз единым графиком, сохраняя прямую, разделяющую их. Для этого нужно использовать аргумент <b>same_series</b></li>
<li>[<b>models.retention</b>] в <b>MultipleRetention</b> исправлен баг с бесконечностями в прогнозе</li>
    </ul>
</details>
</br>


<details>
<summary><u>Версия 2.0.48</u></summary>
    <ul>
    <li>[<b>databases.hahn</b>] В <b>hahn.read</b> можно передавать аргументы для <b>yt.read_table</b> с помощью аргумента <b>yt_kwargs</b></li>
<li>[<b>databases.database_sql</b>] Появился метод <b>backup</b>, который бэкапит таблицы из переданных путей</li>
<li>[<b>queries.reader</b>] Добавлен <b>date_to</b> в <b>read_parameter</b>, чтобы можно было отсчитывать <b>periods_from_today</b> от произвольной даты, а не от сегодняшнего дня</li>
<li>[<b>graph</b> ]Граф и дата менеджер обучены работе с <b>date_to</b> на чтении</li>
<li>[<b>graph.configurator</b>] в <b>score</b> можно передавать <b>select_nodes</b></li>
<li>[<b>models</b>] появился отдельный класс <b>VerboseParameters</b>, который ведет себя как словарь, но умеет записывать данные на диск и читать их оттуда при необходимости</li>
<li>[<b>graph.configurator</b>] Метод <b>score</b> теперь в явном виде читает сначала данные из факта, а потом из получившегося прогноза с <b>date_to</b></li>
<li>[<b>models.retention</b>] <b>MultipleRetention</b> научился работать с прямоугольными когортными матрицами</li>
<li>[<b>models.retention</b>] <b>Retention</b> получил методы, которые позволяют создавать когортные матрицы из плоских данных, разворачивать матрицы в плоские данные и менять тип когортной матрицы</li>
    </ul>
</details>
</br>


<details>
<summary><u>Версия 2.0.47.1</u></summary>
    <ul>
    <li>[<b>queries</b>] Исправлен баг в recount_metrics, появившийся при переходе на phone_pd_id</li>>
    </ul>
</details>
</br>


<details>
<summary><u>Версия 2.0.47</u></summary>
    <ul>
    <li>[<b>converter</b>] <b>HierarchyConverter.convert</b> распилен на более короткие логические куски + появилась возможность пропустить шаг с разбивкой на агломерации (<b>only_squeeze</b>=<b>True</b>)</li>
<li>[<b>queries</b>] У <b>runner</b> появился метод <b>restore_failed_planning</b>, позволяющий восстанавливать упавший на валидации прогноз</li>
<li>[<b>util.dates</b>] Исправлен баг в <b>shift_date</b> с неправильной обработкой часов при <b>scale</b>='<b>month</b></li>
<li>[<b>queries</b>] В <b>metrics</b> и <b>cohorts</b> идентификатор уникального пользователя сменился с <b>user_phone</b> на <b>pd_id</b></li>
<li>[<b>databases</b>] Исправлено отображением ошибки о создании объектов из <b>gptransfer_client</b></li>
    </ul>
</details>
</br>


<details>
<summary><u>Версия 2.0.46.2</u></summary>
    <ul>
    <li>[<b>graph.configurator</b>] В <b>score</b> <b>create_scale_with_reload</b> и <b>skip_top_level_source</b> вернулись в дефолтные значения</li>
<li>[<b>models.seasonality</b>] В <b>get_one_dim_season</b> у <b>rotation_seasonality</b> теперь можно передать <b>index.</b> Тогда внутри данные сгруппируются до <b>index</b>+<b>scale.</b> Это позволяет корректно работать с когортными данными</li>
<li>[<b>tests.graph_forecasts_tests</b>] В <b>make_forecasts_tests</b> можно передать <b>select_nodes</b></li>
    </ul>
</details>
</br>


<details>
<summary><u>Версия 2.0.46.1</u></summary>
    <ul>
    <li>[<b>databases.gdocs</b>] Появился метод <b>run_by_update</b>, который сделать так, чтобы функция запускалась по значению ячейки в <b>Googledoc</b></li>
<li>[<b>queries.queries_config</b>] Добавлена <b>fi_lithuania</b> как кастомная нода географии</li>
<li>[<b>database</b>] можно выгружать топ N строк из таблицы для любой <b>Database</b>, у которой определен <b>call</b></li>
    </ul>
</details>
</br>


<details>
<summary><u>Версия 2.0.46</u></summary>
    <ul>
    <li>[<b>optimize</b>] класс <b>DimensionGrouper</b> для поиска похожих городов + пример использования</li>
<li>[<b>models.anomaly.normaliaztion</b>] Исправлен баг с неверным определением начальной даты в режиме <b>use_normed</b></li>
<li>[<b>graph</b>] <b>Configurator.graph_logger</b> перестал всегда быть <b>None</b>'ом</li>
    </ul>
</details>
</br>


<details>
<summary><u>Версия 2.0.45.2</u></summary>
    <ul>
    <li>[<b>queries.reader</b>] Исправлен баг с путем для иерархии</li>
    </ul>
</details>
</br>


<details>
<summary><u>Версия 2.0.45.1</u></summary>
    <ul>
    <li>[<b>graph</b>] Переделана работа с логами в графе. Теперь директории для логов будут создаваться непосредственно перед использованием + действительно можно сменить путь для логов после создания объекта</li>
<li>[<b>util</b>] объект <b>EmptyWithStatement</b>, который игнорирует <b>with</b></li>
<li>[<b>graph</b>] у <b>DataManager</b> теперь можно отрывать <b>lock</b> без последствий для работы (только если вы не в параллельном режиме запускаетесь, конечно)</li>
<li>[<b>queries.reader</b>] Исправлен баг с <b>extra_column</b> в <b>reader</b></li>
<li>[<b>reader</b>] <b>hierarchy_table</b> теперь выбирается внутри <b>sub_path</b></li>
<li>[<b>queries</b>] Деманд считается без учета сессий с одним пином</li>
    </ul>
</details>
</br>


<details>
<summary><u>Версия 2.0.45</u></summary>
    <ul>
    <li>[<b>graph</b>] Переделана работа с логами в графе. Теперь директории для логов будут создаваться непосредственно перед использованием + действительно можно сменить путь для логов после создания объекта</li>
<li>[<b>util</b>] объект <b>EmptyWithStatement</b>, который игнорирует <b>with</b></li>
<li>[<b>graph</b>] у <b>DataManager</b> теперь можно отрывать <b>lock</b> без последствий для работы (только если вы не в параллельном режиме запускаетесь, конечно)</li>
    <li>[<b>queries.runner</b>] <b>write_forecast</b> умеет записывать несколько дополнительных столбцов</li>
<li>[<b>queries.reader</b>] <b>read_parameter</b> умеет читать несколько дополнительных столбцов</li>
<li>[<b>queries.reader</b>] в <b>read_normalization</b> можно выбрать, какая колонка в таблице с нормализацией будет фактом, а какая - нормализованными данными</li>

    </ul>
</details>
</br>


<details>
<summary><u>Версия 2.0.44</u></summary>
    <ul>
<li>[<b>queries.yql_src</b>] Добавлены скрипты расчета когорт и метрик для лавок</li>
<li>[<b>queries.yql_src</b>] когорты в лавках больше не содержат закрывшиеся лавки</li>
<li>[<b>queries.yql_src</b>] <b>city_capacity</b> и <b>lavka_zones_populataion</b> теперь имею поле <b>month</b> и не удаляют результаты предыдущих запусков</li>
<li>[<b>queries.runner</b>] <b>city_capacity</b> и <b>lavka_zones_population</b> реплицируются на <b>greenplum</b></li>
<li>[<b>cron.lavka</b>] Добавлен <b>recount_inputs</b> для лавки</li>
<li>[<b>cron.lavka</b>] Запрос с расчетом когорт переехал в <b>queries</b></li>
<li>[<b>queries.yql_src</b>] Исправлен запрос для населения лавок. Теперь там действительно учитываются разные зоны по типам доставки. И оттуда убраны города, чтобы лавку на разбивало на несколько городов</li>
<li>[<b>queries.reader</b>] <b>read_table</b> с фильтром заработал для gp</li>
<li>[<b>queries.reader</b>] В <b>read_table</b> можно передавать <b>run_kwargs</b></li>
<li>[<b>queries.yql_src</b>] Добавлен скрипт <b>download_any_table</b> для <b>reader_gp</b></li>
<li>[<b>models</b>] <b>SeriesModelWrapper</b> теперь может сохранять данные на <b>fit</b> и строить прогноз по ним, а не по тем, что переданы в <b>forecast</b></li>
<li>[<b>models</b>] <b>CohortModel</b> будет работать, если измерения нет в данных, переданных в <b>forecast</b>, но по нему есть новички и для него есть результаты обучения</li>
<li>[<b>models</b>] <b>TruncatedCohortModel</b> получила параметр <b>default_churn_rate</b>, в который можно отдавать значение <b>churn_rate</b> для тех измерений, для которых не смогли его обучить</li>
<li>[<b>models</b>] В <b>UserBaseModel</b> правда работает ограничение сверху и снизу на <b>value_name</b></li>
<li>[<b>runner.recount_all_capacity</b>] Исправлено название и добавлен <b>grant</b> в <b>replicate</b></li>
    </ul>
</details>
</br>


<details>
<summary><u>Версия 2.0.43</u></summary>
    <ul>
    <li>[<b>databases</b>] Исправили работу <b>greenplum.replicate</b> и изолирование импортов с типами данных</li>
    <li>[<b>botolib</b>] Убрали ещё пару причин падений ботов из-за возвращаемых пустых списков и словарей</li>
    <li>[<b>convert</b>] ScaleConverer не будет выкалывать отдельные дни в маленьких городах (если там случается 0 поездок где-то в истории)</li>
    <li>[<b>convert</b>] ScaleConverer теперь может конвертировать из дней в указанный скейл</li>
    <li>[<b>convert</b>] ScaleConverer не удаляет данные при работе в режиме AMR, если факта в AMR не нашлось. Вместо этого идет переключение на конвертацию по cubic-кривой</li>
    <li>[<b>util</b>] В monitor_difference_frames можно передавать значение в абсолютах, которое не стоит считать расхождением</li>
    </ul>
</details>
</br>


<details>
<summary><u>Версия 2.0.42 (версия содержит критические баги)</u></summary>
    <ul>
    <li>* <b>new</b> <b>version</b> 2.0.41.4</li>
<li>* <b>Update</b> <b>README.md</b></li>
<li>[<b>queries.yql_src</b>] Переписаны запросы <b>capacity.</b> Теперь в них включен расчет населения Лавок</li>
<li>[<b>queries.runner</b>] Появился метод <b>get_polygons_capacity</b>, который позволяет получить население списка произвольных полигонов</li>
<li>[<b>graph.data_manager</b>] В <b>init</b> при генерации <b>store_folder</b> в конце добавляется произвольный ключ, чтобы даже если тесты в одновременно создавали файл, они не конфликтовали</li>
<li>[<b>databases.database</b>] Добавился метод <b>get_table_schema</b></li>
<li>[<b>databases.hahn</b>] Появился метод <b>get_table_schema</b></li>
<li>[<b>databases.greenplum</b>] Метод <b>get_table_structure</b> переименован в <b>get_table_schema</b></li>
<li>[<b>databases.greenplum</b>] При репликации метод берет типы из схемы в yt и переводит их в гринпламовские типы</li>
<li>[<b>databases</b>] Появились словари для перевода типов данных одних DB в другие</li>
    </ul>
</details>
</br>


<details>
<summary><u>Версия 2.0.41.4</u></summary>
    <ul>
    <li>[queries.runner] Исправлен баг с <b>gp_table_names</b> в <b>replicate</b></li>>
    </ul>
</details>
</br>


<details>
<summary><u>Версия 2.0.41.3</u></summary>
    <ul>
    <li>[<b>queries.queries_config</b>] Для GP параметр <b>hierarchy_table_gp</b> переименован в <b>hierarchy_table</b></li>
<li>[<b>queries.runner</b>] В <b>create_report</b> появился параметр <b>hierarchy_table</b>, которые передается в <b>recount_metrics_gp</b> и в запрос с отчетом</li>
<li>[<b>queries.runner</b>] В <b>replicate</b> исправлен баг, при котором таблицы реплицировались в одно место при передаче списка таблиц</li>
<li>[<b>cron.forecast.recount</b>] <b>metrics_gp</b> считаются, используя все аггломерации</li>
<li>[<b>cron.forecast.report</b>] Таблица для балансового отчета (и зависимые таблицы <b>metrics_gp</b>) считаются , используя все аггломерации</li>
    </ul>
</details>
</br>


<details>
<summary><u>Версия 2.0.41.2</u></summary>
    <ul>
    <li>[<b>queries</b>] <b>hierarchy_table</b> и <b>hierarchy_table_gp</b> добавлены в <b>mutable_parameters</b></li>
    </ul>
</details>
</br>


<details>
<summary><u>Версия 2.0.41.1</u></summary>
    <ul>
    <li>[<b>queries</b>] hierarchy_table переехал в параметры</li>
<li>[<b>queries</b>] Передача параметра про hierarchy_table производится через $hierarchy, где есть start_part и прописано отдельно в параметрах, где его нет</li>
<li>[<b>cron.make_fact</b>] Недельный факт в incomplete_scale больше не пересчитывается по часовым точкам, а сами часовые точки не считаются по всем аггломерациям</li>
    </ul>
</details>
</br>


<details>
<summary><u>Версия 2.0.41</u></summary>
    <ul>
    <li>[<b>queries</b>] У всех запросов обращение к иерархии происходит через переменную <b>hierarchy_table</b>, в который можно передать <b>hierarchy_with_all_agglomeration</b> для расчета по все агломерациям</li>
<li>[<b>reader</b>] У <b>read_table</b> добавилась возможность передачи фильтра</li>
<li>[<b>reader</b>] У <b>read_table</b> появился флаг <b>use_all_agglomerations.</b> Если он <b>False</b>, регионы зафильтруются по наличию в основной иерархии</li>
<li>[<b>cron.forecast</b>] <b>make_fact</b> разбивает <b>supply_change</b> и <b>demand_elasticity</b> по всем регионам</li>
    </ul>
</details>
</br>


<details>
<summary><u>Версия 2.0.40.6</u></summary>
    <ul>
    <li>[<b>graph.forecast_model</b>] В методе <b>_send_to_manager</b> начал логироваться момент с чтением параметров.</li>
    </ul>
</details>
</br>


<details>
<summary><u>Версия 2.0.40.5</u></summary>
    <ul>
    <li>[<b>geo_tools</b>] <b>add_by_region_id</b> получил аргумент <b>target_columns_rename</b>, в который можно передавать то, во что переименовать целевые столбцы</li>
<li>[<b>geo_tools</b>] <b>add_by_region_id</b> удаляет столбцы из <b>target_columns_rename</b>, если они уже есть в датафрейме</li>
<li>[<b>queries.runner</b>] В случае отсутствия части <b>region_name</b> <b>write_forecast</b> дополнит их (раньше дополнил если бы совсем не было колонки)</li>
    </ul>
</details>
</br>


<details>
<summary><u>Версия 2.0.40.4</u></summary>
    <ul>
    <li>[<b>databases.greenplum</b>] Изменено кол-во строк с 1 до 1000 в <b>get_table_structure.</b> Теперь меньше шансов ошибиться с типом колонки</li>
    </ul>
</details>
</br>


<details>
<summary><u>Версия 2.0.40.3</u></summary>
    <ul>
    <li>[<b>bots</b>] Исправлены проблемы с кодировками при отсылке картинок</li>
<li>[<b>graph.deviations_report</b>]  В <b>build</b> добавлено принудительное выставление типов колонок перед записью в патч</li>
<li>[<b>cron.budget.compute_deviations</b>] В <b>compute_scale</b> добавлен аргумент <b>skip_forecast_calculation</b>, который позволяет пропустить запуск графа и собрать отчет на посчитанных ранее данных</li>
<li>[<b>graph.configuration</b>] В <b>check_contains</b> появился аргумент <b>is_any.</b> Позволяющий выбирать, как отфильтровывать конфигурации  по <b>include_configurations</b> и <b>exclude_configurations</b></li>
<li>[<b>graph.configurator</b>] В <b>run</b> и <b>process_model</b> передается <b>configuration_filter_kwargs</b>, потаскивающиеся в  <b>check_contains</b></li>
    </ul>
</details>
</br>


<details>
<summary><u>Версия 2.0.40.2</u></summary>
    <ul>
    <li>[<b>bots</b>] Исправлены проблемы с кодировками при отсылке картинок</li>
    <li>[<b>queries</b>] В конце пересчета commissions функция дропается. Не будет проблем с запусками не из-под робота</li>
    </ul>
</details>
</br>


<details>
<summary><u>Версия 2.0.40.1</u></summary>
    <ul>
    <li>[<b>queries</b>] вычисление субсидий в <b>tariff_metrics</b> исправлено</li>
<li>[<b>queries</b>] Добавился расчет <b>subsidies</b> и <b>commissions</b> в <b>metrics_gp</b></li>
<li>[<b>queries</b>] Субсидии для <b>agg_management_metrics</b> считаются по таблице <b>subsidies</b></li>
<li>[<b>graph.deviations_report</b>] В <b>build</b> добавлен аргумент <b>data_to_append.</b> Туда можно передать сторонние данные, которые нужно добавить в отчет</li>
<li>[<b>cron.budget.compute_deviations</b>] Добавился метод  <b>append</b> <b>to_report</b> читающий данные из <b>metric_gp</b></li>
<li>[<b>greenplum</b>] Появился метод <b>get_table_structure</b>, который вернет словарь со столбцами таблицы и их типами</li>
<li>[<b>databases.greenplum</b>] В <b>get_table_meta</b> появился параметр <b>if_not_exists.</b> Если '<b>fall</b>' - упадет, если '<b>return</b>' - вернет пустой датафрейм</li>
<li>[<b>databases.greenplum</b>] <b>check_table_exists</b> теперь работает на основе <b>get_table_meta</b></li>
<li>[<b>queries</b>] <b>Subsidies</b> теперь не вьюшка, а таблица</li>
    </ul>
</details>
</br>


<details>
<summary><u>Версия 2.0.40</u></summary>
    <ul>
    <li>[<b>queries</b>] <b>runner.get_small_forecast_input</b> теперь работает на <b>region_id</b></li>
<li>[<b>graph</b>] исправлен баг в валидации графа, из-за которого статус неверно определялся</li>
<li>[<b>util</b>] в <b>left_first_join</b> можно передать флаг, который приведет результат к виду левого датафрейма</li>
<li>[<b>util.basic</b>] Пофикшено противоречие про <b>is_html</b> между документацией и кодом</li>
    </ul>
</details>
</br>


<details>
<summary><u>Версия 2.0.39.2</u></summary>
    <ul>
    [queries] runner.get_small_forecast_input теперь работает на region_id
    </ul>
	<ul>
    [graph] исправлен баг в валидации графа, из-за которого статус неверно определялся
    </ul>
</details>
</br>


<details>
<summary><u>Версия 2.0.39.1</u></summary>
    <ul>
<li>[<b>queries</b>] <b>read_parameter</b> в <b>greenplum</b> снова работает с кастомными путями не из конфига</li>
<li>[<b>queries</b>] <b>write_forecast</b> может добавить <b>region_name</b> по названию <b>region_id</b> перед заливкой данных</li>
<li>[<b>models</b>] <b>AdjustModel</b> теперь будет нормально рисовать прогноз</li>
    </ul>
</details>
</br>


<details>
<summary><u>Версия 2.0.39</u></summary>
    <ul>
    <li>[<b>queries</b>] В запросе <b>capacity</b> изменилась таблица источник с <b>metrika-mobile-log</b> и <b>metrika-mobile-private-log</b> на <b>appmetrica-location-log</b></li>
    </ul>
</details>
</br>


<details>
<summary><u>Версия 2.0.38.1</u></summary>
    <ul>
    <li>[<b>graph</b>] <b>DataManager</b> снова может принимать <b>sys.stderr</b> вместо <b>logfile</b> (и делает это по-умолчанию)</li>
<li>[<b>anomaly</b>] <b>AnomalyCorrector</b> умеет автоматически добавлять в исключения малые города</li>
<li>[<b>models</b>] <b>OneParameterModel</b> будет кидать ворнинги, если не получилось сделать подстановку параметров (вместо падения)</li>
<li>[<b>seasonality</b>] <b>RotationSeasonality</b> могла становиться отрицательной. Если на такое наткнулись, теперь она вернёт сезонность равную 1</li>
<li>[<b>series_models</b>] <b>ConstrainedLinearModel</b> умеет автоматически подбирать ограничение сверху на <b>slope</b> по ограничению на рост функции за N периодов</li>
<li>[<b>models</b>] <b>TruncatedCohortModel</b> при использовании <b>kernel_model</b> теперь будет предсказывать города, где не было ядра, если передать <b>churn_rate</b></li>
<li>[<b>util</b>] метод <b>make_number</b> теперь умеет работать с каким-то стрёмным пробельным символом в гуглдоках</li>
<li>[<b>util</b>] <b>Handler</b> больше не будет дублировать логи + снова научился работать со стандартными потоками вывода (например <b>sys.stderr</b>)</li>
<li>[<b>queries</b>] поправлен запрос для вычисления метрик в разбивке по тарифам: после апгрейда GP появились проблемы с датами</li>
<li>[<b>util</b>] <b>Handler</b> не будет печатать трейс ошибки, если его не удалось собрать (например, из-за кодировок)</li>
<li>[<b>models</b>] <b>ElasticityModel.validate</b> теперь может пропустить часть городов в своей проверке</li>
<li>[<b>util</b>] <b>normalize_data</b> не будет занулять данные, если в нормализации стоят нули</li>
<li>[<b>planning</b>] <b>HitMultiplicate</b> поправлен баг с маленькими городами + баг, который неправильно собирал коэффициенты (в будущее, вместо прошлого), из-за чего появлялись резкие ступеньки</li>
<li>[<b>planning</b>] <b>Plan.evaluate</b>() будет собирать изменения в абсолютах корректно, в случае, когда в изначальном плане были нули</li>
<li>[<b>planning</b>] <b>Planner.generate_plan</b>() получил аргумент <b>critical_diff_proc</b> для игнорирования (увеличения порога) ограничений на подкрутки. Это позволит автоматически исправлять забагованные модели (где что-то улетело в бесконечность или 0)</li>
<li>[<b>planning</b>] <b>Properties.check_properties</b> будет аккуратнее проверять списки городов и не падать, если модель обучилась для лишних городов</li>
<li>[<b>geo_tools</b>] Пофиксили баг с импортами</li>
<li>[<b>queries.runner</b>] Пофиксили баг с <b>write_forecast</b>, из-за которого записывался только первый <b>parameter_name</b></li>
    </ul>
</details>
</br>


<details>
<summary><u>Версия 2.0.38</u></summary>
    <ul>
    <li>[<b>seasonality</b>] неправильно обрезалась сезонность по нижней границе</li>
<li>[<b>queries.food</b>] Изменена география в соответствии с той, которую используют в еде финансисты</li>
<li><b>graph</b>: В <b>DeviationsReport</b> более компактное сообщение об ошибке</li>
<li><b>queries</b>: <b>write_forecast</b> не ставит принудительно <b>group_data</b>=<b>True</b></li>
<li>[<b>queries.reader</b>]  С помощью <b>read_table_by_path</b> теперь можно читать таблицы из <b>GoogleDoc</b></li>
<li>[<b>util.dataframes</b>] <b>make_numbers_frame</b> теперь пытается преобразовать все столбцы в числа</li>
<li>[<b>util.dataframes</b>] В <b>preprocess</b> появился флаг <b>make_numbers</b>, который вызовет <b>make_numbers_frame</b></li>
<li>[<b>greenplum</b>] новый метод <b>get_table_meta</b>, через который можно получить метаинформацию о таблице (например, её владельца)</li>
<li>[<b>greenplum</b>] увеличили дефолтный размер чанков до 1млн</li>
<li>[<b>geo_tools</b>] <b>add_region_id_by_name</b> удалит колонку <b>region_id</b>, если она уже была в данных</li>
<li>[<b>graph</b>] теперь граф может вызывать <b>Model.validate</b> после обучения модели. Для этого в конфигурацию нужно передать <b>validate</b>=<b>True</b></li>
<li>[<b>graph</b>] <b>index</b> в конфигурации может быть сторкой</li>
<li>[<b>models</b>] в <b>ActivityCohortModel</b> пофикшен баг с запуском в режиме <b>return_all_forecasts</b>=<b>True</b></li>
<li>[<b>models</b>] в <b>GLMModel</b> добавлен <b>validate</b> и несколько приятных методов для понимания, что происходит</li>
<li>[<b>models</b>] в <b>forecast</b> можно передать флаг <b>add_new_columns_to_fact</b>, который проследит, что новые колонки из прогноза не затрутся <b>NaN</b>'ами из факта</li>
<li>[<b>models</b>] в <b>TruncatedCohortModel</b> <b>churn_rate</b> в факте будет заменяться на 1, если там был <b>NaN</b></li>
<li>[<b>queries</b>] в <b>queries_config.get_database_path</b> можно передавать флаг <b>ignore_config</b>, чтобы не городить в конфиге полу-фейковые таблицы "<b>planning</b>/<b>week</b>/<b>...</b>" с прогнозами</li>
<li>[<b>queries</b>] в <b>runner.write_forecast</b> теперь можно отдавать данные без <b>region_id.</b> В этом случае <b>region_id</b> будет подтягиваться автоматически из <b>LocalGeoHierarcy</b></li>
<li>[<b>util</b>] в <b>preprocess</b> можно передавать аргументы <b>fill_missing_cohorts</b> (чтобы добить матрицу ретеншена до квадратной) и <b>types</b> (чтобы изменить часть типов данных, например <b>region_id</b>)</li>
<li>[<b>graph</b>] <b>DataManager.update_parameters</b> будет корректно подставлять таблицы внутрь списковых параметров</li>
<li>[<b>queries</b>] исправлены запросы для вычисления даннных по Еде</li>
<li>[<b>queries.yql_src.food</b>] Исправлена география в <b>start_part</b></li>
    </ul>
</details>
</br>


<details>
<summary><u>Версия 2.0.37.3</u></summary>
    <ul>
    <li>[<b>models</b>] В <b>TruncatedCohortModel</b> добавилась возможность накладываться ограничения на <b>churn_rate</b></li>
<li>[<b>models</b>] В <b>TruncatedCohortModel</b> добавилась возможность продления данных с пустым ядром</li>
<li>[<b>retention</b>] Будут корректно обрабатываться ворнинги, когда <b>dimensions</b> это не строки</li>
<li>[<b>queries</b>] в расчете отчета с насыщенностью, если нет данных о доле, то будем считать, что наша доля 100%</li>
<li>[<b>queries</b>] больше нельзя запрашивать путь к таблице через <b>get_database_path</b>, если <b>query_name</b> не соответствует переданной <b>database</b></li>
<li>[<b>util</b>] <b>data_to_file</b>/<b>data_from_file</b> для <b>pickle</b> будут передавать <b>kwargs</b> в методы <b>dump</b>/<b>load</b></li>
<li>[<b>models</b>] модели пиклятся с <b>protocol</b>=2</li>
<li>[<b>queries</b>] исправлен баг при чтении нормализации (<b>read_normalization</b>) с GP</li>
    </ul>
</details>
</br>


<details>
<summary><u>Версия 2.0.37.2</u></summary>
    <ul>
    <li>[<b>models</b>] в <b>MultipleConfigs</b> можно включать и отключать кидание исключений на <b>fit</b>/<b>forecast</b></li>
<li>[<b>models</b>] в <b>MultipleConfigs</b> исправлен баг с передачей <b>dimensions</b> в дефолтную модель</li>
<li>[<b>graph</b>] исправлена ещё порция багов с отчетом по отклонениям от плана</li>
    </ul>
</details>
</br>


<details>
<summary><u>Версия 2.0.37.1</u></summary>
    <ul>
    <li>[<b>graph</b>] <b>TableID</b> отнаследован от <b>object</b> (чиним баг с <b>mro</b>)</li>
    <li>[<b>anomaly.normalization</b>] исправлена сортировка ключей для Python2 </li>
    </ul>
</details>
</br>


<details>
<summary><u>Версия 2.0.37</u></summary>
    <ul>
    <li>[<b>queries</b>] <b>runner.recount_metrics_gp</b> теперь может возвращать текст запроса</li>
<li>[<b>queries</b>] новый запрос <b>tariffs_metrics</b>, считающий бюджетные метрики в разбивке по тарифам</li>
<li>[<b>queries</b>] метод <b>runner.update_metric_gp</b> умеет обновлять результат расчета объекта. Например, чтобы не перелопачивать весь <b>dm_order</b> каждый раз, а считать только кусочек с новыми данными</li>
<li>[<b>util</b>] <b>parse_dates</b> не будет спамить ворнингами</li>
<li>[<b>models.seasonality.common</b>] Добавлена функция <b>extend_seasonality.</b> Она распространит сезонность от одних измерений к другим. Например, если нужно перенести сезонность страны на все города в ней.</li>
<li>[<b>models.seasonality</b>] Изменен метод <b>crop_seasonality.</b> Теперь он не просто обрежет сезонность, а изменит ее пропорционально ограничениям</li>
<li>[<b>models.seasonality</b>] Добавлен новый вид сезонности - <b>DoubleRotationSeasonality.</b> Она считает одну <b>RotationSeasonality</b>, вычищает ее из данных, считает еще одну по вычищенным данным. После чего объединяет 2 сезонности</li>
<li>[<b>models.series_models</b>] Появилась новая модель <b>ConstrainedLinearModel.</b> Это линейная модель, на все коэффициенты которой можно накладывать ограничения</li>
<li>[<b>models.anomaly</b>] Появилась функция <b>normalize.</b> Она вычищает из данных аномалии.</li>
<li>[<b>util.dataframes</b>] Появилась функция <b>smooth</b>, которая сгладит данные по переданному окну</li>
<li>[<b>util.dates</b>] Появилась функция <b>get_full_dates_borders.</b> Для переданного списка дат она подберет такие даты в более крупном скейле, что весь список точно входит в них</li>
    </ul>
</details>
</br>


<details>
<summary><u>Версия 2.0.36.1</u></summary>
    <ul>
    <li>[<b>queries</b>] <b>runner.get_small_forecast_input</b> теперь может скопировать данные по всем городам (если передать <b>cities</b>=<b>None</b>) и не зависит от наличия/отсутствия таблички <b>planning</b>/<b>week</b>/<b>supply</b></li>
<li><b>queries</b>: <b>runner.replicate</b> теперь можно передавать имя для гпшной таблицы отдельно</li>
<li><b>models</b>:  Правильное склеивание путей в загрузке моделей</li>
<li><b>deviations</b>: всякое</li>
    </ul>
</details>
</br>


<details>
<summary><u>Версия 2.0.36</u></summary>
    <ul>
    <li><b>converter</b>: <b>Converter</b> получил метод <b>filter_value_types</b> который может профильтровать переданные <b>value_types</b> по колонкам в данных</li>
<li><b>crin.budget</b>: <b>recount_inputs</b> пересобирает <b>budget</b>/<b>plan</b> в актуальной бюджетной иерархии</li>
<li>[<b>models</b>] <b>EvalModel</b> теперь может принимать <b>engine</b></li>
<li>[<b>botolib</b>] <b>bot.disable</b>() не будет ронять отдельные методы</li>
<li><b>converter</b>: <b>ConvertedValues</b> научился по-честному  не делать <b>fillna</b> при <b>squueze</b> метрик, если его попросили</li>
<li><b>converter</b>: Производные <b>AggManagementConverter</b> получили дополнительный параметр  <b>derivative_metrics</b> дополнительные метрики, которые модно посчитать над саггрегированными базовыми метриками</li>
<li><b>git_util</b>: новый модуль, враппер над работой с гитом</li>
<li><b>graph</b>: <b>Configurator</b> поправлено составление <b>table_graph</b> в поиске изолированных вершин</li>
<li><b>graph</b>: <b>Configuration</b> теперь можно апдейтить конфигурацию аттрибутами, которых в ней раньше не было(ограничение от <b>DictAlikeObject</b>)</li>
<li><b>graph</b>: <b>DataManager</b> вынесен метод итерации по айдишникам стораджа <b>iterate_keys</b></li>
<li><b>graph</b>: добавился код вычисления прогнозов-отклонения <b>deviations_forecast</b></li>
<li><b>graph</b>: добавился код сборщика репорт-таблицы для отклонений <b>deviations_report</b></li>
<li><b>runner</b>: В <b>update_table_gp</b> явно прописываются колонки при <b>union</b> <b>all</b> (gp не умеет этого автоматически делать)</li>
<li><b>util</b>: <b>dict_recursive_update</b> заимел режим, в котором он списки не перезатирает, а экстендит</li>
<li><b>util</b>: <b>preprocess</b> параметр <b>clip_lower</b> для обрезки данных снизу</li>
<li><b>util</b>: новая функция <b>left_only_join</b> над датафреймами</li>
<li><b>graph</b>: вынесены модели</li>
    </ul>
</details>
</br>


<details>
<summary><u>Версия 2.0.35</u></summary>
    <ul>
    <li><b>convert</b>: <b>ScaleConverter</b> получил режим пропорций <b>amr</b>, где считает все пропорции в том числе неаддивиные по <b>AMR</b></li>
<li><b>geo_tools</b>: багфикс в методе <b>add_region_id_by_name</b></li>
<li>[<b>queries</b>] Для запроса <b>city_last_openings</b> появился аргумент <b>opening_exceptions</b>, в который можно добавлять id регионов, для которых всегда нужно брать их первое появление в <b>dm_order</b> без учета переоткрытий</li>
<li>[<b>queries</b>] В иерархию теперь не добавляются регионы Украины</li>
<li>[<b>models</b>] в <b>RecursionModel</b> исправлен баг, когда флаг <b>has_constant_term</b>=<b>False</b></li>
<li>[<b>models</b>] в <b>EvalModel</b> исправлен баг с группировкой регионов</li>
<li>[<b>models</b>] <b>SeriesModelWrapper</b> и <b>UserBaseModel</b> теперь не будут падать, если в одном из измерений возникла ошибка</li>
<li>[<b>queries</b>] в факт теперь можно грузить <b>users_base</b> по месяцам</li>
<li>[<b>util</b>] нормализация в <b>preprocess</b> делается до кастомных вычислений</li>
<li>[<b>cron.capacity</b>] модель насыщенности немного распуталась + в неё доехал учет <b>COVID</b></li>
<li>[<b>queries</b>] в вычисление таблиц с новичками добавлена фильтрация неполного периода</li>
    </ul>
</details>
</br>


<details>
<summary><u>Версия 2.0.34.2</u></summary>
    <ul>
    <li>[<b>queries</b>] в конфиге наша реплика <b>planning</b> таблиц переименована из *<b>_data</b> в <b>bm_</b>*<b>_data</b></li>
    </ul>
</details>
</br>


<details>
<summary><u>Версия 2.0.34.1</u></summary>
    <ul>
    <li>[<b>graph</b>] в валидации проверяются еще и города, для которых прогноз не собрался</li>
<li>[<b>seasonality</b>] в методе <b>change_seasonality</b>, если сезонность для какого-то измерения не передана, то она считается единичной (то есть теперь падать с исключением не будем)</li>
    </ul>
</details>
</br>


<details>
<summary><u>Версия 2.0.34</u></summary>
    <ul>
<li>[<b>botolib</b>] бота теперь можно отключать и включать методами <b>disable</b> и <b>enable</b></li>
<li>[<b>tests</b>] бот не будет присылать сообщения в чат из графа во время прогонки тестов</li>
<li>[<b>models</b>] новая модель <b>UserBaseModel</b> - предсказывающая новичков от населения</li>
<li>[<b>models</b>] <b>SeriesModelsWrapper</b> не будет игнорировать <b>ndots_fit</b> на фите + можно передать ему параметры для модели в конструктор</li>
<li>[<b>models</b>] в <b>RecursionModel</b> появился флаг, зануляющий свободный член в рекуррентном соотношении</li>
<li>[<b>series_models</b>] включили <b>presort</b>=<b>True</b> по-умолчанию</li>
<li>[<b>graph</b>] в <b>DataManager.update_parameters</b> таблицы будут искаться без учета конфигурации. Если с переданной конфигурацией они не были найдены</li>
<li>[<b>graph</b>] на этапе <b>validate</b> добавлены нотификации в бота, если что-то упало на чтении данных</li>
<li>[<b>queries</b>] при передаче <b>periods_from_today</b> текущая дата будет приводиться к началу скейла (чтобы кэширование в <b>yql</b> работало нормально)</li>
    </ul>
</details>
</br>


<details>
<summary><u>Версия 2.0.33</u></summary>
    <ul>
<li><b>queries</b>: <b>sub_path</b> может быть списком</li>
<li>[<b>models</b>] новая модель <b>AdjustModel</b> -- предсказывает отклонение метрики от голдена и так продлевает основную метрику</li>
<li>[<b>curves</b>] две новые кривые на основе сигмоиды <b>SigmoidCurve</b> и <b>DoubleSigmoidCurve</b></li>
<li>[<b>curves</b>] у <b>Curve</b> появляется метод <b>get_seed</b>, который умеет подбирать дефолтные параметры под конкретные данные</li>
<li>[<b>models</b>] немного аккуратнее очищаются <b>verbose_parameters</b> на <b>fit</b></li>
<li>[<b>models</b>] метод <b>Model.get_dimensions_from_dataframe</b> возвращает <b>tuple</b> со значениями измерений из переданного датафрейма</li>
<li>[<b>graph</b>] <b>DataManager.update_parameters</b> теперь будет честно копировать входные параметры</li>
<li>[<b>graph</b>] <b>ForecastModel</b> будет сохранять в себя модель сразу после создания (а не только при успешном обучении) + в текст лога с ошибкой добавится название модели</li>
<li>[<b>graph</b>] конфиг с параметрами модели можно задавать в виде <b>python-</b>файла, в котором есть переменная <b>config</b></li>
<li>[<b>reader</b>] метод чтения нормализованных данных в любом скейле: <b>read_normalization</b></li>
<li>[<b>dataframes</b>] метод <b>normalize_data</b> по-умолчанию будет считать, что данные с нормализацией приходят в том же скейле, что и основные данные</li>
<li>[<b>dataframes</b>] метод <b>preprocess</b> может сделать группировку данных</li>
<li>[<b>dataframes</b>] в <b>left_first_join</b> исправлен баг, из-за которого неправильно вычислялось название колонки, если в ней содержался <b>suffix</b></li>
    </ul>
</details>
</br>


<details>
<summary><u>Версия 2.0.32</u></summary>
    <ul>
    <li>[<b>models</b>] в <b>ActivityModel</b> исправлен баг, не позволявший подставить кастомную активность</li>
<li>[<b>models</b>] в <b>CohortModel</b> новичков теперь правда можно передавать в виде словаря</li>
<li>[<b>queries</b>] переезд <b>demand_sessions</b> в <b>CDM</b></li>
<li><b>convert</b>: <b>HierarchyConverter</b> научился работать с неаддитивными метриками</li>
<li><b>convert</b>:  <b>NonAdditiveValues</b> по дефолту <b>squueze</b>'ятся через <b>median</b> вместо <b>sum</b></li>
<li><b>geo_util</b>: Убрала костыль про подстановку <b>population_groups</b> вместо <b>node_id</b>, зато теперь есть метод, чтобы извлекать ноды-популяции из геоиерархии</li>
<li>[<b>queries.reader</b>] в <b>read_parameter</b> появился параметр <b>from_date.</b> С ним можно прочесть все данные не раньше переданной даты</li>
<li>[<b>queries.reader</b>] в <b>read_parameter</b> добавлен параметр <b>periods_from_today.</b> С его помощью можно прочесть последние n периодов от сегодняшнего дня (по <b>filter_scale</b>).</li>
<li><b>queries</b>: фикс фильтрации даты в <b>read_parameter</b></li>
<li>[<b>queries</b>] новая группа запросов на GP <b>food</b> с данными еды для планирования</li>
<li>[<b>queries</b>] теперь можно добавить <b>start_part</b> в конкретную группу запросов, в том числе в  GP запросы, если они начинаются с "<b>WITH</b> <b>...</b>"</li>
<li>[<b>util.log</b>] В <b>Handler</b> появился параметр <b>finally_call</b>, куда можно передать функцию, которая всегда выполнится в конце</li>
<li>[<b>queries.queries_configs</b>] Появился метод <b>reset_prefix</b>, который вернет префикс к дефолтному значению</li>
<li><b>geo_tools</b>:  Добавились функции для приджойнивания <b>region_id</b> по имени региона и произвольной гео-колонки по <b>region_id</b></li>
<li><b>queries</b>: Оклонения и бюджетный отчет переехали в <b>query</b>='<b>budget</b>'</li>
<li><b>queries</b>: В <b>runner</b> появился метод для накатывания патча на gp табличку</li>
<li><b>queries</b>: Добавился рассчет финаннсовых метрик в <b>aggmanagement_metrics</b></li>
<li><b>util</b>: <b>shift_date</b> может работать с кварталами</li>
<li><b>queries</b>: Переехал  запрос от <b>scaleconverter</b></li>
<li><b>converter</b>: Рефакторинг <b>ScaleConverter</b></li>
<li>[<b>util.dataframes</b>] Появился метод <b>normalize_data</b>, который убирает из данных аномалии</li>
<li>[<b>util.dataframes</b>] В <b>preprocess</b> добавился аргумент <b>normalize</b>, при передаче которого вызовется <b>normalize_data</b></li>
<li>[<b>models.seasonality</b>] В <b>RotationSeasonality</b> появился аргумент <b>iteration_step</b>, определяющий размер шага при вычислении сезонности</li>
    </ul>
</details>
</br>


<details>
<summary><u>Версия 2.0.31</u></summary>
    <ul>
    <li><b>queries</b>: в <b>balance_report</b> будут корректно считаться доверительные интервалы</li>
<li><b>queries</b>: в запросе для записи плана исправлен баг с джойном</li>
<li><b>converter</b>: Переименование метрики <b>revenue</b> -> <b>gross_revenue</b></li>
<li>[<b>botolib</b>] при отправке файлов они читаются как rb</li>
<li><b>configurator</b>: <b>Configurator.score</b> -- правильное считывание <b>fact_data</b></li>
<li>[<b>cron.lavka</b>] Добавлен скрипт для расчета прогноза по лавкам</li>
<li>[<b>models</b>]  В <b>RecursionModel</b> исправлен баг из-за которого она продлевала данные на 1 точку меньше нужного</li>
    </ul>
</details>
</br>


<details>
<summary><u>Версия 2.0.30.1</u></summary>
    <ul>
    <li><b>queries</b>: <b>capacity_report</b> исправлено вычисление <b>user_cost</b></li>
<li><b>queries</b>: фильтрация часовых метрик по геоиерархии</li>
    </ul>
</details>
</br>


<details>
<summary><u>Версия 2.0.30</u></summary>
    <ul>
    <li>[<b>queries</b>] агломерации берем всегда из операционной иерархии</li>
<li><b>queries</b>: <b>balance_report</b>  корректный шифт для новичков</li>
<li><b>graph</b>: исправлена ошибка со сбрасывающимся аттрибутом <b>append</b> у конфигурации</li>
<li><b>converter</b>: убралось задубливание внутри <b>HierarchyConverter.get_regions</b>()</li>
    </ul>
</details>
</br>

<details>
<summary><u>Версия 2.0.29(содержит баги)</u></summary>
	Залита в репозиторий по ошибке
</details>
</br>

<details>
<summary><u>Версия 2.0.28</u></summary>
    <ul>
    <li>[<b>graph</b>] глобальный рефакторинг метода <b>validate</b> и его результатов</li>
<li>[<b>modesl.anomaly</b>] <b>AnomalyCorrector.get_sos_metrics</b> теперь может возвращать. все данные, а не только часть прогноза: флаг <b>return_only_future</b></li>
<li>[<b>util.dataframe</b>] новый метод <b>get_unique_index</b>, который умет выдавать список уникальных значений индекса (можно выбросить часть измерений)</li>
<li>[<b>util.basic</b>] <b>compare_equal</b> умеет сравнивать <b>Series</b> и <b>DataFrame</b></li>
<li>[<b>cron.forecast</b>] конфиги для валидаций переехали из <b>SanityCheck</b> в <b>Validate</b> и в целом преобразились</li>
<li>[<b>cron.forecast</b>] глобальный рефакторинг скрипта для создания тикета с проблемами <b>errors_logging.py</b></li>
    </ul>
</details>
</br>


<details>
<summary><u>Версия 2.0.27</u></summary>

<ul>
<li>[<b>seasonality</b>] <b>RotationSeasonality</b> - новая сезонность, которая перед вычислением сезонности убирает тренд в данных поворотом. Также умеет считать дневную сезонность внутри недели и распространять её на год данных. Есть пример её использования</li>
<li>[<b>accuracy</b>] набор методов для скоринга сезонности. Основная идея: в <b>SeasonalitySample</b> лежат какие-то красивые модельные данные, мы подставляем их в <b>Model</b> с сезонностью и можем посмотреть на прогноз</li>
<li>[<b>seasonality</b>] <b>create_full_seasonality</b> отрефакторен и теперь занимает меньше места + умеет работать с разными <b>base_scale</b></li>
<li>[<b>seasonality</b>] у <b>change_seasonality</b> в аргументе <b>restricts_sum_change</b> исправлена опечатка</li>
<li>[<b>seasonality</b>] аргумент <b>ensure_sum_eq_periods</b> заменен на работу с инвариантами сезонности: методы *<b>_invariants</b></li>
<li>[<b>plot</b>] в <b>plot_forecast</b> пофикшен порядок отрисовки соединительной линии (теперь цвета более адекватные)</li>
<li>[<b>util</b>] <b>Factory.get_with_fallback</b> больше не кидает исключений</li>
<li>[<b>util</b>] <b>shift_date</b> умеет работать с годами</li>
<li>[<b>util</b>] <b>get_scale_number_in_year</b> теперь умеет считать периоды не только внутри года, но и внутри любого <b>scale</b></li>
<li>[<b>util</b>] <b>get_total_periods</b> - вернет максимальное число периодов внутри более крупного (например, максимальное число дней в году)</li>
<li><b>util</b>: <b>Timer</b> наследник. <b>Handler</b></li>
<li><b>queries</b>: В <b>capacity</b> добавили вычисление <b>population</b> по геоиерахии</li>
<li><b>queries</b>: Добавился <b>capacity_report</b> для построение таблицы для отчета</li>
<li><b>queries</b>: <b>create_balance_report</b> обощился до <b>create_report</b></li>
    </ul>
</details>
</br>


<details>
<summary><u>Версия 2.0.26</u></summary>
    <ul>
    <li><b>graph</b>: У <b>Configurator</b> выделился метод <b>get_forecact_model.</b> Нужно  для теста</li>
<li><b>graph</b>:  в методе <b>score</b> при незаданном <b>end_date</b> больше не будет пролезать последняя неполная неделя</li>
<li><b>queries</b>: переехали на таблицу с иерархией, где есть геозоны</li>
    </ul>
</details>
</br>


<details>
<summary><u>Версия 2.0.25</u></summary>
    <ul>
    <li><b>queries</b>: <b>read_parameter</b> теперь умеет работать и с <b>database</b>='<b>greenplum</b>'. Умеет читать из таблицы по полному пути</li>
<li>[<b>greenplum</b>] В <b>replicate</b> параметр <b>columns_order</b> по умолчанию равен '<b>auto</b>'</li>
<li>[<b>hahn</b>] При ошибке <b>hahn</b> выдает в трейсе публичную ссылку на запрос</li>
<li>[<b>hahn.backup</b>] При отсутствии таблицы, которую нужно бэкапнуть, будет присылаться <b>warning</b> вместо падения</li>
<li><b>models</b>: <b>SeriesModelsWrapper</b> больше не пробрасывает своей модели параметр <b>index</b></li>
<li>[<b>models</b>] в <b>CohortModel</b> теперь не обязательно передавать сезонность как <b>Series</b></li>
<li>[<b>seasonality</b>] сезонность будет кидать понятное исключение, если не передали <b>index</b> ни в каком виде</li>
<li>[<b>queries</b>] в конфиг добавлены две новые таблицы: <b>demand_seasonality</b> и <b>supply_seasonality</b></li>
<li>[<b>queries</b>] <b>forecast_inputs_subsample</b> тащит за собой таблицы с сезонностью тоже</li>
<li>[<b>greenplum</b>] добавлена попытка еще раз авторизоваться, если запрос упал</li>
<li>[<b>models</b>] в <b>GrowthRate</b> починили баг, генерирующий падения, если <b>ndots_fit</b> меньше года</li>
    </ul>
</details>
</br>


<details>
<summary><u>Версия 2.0.24</u></summary>
    <ul>
    <li>[<b>queries</b>] при передаче кастомных регионов, агломерации, которые в них полностью входят удалятся</li>
<li>[<b>queries</b>] по-умолчанию считаем для <b>custom_regions</b>="'<b>fi_ru_</b>100kp', '<b>fi_ru_</b>50km', '<b>fi_ru_</b>50kp'"</li>
<li>[<b>graph</b>] <b>Configurator.run</b> в режиме <b>only_read</b> теперь не запускает валидацию</li>
<li>[<b>graph</b>] в <b>DataManager.pop</b>() исправлена проблема, вызывающая <b>deadlock</b></li>
<li>[<b>graph</b>] <b>Configurator.run.validate</b>() будет падать более детально, прогоняя в любом случае все метрики и спамя в лог о том, какая не отработала из-за багов</li>
<li>[<b>queries</b>] первая попытка решить проблему <b>drop</b>/<b>create</b> в запросах: появились параметры <b>insert_type</b> и <b>optional_as.</b> Они определяются автоматически в зависимости от того существует таблица или нет</li>
<li>[<b>queries</b>] в <b>metrics_gp</b> добавлен расчет <b>region_profile</b> - который содержит набор фактов о регионе (без истории), например, население</li>
<li>[<b>queries</b>] новый тип запросов <b>planning_gp</b> : в нем создание из таблиц <b>ods.am_</b>* широких таблиц (где каждая метрика в своей колонке)</li>
<li>[<b>queries</b>] новый тип запросов <b>report</b> : сейчас в него добавлен балансовый отчет</li>
<li>[<b>queries</b>] <b>QueriesConfig.run_script</b> теперь может просто вернуть текст запроса (удобнее дебажить запросы к GP)</li>
<li>[<b>queries</b>] <b>Runner.recount_metric_gp</b> теперь может пропускать копирование таблицы на YT</li>
<li>[<b>graph</b>] <b>Configuration</b> умеет конвертироваться в красивую строку (в логах станет поприятнее)</li>
    </ul>
</details>
</br>


<details>
<summary><u>Версия 2.0.23.1</u></summary>
    <ul>
    <li><b>queries</b>: мониторинг поправили (перевели окончательно на новую иерархию)</li>
    <li><b>graph</b>: в <b>DataManagerю.write</b> перед записью таблицы поднимаются из дампа</li>
    </ul>
</details>
</br>


<details>
<summary><u>Версия 2.0.23</u></summary>
    <ul>
    <li><b>converter</b>: Перенесли <b>HierarchyConverter</b> на новую иерархию</li>
<li><b>queries</b>: Запрос конвертера уехал в <b>queries</b>, в конфиг пророс новые иерархия и <b>aggmanagement</b></li>
<li><b>geo_tools</b>: Новый класс <b>LocalGeoHierarchy</b>, который хранит локально новую иерарзию, и умеет по ней возвращать нужные ноды с их аттрибутами, показывать все доступные значения параметра и приджойнивать к произвольному даатфрейму <b>population_group</b> по <b>region_id</b></li>
<li>[<b>all</b>] поддержана новая иерархия (в <b>forecast</b>)</li>
    </ul>
</details>
</br>


<details>
<summary><u>Версия 2.0.22</u></summary>
    <ul>
    <li><b>graph</b>: У скоринга поправлен перебор дат, чтобы не создаваласьь <b>ndots_predict</b>=0 расчета</li>
<li>[<b>startrek</b>] новый метод <b>create_or_update_comment</b>, который в зависимости от наличия комментария обновляет его или создает новый</li>
<li>[<b>all</b>] полная совместимость библиотеки с 3 питоном и более новым <b>pandas</b></li>
    </ul>
</details>
</br>


<details>
<summary><u>Версия 2.0.21</u></summary>
    <ul>
    <li>[<b>util</b>] <b>FakeObject</b> на <b>call</b> тоже будет ругаться правильно</li>
<li>[<b>models</b>] в методе <b>fit_forecast</b> была опечатка, я ее поправила и добавила все-таки тесты</li>
<li>[<b>series_models</b>] в <b>CopyModel</b> исправлен баг, неверно считающий коэффициент сглаживания по отношению период к периоду</li>
<li>[<b>series_models</b>] в <b>GrowthRateModel</b> теперь корректно обрабатываются дни</li>
<li><b>graph</b>: Аттрибут <b>data</b> у <b>Table</b> стал <b>property</b> и теперь всегда при обновлении данных автоматически пересчитывается размер таблицы</li>
<li><b>convert</b>: <b>HierarchyConverter</b> пофикшена некорректная работа в режиме <b>skip</b></li>
<li><b>graph</b>: Пофиксшено сообщение об ошибке при коллизии имен таблиц с разными <b>load_parameter</b></li>
<li><b>graph</b>: Логика  заполнения конфига конвертера уехала полностью в конфигуратор в <b>get_parameters</b></li>
<li><b>queries</b>: В скрипте <b>agg_management_metrics.sql</b> исправлен поле источник <b>gmv</b></li>
    </ul>
</details>
</br>


<details>
<summary><u>Версия 2.0.20</u></summary>
    <ul>
    <li><b>models</b>: у моделей появился атрибут <b>is_cohort</b>, отвечающий за то, работают они с когортными данными или нет</li>
<li><b>models</b>: временно удалены модели <b>CohortGLMModel</b> и <b>NPreviousScaleMigration</b> из-за несоответтвия интерфейсу <b>Model</b></li>
<li><b>models</b>: у <b>ActivityCohortModel</b> удалили параметр <b>group_for_activity</b> (заменен на использование <b>Model.is_cohort</b>)</li>
<li><b>models.cluster</b>: при разбивке данных на кластеры стало возможным передавать <b>column_rename</b>, чтобы правило не зависило от названий колонок в данных</li>
<li><b>model.cluster</b>: в правила разбивки <b>FilterCluster</b> теперь можно передавать не только атрибуты,  но и функции без аргументов</li>
<li><b>models</b>: все модели приведены к единому интерфейсу, отвечающему тестам из <b>model_interface_tests.py</b></li>
<li><b>util</b>: <b>deep_compare</b> переехал на <b>iterate_values</b> и теперь покрыт тестами</li>
<li><b>util</b>: <b>change_index</b> научился работать со списками <b>DataFrame</b> на входе</li>
<li><b>util</b>: появился метод <b>get_missing_dates</b>, который сравнивает наборы дат в данных и возвращает различия</li>
<li><b>util.log</b>: <b>Handler</b> научился принимать методы логгирования (это позволяет например передавать в качестве <b>logger</b> <b>print</b> или <b>warnings</b>)</li>
    </ul>
</details>
</br>


<details>
<summary><u>Версия 2.0.19.2</u></summary>
    <ul>
    <li><b>graph</b>: В скоринге добавилась очистка данных в менеджере</li>
    </ul>
</details>
</br>


<details>
<summary><u>Версия 2.0.19.1</u></summary>
    <ul>
    <li><b>graph</b>:  У <b>Configurator</b> теепрь правилная обработка <b>dict</b> в <b>output_tables</b></li>
    </ul>
</details>
</br>


<details>
<summary><u>Версия 2.0.19</u></summary>
    <ul>
    <li><b>databases</b>: <b>gdocs.contains</b> корректно работает с <b>non-ascii</b> именами листов</li>
<li><b>graph</b>:  <b>DataManager</b> дампит только на диск. Счетчик у него таймерный, а не интовый. В <b>Configurator</b> можно эксклюдить конфигурации</li>
<li><b>graph</b>: при скоринге не подчищаются логи</li>
<li><b>startrek</b>: появилась возможность выгружать вложения из конкретного комментария через аргумент <b>comment_id</b> в методе <b>get_attachments</b></li>
<li><b>model</b>: <b>RecursionModel</b> продляет каждый <b>dimension</b> до его финальной даты</li>
    </ul>
</details>
</br>


<details>
<summary><u>Версия 2.0.18</u></summary>
    <ul>
    <li><b>databases</b>: <b>gdocs</b> исправлена ошибка с созданием  <b>sheet</b> с указанной ячейкой</li>
    </ul>
</details>
</br>


<details>
<summary><u>Версия 2.0.17</u></summary>
    <ul>
    <li><b>util</b>: починили импорты потенциально фейковых объектов в 3 питоне</li>
<li><b>models.seasonaliy</b>: <b>Seasonality</b> будет сама следить, чтобы внутри года сумма была равна количеству периодов (решает заодно проблему 52/53 недель и 365/366 дней)</li>
<li><b>convert</b>: багфикс в конвертерах с сезонностью, теперь гарантируется, что конвертер не изменит сумму</li>
<li><b>graph</b>: Исправлены проблемы с именами таблиц при дампе. Поправлены приоритеты сравнения эквивалентности <b>table_id</b></li>
<li><b>queries</b>: Дополнен запрос, делающий сабсемпл продовой папки, чтобы скорингу тоже хватало</li>
<li><b>tests</b>: приехал тест на скоринг</li>
<li><b>databases</b>: произошло обобщение <b>GreenplumManager</b> в <b>DatabaseSql</b> и выделение из него <b>MysqlManager</b></li>
<li><b>models</b>: В <b>MultipleConfigs</b> больше не приджойниваются в результат пустые возвращенные датафреймы, чтобы схему не портить</li>
<li><b>graph</b>: У конфигуратора появилась опция <b>skip_top_level_source</b> -- чтобы не читать верхнеуровневые таблицы(легкий способ заигнорить скоринг)</li>
<li><b>graph</b>: исправления в скоринге</li>
<li><b>tests</b>: исправления в тестах скоринга</li>
    </ul>
</details>
</br>


<details>
<summary><u>Версия 2.0.16.1</u></summary>
    <ul>
    <li><b>graph</b>: фикс итерации во ключам датаменеджера в <b>parallel</b> режиме</li>
    </ul>
</details>
</br>


<details>
<summary><u>Версия 2.0.16</u></summary>
    <ul>
    <li><b>converters</b>: В <b>Hierarchyonverter</b> появились опции для предварительного отбрасывания регионов из данных и "что делать если нам передали регионы на конертацию, а они уже есть"</li>
<li><b>converters</b>: Пропорции всегода теперь имебют суффикс <b>proportions</b></li>
<li><b>graph</b>: <b>ForecastModel</b> теперь может работать в режиме конвертера. Починили баг с параллельным дампом в датаменеджере</li>
<li><b>model</b>: <b>ClusterModel</b> если какая-то из подмоделей не смогла предсказать <b>dimension</b> -- он полностью дропается из результата, а не возвращается нулем</li>
<li><b>queries</b>: <b>reader.read_table_by_path</b>  может читать из <b>sub_path.</b> В  <b>runner.write_forecast</b> создается не <b>yt.TempTable</b>, а генерится временная таблица в //<b>tmp</b>, чтобы было проще дебажить падения</li>
<li><b>util</b>: добавлена функция для рекурсивного апдейта вложенных словарей <b>dict_recursive_update</b> и функция для мерджа датафреймов с приоритетом <b>left_first_join</b></li>
<li><b>botolib</b>: починили несовместимость <b>bot.get_updates</b>() с py3</li>
<li>[<b>gdocs</b>] В метод <b>write</b> добавлен флаг <b>if_not_exists</b>, говорящий что делать, если таблицы нет</li>
<li>[<b>gdocs</b>] Добавлены более понятные падения от наличия/отсутствия листа</li>
<li>[<b>common_scripts</b>] Обновлен пример для <b>gdocs</b></li>
<li>[<b>common_scripts</b>] Небольшие изменения в тексте большого примера</li>
<li><b>all</b>: Все импорты и объекты требующие токенов завернуты в специальный класс, кидующий внятные исключения</li>
    </ul>
</details>
</br>


<details>
<summary><u>Версия 2.0.15</u></summary>
    <ul>
    <li>[<b>models.Model</b>]  Появился <b>_plot_forecast</b>  - общий метод отрисовки прогноза для моделей</li>
<li>[<b>models.OneParameterModel</b>]  Добавлена логика отрисовки</li>
<li>[<b>models.CohortModel</b>] Переименован метод отрисовки форкаста</li>
<li>[<b>plot</b>] Если в <b>plot_object</b> передан <b>label</b>, легенда будет выводиться автоматически</li>
<li>[<b>models.SeasonalityModel</b>] Добавлена логика отрисовки</li>
<li><b>util</b>: добавлены методы <b>iterate_values</b> (генератор всех внутренностей словаря) и <b>flatten_list</b></li>
<li><b>model</b>: <b>Model.get_nested_models</b> переехал на <b>iterate_values</b></li>
<li><b>model</b>: в <b>Model.plot</b> добавлена поддержка вложенных моделей</li>
<li><b>plot</b>: комментарии доехали до всех новых методов отрисовки</li>
<li>[<b>plot</b>] Добавлен кусок, соединяющий факт и прогноз в <b>plot_forecast</b></li>
<li>[<b>model</b>] Добавлен метод <b>fit_forecast</b></li>
<li>[<b>common_scripts</b>] Появился большой и классный пример по работе с моделями</li>
    </ul>
</details>
</br>


<details>
<summary><u>Версия 2.0.14</u></summary>
    <ul>
    <li><b>hahn</b>: багфикс ожидания анлока таблицы: если лок таблицы не существует нечего и ждать</li>
<li><b>hahn</b>: Добавили запуск запроса по <b>public-link</b></li>
<li><b>graph</b>: Большой рефакторинг. Выделен объект конфигурации. Добавлено измерение в <b>TableId.</b> Датаменджер может шарить свой словарь между потоками</li>
<li><b>models</b>: Во враппере <b>forecast</b>'а у <b>Model</b> появился флаг <b>validate_params_consistency</b> позволяющий скипать проверку консистентности параметров</li>
<li><b>queries</b>:  Методы <b>read_table</b>/<b>write_forecast</b>/<b>read_parameter</b>/<b>write_table</b> научились писать и писать <b>value_name</b>'ы c тегами</li>
<li><b>util</b>: <b>DictAlikeObject</b> добавили метод <b>update</b>  и метод <b>as_dict</b> стал публичным</li>
<li>[<b>runner</b>] Добавлены методы <b>recount_capacity</b> и <b>recount_all_capacity</b>, пересчитывающие скрипты из группы <b>capacity</b></li>
<li><b>plot</b>: новый набор методов для рисования <b>add_axes</b>, <b>plot_object</b>, <b>plot_dataframe</b>, <b>plot_scale_index</b>, <b>plot_many</b>, <b>plot_forecast</b></li>
<li><b>models</b>: у <b>Model</b> появился метод <b>plot</b> для отрисовки информации о предсказании</li>
<li><b>models</b>: в <b>CohortModel</b> исправлен баг, из-за которого сезонность на <b>fit</b> не всегда вычищалась + добавлена реализация отрисовки модели</li>
<li><b>util</b>: в функции <b>get_list</b> флаг <b>wrap_list</b> оборачивает список только если внутри не все является списками</li>
    </ul>
</details>
</br>


<details>
<summary><u>Версия 2.0.13</u></summary>
    <ul>
    <li><b>databases</b>: <b>Greenplum</b> во <b>write</b> теперь тоже работает флаг <b>with_truncate.</b> В методах <b>write</b> и <b>replicate</b> появился флаг <b>columns_order</b>, которым можно выравнивать колонки датафрейма</li>
<li><b>util</b>: функция <b>to_wiki_table</b> для конвертации <b>DataFrame</b> в табличку в вики-разметке</li>
<li><b>models</b>: <b>SeriesModelWrapper</b> корректно обрабатывает <b>verobse</b></li>
    </ul>
</details>
</br>


<details>
<summary><u>Версия 2.0.12.4</u></summary>
    <ul>
    <li><b>models</b>: <b>bugfix-2</b> в <b>MultipleConfigsModel</b> дважды обрабатывались города</li>
    <li>util: dataframes.preprocess не падает на eval со всякими сложными функциями типа cumsum</li>
    </ul>
</details>
</br>


<details>
<summary><u>Версия 2.0.12.3</u></summary>
    <ul>
    <li><b>models</b>: <b>bugfix</b> в <b>MultipleConfigsModel</b> дважды обрабатывались города</li>
    </ul>
</details>
</br>


<details>
<summary><u>Версия 2.0.12.2</u></summary>
    <ul>

    </ul>
</details>
</br>


<details>
<summary><u>Версия 2.0.12.1</u></summary>
    <ul>
    <li><b>hahn</b>: добавился параметр для ожидания разлоченной таблицы</li>
<li><b>queries</b>: запись в <b>planning</b> добавляет к вызову хана ожидание разлока</li>
<li><b>graph</b>: В <b>DataManager</b> повышен лимит по памяти, и создается папка для временных файлов</li>
    </ul>
</details>
</br>


<details>
<summary><u>Версия 2.0.12</u></summary>
    <ul>
    <li><b>queries</b>: тащим <b>trips_plan</b> из <b>agg_management</b></li>
<li><b>databases.gdocs</b>: поправили имя индекса при записи</li>
<li><b>models.series_models</b>: добавили <b>AbsoluteGrowthModel</b></li>
<li><b>databases.greenplum</b>: <b>replicate</b> получил опцию <b>with_truncate.</b> Если она <b>True</b>, то перзапись не дропает и пересоздает таблицу, а просто  транкейтит существующую</li>
<li><b>databases.gdocs</b>: обрабатываем исключения типа <b>connection</b> <b>reset</b> by <b>peer</b> повторным перезапросом</li>
<li><b>models</b>: почнили багу со сбрасыванием индекса в <b>fit_wrapper</b></li>
<li><b>models.SeasonalityModel</b>: можно <b>verbose</b> прокидывать в <b>forecast</b></li>
<li><b>models.plot</b>: рефакторинг <b>plot_many_frames</b></li>
<li><b>queries.reader</b>: новый метод <b>call_proxy</b> читает результат выполнения запроса</li>
<li><b>models</b>: В <b>TruncatedCohortModel</b> вставили быстрофикс проблемы с предсказанием чурна по датафрейму с одним городом</li>
<li><b>models.series_model</b>: не падает при передаче пустого <b>series</b></li>
<li><b>models</b>: Методы <b>forecast</b> всех моделей заворачиваются декоратором, который гарантирует копирование данныз, сброс индекса, фильтрацию перед непосредственным выполнение форкаста, сортировку по индексным колонкам, сброс индекса и заворачивание в <b>ModelResultsHolder</b> после выполнения</li>
<li><b>models</b>: Добавились спец типы исклчений и ворнингов <b>ModelParametersError</b> и <b>ModelParametersWarning</b> для плохих параметров моделей</li>
<li><b>models</b>: <b>bugfix</b> <b>fit</b> в моделях без фита разваливался</li>
<li><b>models.seasonality_model</b>: <b>bugfix</b> прикрыли проблему с лишним пробросом <b>return_all_forecasts</b></li>
    </ul>
</details>
</br>


<details>
<summary><u>Версия 2.0.11.1</u></summary>
    <ul>
    <li><b>models.series_models</b> : <b>growthratemodel</b> пофиксили баги со скейлами</li>
<li><b>hahn</b>: аргументы <b>files</b> и <b>urls</b> теперь работают</li>
<li><b>models</b>: В <b>CohortModelm</b> дефолт <b>series_mode</b> -- l это <b>nonlinear</b></li>
<li><b>databases.greenplum</b>: Исправлен поиск <b>username</b> через <b>yaml</b> конфиг</li>
<li><b>databases</b>:<b>gdocs</b>: Исправлен баг с  авторизацией, от котрого страдал только <b>yaml</b> конфиг</li>
    </ul>
</details>
</br>


<details>
<summary><u>Версия 2.0.11</u></summary>
    <ul>
    <li><b>databases.greenplum</b>: Не падает при %% в делении</li>
<li><b>models</b>: <b>SeriesModelsWrapper</b> больше не изменяет прошлое</li>
<li><b>models</b>: в <b>ElasticityModel</b> снова корректно работают методы <b>get_</b>*</li>
<li><b>models</b>: починили переставшие прорастать в модели <b>substitution_rules</b></li>
<li>[<b>cron.budget</b>] Добавлены конфиги для границ новичков</li>
<li>[<b>models.series_models</b>] <b>GrowthRateModel</b> научилась порождать векторы роста на основе переданного <b>series</b></li>
<li>[<b>tests.model_tests</b>] Добавлен тест для <b>GrowthRateModel</b></li>
<li><b>models</b>: в <b>TruncatedCohortModel</b> добавлен вариант с вычислением <b>churn_rate</b> (должен переехать в <b>CohortModel</b> однажды)</li>
<li><b>models</b>: <b>TruncatedCohortModel</b> <b>fix</b></li>
<li><b>databases</b>: <b>gdocs-hotfix</b>, падало, если при чтении в заголовок попадала полностью пустая строка, теперь не будет падать</li>
<li><b>models</b>: <b>OneParameterModel</b> <b>verbose</b>=<b>True</b> снова работает</li>
<li>* <b>fixes</b></li>
<li>* <b>Update</b> <b>add_base_regions.py</b></li>
    </ul>
</details>
</br>


<details>
<summary><u>Версия 2.0.10.2</u></summary>
    <ul>
    <li><b>databases.greenplum</b>: Не падает при %% в делении</li>
    </ul>
</details>
</br>


<details>
<summary><u>Версия 2.0.10.1</u></summary>
    <ul>
    <li><b>queries</b>: <b>agg_management_metrics</b> считают деньги в рублях, а не в локальной валюте</li>
    </ul>
</details>
</br>


<details>
<summary><u>Версия 2.0.10</u></summary>
    <ul>
    <li><b>models.elasticity_model</b>: Пофикшен баг с потерей параметра <b>balance</b> при копировании модели</li>
<li><b>botolib</b>: <b>send_message</b> научился разбивать длинные сообщения</li>
<li><b>databases.gdocs</b>: Правильно берется дефолтный путь до <b>credentials</b></li>
<li><b>databases.greenplum</b>: Теперь в <b>call</b> будет автоматом эскейпится процент.  И запуск операций будет с автокоммитом</li>
<li><b>config_holder</b>: более информативное сообщение про ненайденные аттрибуты</li>
<li><b>databases.greenplum</b>: поправила неправильный префикс при поиске по <b>dwh-settings</b> настройкам</li>
<li><b>series_models</b>: <b>YoYSlowDown</b> исправлена проблема с индексами</li>
    </ul>
</details>
</br>


<details>
<summary><u>Версия 2.0.9.1</u></summary>
    <ul>
    <li><b>models.series_models</b>: Убрали принудительное обрушение при подозрении на несоответствие скейлов</li>
<li><b>models</b>: <b>SerieModelsWrapper</b> не делает лишней группировки</li>
<li><b>models.series_models</b>:  В <b>GrowthRateModel</b> поправили баг при автоматическом вычислении коэффициентов роста</li>
    </ul>
</details>
</br>


<details>
<summary><u>Версия 2.0.9</u></summary>
    <ul>
    <li>[<b>queries</b>] в <b>demand_sessions</b> <b>last_pin_tariff_zone</b> заменен на <b>last_tariff_zone.</b> Также удалены остатки расчета <b>user_phone_id_mapping</b></li>
<li><b>util</b>: метод <b>shift_date</b> получил значимое ускорение</li>
<li><b>models</b>: <b>EvalModel</b> может группировать данные по <b>dimensions</b> и вычислять формулы внутри группы (удобно, если используется среднее например)</li>
<li><b>models</b>: <b>EvalModel</b> больше не меняет прошлое и действительно предсказывает на <b>ndots_predict</b></li>
<li><b>optimize</b>: <b>StrategyProperties</b> поддерживают в цепочке предсказания модели, расширяющие индекс</li>
<li><b>queries</b>: <b>runner.get_small_forecast_input</b> умеет принимать на вход <b>date_to</b>, чтобы смоделировать ситуацию, где факт есть только до <b>date_to</b></li>
<li><b>common_scripts</b>: пример для <b>truncatedcohort_model</b></li>
<li><b>models</b>: поправлены опечатки в докстрингах</li>
<li><b>model.series_models</b>:  новая <b>GrowthRateModel</b></li>
<li><b>model</b>: классы <b>Model</b> и <b>SeriesModel</b> снабжены метаклассами для декорации <b>fit</b> и <b>forecast</b></li>
<li><b>model.yoy_model</b>: В <b>forecast</b> появилось дефолтное значение для <b>periods_to_iterate</b></li>
<li><b>model.series_model</b>: <b>GrowthRateModel</b> поправили баги с непрокидывавшимеся кваргми и <b>series</b> длиной 1</li>
<li><b>hahn</b>: исправлен баг, из-за которого неверно считывался результат запроса "<b>select</b> * <b>from</b> <b>range</b>()"</li>
<li><b>graph</b>: <b>Configurator</b> больше не будет посылать информацию о падающих валидациях в чат (только в тикет и в лог)</li>
    </ul>
</details>
</br>


<details>
<summary><u>Версия 2.0.8</u></summary>
    <ul>
    <li>[<b>queries</b>] в <b>demand_sessions</b> <b>last_pin_tariff_zone</b> заменен на <b>last_tariff_zone.</b> Также удалены остатки расчета <b>user_phone_id_mapping</b></li>
<li><b>util</b>: метод <b>shift_date</b> получил значимое ускорение</li>
<li><b>models</b>: <b>EvalModel</b> может группировать данные по <b>dimensions</b> и вычислять формулы внутри группы (удобно, если используется среднее например)</li>
<li><b>models</b>: <b>EvalModel</b> больше не меняет прошлое и действительно предсказывает на <b>ndots_predict</b></li>
<li><b>optimize</b>: <b>StrategyProperties</b> поддерживают в цепочке предсказания модели, расширяющие индекс</li>
<li><b>queries</b>: <b>runner.get_small_forecast_input</b> умеет принимать на вход <b>date_to</b>, чтобы смоделировать ситуацию, где факт есть только до <b>date_to</b></li>
    </ul>
</details>
</br>


<details>
<summary><u>Версия 2.0.7.1</u></summary>
    <ul>
    <li>[<b>queries</b>] в рассчете <b>hourly_demand</b> исправлен баг с обрезанием неполной недели</li>
<li>[<b>plot</b>] больше не будет падать на py3</li>
<li>[<b>tests</b>] падение теста <b>queries.reader</b> из-за нечищенных кешей, падение импорта библиотеки со свежим пандасом из-за <b>msgpack</b></li>
<li>[<b>util</b>] на py3 <b>change_coding</b> возвращает копию объекта, потому что во втором он его копировал</li>
<li>[<b>model</b>] <b>CohortModel</b> не падает с <b>key_seasonality</b></li>
<li>[<b>model</b>] <b>TruncatedCohortModel</b> и <b>ActivityModel</b> корректно обрабатывают <b>dimensions</b> и не падают =)</li>
    </ul>
</details>
</br>


<details>
<summary><u>Версия 2.0.7</u></summary>
    <ul>
    <li><b>models</b>: Большой рефакторинг интерфейсов</li>
<li><b>models</b>: у модели в конструкторе дефолтное <b>scale</b>='<b>week</b>'</li>
<li>[<b>model</b>] новая модель <b>SeasonalityModel</b>, которая умеет вычищать сезонность, продлевать данные без нее и добавлять сезонность обратно</li>
<li>[<b>plot</b>] функция <b>plot_many_frames</b> теперь может группировать данные и рисовать отдельные графики для каждой группы</li>
<li>[<b>series_models</b>] в <b>CopyModel</b> исправлен баг с индексированием, если исходных данных было мало</li>
<li><b>databases.GoogleDocs</b>: новый метод <b>get_all_sheet_titles</b> -- получить список всех листов данного гулдокока</li>
<li>[<b>runner</b>] появился метод <b>replicate</b>, который копирует на GP результаты расчетов на YT</li>
<li>[<b>queries</b>] в расчет <b>agg_management_reporting</b> добавлены новые метрики</li>
<li>[<b>util</b>] <b>preprocess</b> научился прининмать аргументы для <b>get_sample</b></li>
<li>[<b>util</b>] <b>get_logger</b> (а вместе с ним и все объекты графа) научились принимать вместо файла поток вывода</li>
<li>[<b>cron.budegt</b>] в бюджете перешли при чтении данных на <b>DataManager</b> + избавились от старых <b>budget_metrics</b></li>
<li>[<b>queries.queries_config</b>]: Переписаны источники с <b>user_session</b> на <b>demand_session</b></li>
<li>[<b>queries.yql_src</b>]: Переписаны запросы для корректной работы с <b>demand_session</b></li>
<li>[<b>all</b>]:  Перешли с <b>sessions_with_wait</b> на <b>sessions_wo_geo_break</b></li>
<li>[<b>graph.configurator</b>]: Добавлен флаг <b>clear_logs.</b> Если <b>True</b>, то в начале работы чистятся логи</li>
<li>[<b>tests.graph_forecast_tests</b>]: Добавлен аргумент <b>new_base</b>, позволяющий дать путь, в котором уже лежат необходимые файлы</li>
<li>[<b>accuracy.score</b>]: Исправлена ошибка, возникающая при обучении модели на многих <b>date_to</b></li>
<li>[<b>series_models.series_models</b>] Убраны ворнинги про замену когортой матрицы</li>
<li><b>yql</b>: убрали вычислене <b>sessions_with_wait_wo_geo_break</b></li>
    </ul>
</details>
</br>


<details>
<summary><u>Версия 2.0.6.1</u></summary>
    <ul>

    </ul>
</details>
</br>


<details>
<summary><u>Версия 2.0.6</u></summary>
    <ul>
    <li><b>databases.gdocs</b>: добавили методы <b>add_table</b>, <b>delete_table</b>  для создания и удаление листов в гуглодоке</li>
<li><b>plot</b>: Исправлена ошибка с <b>unicode</b> в <b>plot</b></li>
<li><b>config_holder</b>: не кидаются <b>warnings</b> при отсутствии ключей в конфиге</li>
<li><b>models</b>: приведения <b>SeriesModel</b> к общему интерфейсу нужно</li>
<li><b>graph.configurator</b>: изменился <b>output</b> метода <b>configurator.validate</b>(): теперь возвращаются в том числе и исходные данные, по которым считаются ошибки</li>
<li><b>queries</b>: добавлен <b>get_reversed_method</b>, которые для метода <b>Reader</b> возвращает обратный метод из <b>Runner</b> (и наоборот)</li>
    </ul>
</details>
</br>



<details>
<summary><u>Версия 2.0.5</u></summary>
    <ul>
    <li>[<b>graph</b>] все, что было в <b>cron</b>/<b>graph_forecast</b> перенесено в библиотеку</li>
<li>[<b>queries</b>] метод <b>runner.drop_dimensions_wo_last_flg</b> для удаления измерений без актуальных данных</li>
<li>[<b>util.dates</b>] Добавился флаг <b>to_str</b> в метод <b>to_start</b></li>
<li>[<b>startrek</b>] Добавлен <b>retry</b> при прикладывании файлов</li>
<li>Добавлен <b>retry</b> для комментариев</li>
<li><b>util</b>: <b>bugfix</b> в <b>Handler</b>:  не падает при форматировании сообщения об ошибки с <b>ascii</b> <b>coding</b> ошибками</li>
    </ul>
</details>
</br>


<details>
<summary><u>Версия 2.0.4</u></summary>
    <ul>
    <li>[<b>graph</b>] все, что было в <b>cron</b>/<b>graph_forecast</b> перенесено в библиотеку</li>
    </ul>
</details>
</br>


<details>
<summary><u>Версия 2.0.3</u></summary>
    <ul>
    <li><b>queries</b>: добавлена таблица со скорингом</li>
<li><b>queries.runner</b>: функция для дропа <b>region_id</b> <b>Unknown</b> из <b>planning</b> таблиц</li>
<li><b>queries</b>: Поправили скрипты заливки <b>forecast</b> и <b>fact</b>, чтобы инкремент корректно джойнился по <b>region_id</b></li>
<li>[<b>models</b>] исправлена документация к <b>LinearSeriesModel</b></li>
<li><b>greenplum</b>: <b>write_table</b> не разваливается на py3</li>
<li><b>hahn</b>: <b>syntax_version</b>=1 по дефолту</li>
    </ul>
</details>
</br>


<details>
<summary><u>Версия 2.0.2</u></summary>
    <ul>
    <li><b>queries</b>: добавлена таблица со скорингом</li>
<li><b>queries.runner</b>: функция для дропа <b>region_id</b> <b>Unknown</b> из <b>planning</b> таблиц</li>
    </ul>
</details>
</br>


<details>
<summary><u>Версия 2.0.1.3</u></summary>
    <ul>
    <li><b>databases.gdocs_auth</b>: фикс с записью незаполненных колонок и конвертацией в <b>datetime</b></li>
    </ul>
</details>
</br>


<details>
<summary><u>Версия 2.0.1.2</u></summary>
    <ul>
    <li><b>hahn</b>: <b>bugfix</b> поправили ошибку с <b>AttributeErorr</b> при попытке проставить <b>hahn.base_path</b></li>
    </ul>
</details>
</br>


<details>
<summary><u>Версия 2.0.1.1</u></summary>
    <ul>
    <li>[<b>greenplum</b>] (<b>bugfix</b>) <b>replicate</b> передавал <b>engine</b> в <b>write</b></li>
<li><b>greenplum</b>: починили ошибку в <b>grant</b> в конце <b>write_table</b></li>
    </ul>
</details>
</br>


<details>
<summary><u>Версия 2.0.1</u></summary>
    <ul>
    <li>Добавили <b>sys.path.append</b>, чтобы импорты зарабтали</li>
<li>[<b>queries</b>] (<b>bugfix</b>) Исправлен запрос с расчетом <b>group_cohorts.</b> Теперь параметры <b>metrics</b> и <b>gropped_metrics</b> передаются как списки</li>
<li><b>queries</b>: больше информации в  тесте <b>unknown_region_ids</b></li>
<li><b>queries</b>: багфикс в <b>runner._get_simple_cohorts_parameters</b></li>
<li><b>queries</b>: <b>syntax_version</b>=1 во всем <b>queries</b></li>
<li><b>queries</b>: возможность кастомных <b>start_part</b> для групп запросов</li>
<li><b>databases</b>: новый базовый класс</li>
<li><b>hahn</b>: перешел на <b>databases</b> без изменения интерфейса</li>
<li><b>greenplum</b>: перешел на <b>databases</b> без изменения интерфейса</li>
<li><b>g_docs</b> перешел на <b>databases</b> без изменения интерфейса</li>
<li><b>basic</b>: <b>zip_with_defaults</b>  научился выравниваться по самому длинному генератору</li>
<li><b>model</b>: везде теперь <b>dimensions</b> по дефолту <b>region_id</b>+<b>region</b></li>
<li><b>greenplum</b>: починили <b>drop</b></li>
<li><b>hahn</b>: внутри <b>__call__</b> вызывается <b>read</b>, а не <b>load_result</b></li>
<li><b>curve</b>: новая P<b>ower</b>C<b>urve</b></li>
<li>[<b>queries</b>] фикс неправильно обновлявшихся аргументов <b>databases.__call__</b></li>
<li><b>databases.mongo</b>: изоляция импортов</li>
    </ul>
</details>
</br>

<details>
<summary><u>Версия 2.0.0</u></summary>
   <ul>
   <li>[hahn] Вызов <b>hahn()</b> получил флаг return_shared_url. Если он True, то вместе с резульататми возвращается shared_url YQL операции/li>
   <li><b>Совместимость с python3</b> Альфа версия совместимости с python3. Тестировалось с python3.6. Частично проверялось на python 3.5 и  3.7 </li>
   </ul>
</details>

</br>
<details>
<summary><u>Версия 1.4.8</u></summary>
    <ul>
    <li>[model] В <b>ElasticityModel</b> теперь правильно фильтруются полные недели при подсчете недельной сезонности</li>
    <li>[queries] фикс в yql restore_last_flg</li>
    <li>[models] <b>ClusterModel</b> кидает исключение, если <b>ndots_predict</b> и зафитченные данные не соответствуют данным в <b>forecast</b>
</li>
    <li>[queries] <b>Runner.read_parameter</b> читает только те, колонки, которые нужны</li>
    <li>[hahn] получил атрибут <b>enable_read_parallel</b>, который пробрасывается в <b>load_result</b></li>
    <li>[util] <b>Taskmanager</b> собирает <b>exit_code</b> процессов и может выбрасывать исключения наверх</li>
    <li>[queries.runner] <b>sub_path</b> правильно пробрасывается в <b>Runner.recount_metrics_gp</b></li>
    <li>[queries.queries_config] Ограничения на длину имени таблицы в <b>greenplum</b></li>
    <li>[models] Методы <b>combine_parts</b> передают вглубь <b>date_to</b>, <b>scale</b> и <b>ndots_predict</b></li>
    <li>[models] В метод <b>combine_parts</b> для <b>ActivityCohortModel</b> и <b>TruncatedCohortModel</b> добавлен аргумент <b>with_group</b>, который суммирует когортные данные</li>
    <li>[models] У <b>EvalModel</b> переопределен метод get_filter_date_to</li>
    <li>[queries] <b>Reader.read_table_by_path</b> с аргументом <b>validate_name=True</b>, умеет искать <b>path</b> среди имен таблиц в конфиге</li>
    <li>[queries] (bugfix) <b>Reader.read_versions</b> поддерживает чтение с <b>sub_path</b></li>
    <li>[queries] <b>Reader.read_retention</b> поддерживает чтение новичков извне, а не вычисление их по когортным данным</li>
    <li>[queries] <b>Runner.upload_fact</b> поддерживает в качестве <b>value_name</b> произвольное выражение над колонками в данных</li>
    <li>[queries] (bugfix) <b>Runner.write_plan</b> корректно обрабатывает данные без <b>region_id</b></li>
    <li>[util] Функция <b>send_mail</b> импортируется до основного <b>init</b></li>
    <li>[util.dataframes] Функция <b>preprocess</b> получила аргумент <b>evals</b>, который производит произвольное вычисление над колонками считанных данных</li>

    </ul>
</details>
</br>
<details>
<summary><u>Версия 1.4.7</u></summary>
    <ul>
    <li>[queries] в <b>set_prefix</b> у префикса делается lstrip('/')</li>
<li>[queries] в часовых точках было обрезание по utc, стало обрезание по <b>local</b></li>
<li>[queries] исправлен баг в <b>validate_sub_path</b></li>
<li>[queries] в методы чтения <b>reader</b> добавлен флаг <b>ignore_empty</b></li>
    </ul>
</details>
</br>
<details>
<summary><u>Версия 1.4.6 (версия содержит критические баги)</u></summary>
    <ul>
    <li>[greenplum]: автокоммит по умолчанию</li>
<li>[model]: Поддержано рекурсивное сохранение всех промежуточных моделей в методе <b>save</b></li>
<li>[models](bugfix): замена захардкоженных названий колонок demand, supply, <b>trips</b> на аргументы метода</li>
<li>[queries]: в рассчете часовых точек по deman, supply, <b>trips</b> используется локальное время</li>
<li>[queries]: в группу запросов <b>planning</b> добавлены источники <b>user_info</b> и <b>cannibalization</b></li>
<li>[queries]: в группу запросов <b>planning</b> добавлен новый параметр filter, который позволяет префильтровывать входную таблицу</li>
<li>[queries.runner](bugfix): write_table, <b>write_plan</b> и <b>write_forecast</b> больше не игнорируют <b>sub_path</b></li>
<li>[queries]: запрос <b>app_cannibalization</b> добавляет в таблицу <b>region_id</b></li>
<li>[queries](bugfix): запрос для загрузки плана корректно обрабатывает <b>null</b> в <b>region_id</b></li>
<li>[models]: <b>Model</b> теперь корректно распикливается в составных моделях</li>
<li>[queries](bugfix): в расчете cohorts/hierarchy снова можно передавать пересекающиеся регионы</li>
<li>[queries]: <b>runner.get_small_forecast_input</b> - копирует данные для тестирования графа</li>
    </ul>
</details>
</br>
<details>
<summary>Версия 1.4.5</summary>
<li>[cron.graph_forecast] В конфигураторе поправили дефолтный путь</li>
<li>[models] Model.save теперь кидает внятное исключение, путь клеиться правильным методом</li>
<li>[queries](bugifx) sub_path passed теперь передается в write_forecast</li>
<li>[queries](bugfix) Поправили загрузку нескольких параметров</li>
<li>[queries](bugfix) Поправили загрузку нескольких параметров</li>
<li>[queries](bugifx) Пофикшен  agg_management_metrics.sql</li>
</details>
</br>
<details>
<summary>Версия 1.4.4</summary>
<li>[queries] Новая версия queries</li>
<li>[curves] CurveFitter может в качестве x0 и bounds принимать функции для их вычисления на данных</li>
</details>
</br>
<details>
<summary>Версия 1.4.3</summary>
<li>[queries] Пофикшены баги  metrics/hourly и tests/regions</li>
<li>[score] model.__params__ заменены на model.external_parameters</li>
<li>[accuracy] rsquared_adjusted получил дефолтный параметр для единообразия с остальными</li>
</details>
</br>
<details>
<summary>Версия 1.4.2</summary>(версия содержит баги)
<li> [hahn](bugfix) <b>load_result</b> При чтении по чанкам теперь гарантируется уникальность числового индекса </li>
<li> [greenplum] документация методов снова доступна (декоратор initialize обернут в wraps) </li>
<li> [greenplum] В <b>replicate</b> можно в явном виде передавать типы </li>
<li> [hahn], [greenplum] пербор в том числе secidst в поисках токенов </li>
<li> [config_holder] изменили дефолтное место с yaml конфигом </li>
<li> [gdocs_helper] можно прокинуть в метод config_holder, который будет из недр yaml конфига тащить токены </li>
<li> [models] <b>ClusterModel</b>  модель умеющая предсказывать кластера отдельно: моделями или долями от других </li>
<li> [models](bugfix) <b>ClusterModel</b> теперь правильно фильтрует данные, если передано date_to </li>
<li> [queries] Поправили aggregate_by_regions_forecast.yql под новую таблицу с иерархией </li>
<li> [queries] запрос для очистки forecast таблицы от старых load_date </li>
<li> [queries] метод для валидации planning/* таблиц </li>
<li> [queries] доабвила data_check.yql для проверки чека дат и тарифных зон </li>
<li> [queries] метод для валидации planning/* таблиц </li>
<li> [queries] запрос для очистки forecast таблицы от старых load_date </li>
</details>
</br>
<details>
<summary>Версия 1.4.1.1</summary>
пофикшен setup
</details>
</br>
<details>
<summary><u>Версия 1.4.1</u></summary>
<ul>
<li> (bugfix) [botolib] <b>Bot</b> починили непередававшийся дефолтный chat_id в send_message </li>
<li> [hahn] <b>hahn()</b> умеет запускать запросы в режиме валидации (флаг validation_mode) </li>
<li> [util] log <b>Handler</b> исправлена опечатка в параметре конструктора notify_sucCess. Старый параметр продолжит тоже обрабатываться корректно</li>
<li> [util] Новая функция <b>monitor_difference_frames</b> - проверяет идентичность числовых данных в датафрейме + выводит ошибки</li>
<li> [queries] Функция для сравнения диффа таблиц по индексу <b>compare_tables</b></li>
<li> [queries] функция для отката last_flg в planning таблицах <b>restore_last_flag</b></li>
<li> [queries] Добавлен новый тип запросов <b>tests</b> + метод run_test, который их вызывает (проверяет дубли в planning таблице)</li>
<li> [queries] Переделан метод <b>upload_plan</b> (теперь он аналогичен upload_forecast)</li>
<li> [models] В AnomalyCorrector.<b>get_sos_metrics</b> пофиксили баг с неправильным вычислением длины прогноза</li>
<li> [models] ElasticityModel.  <b>_fit_week_split</b> - список городов считается до фильтрации</li>
<li> [models] seasonality.holiday_season. <b>get_smoothing_value</b> можно использовать разные размеры окна для разных дат, оптимизировано вычисление</li>
<li> [convert] Все конвертеры могут принимать в value_types None, вместо указания дефолтной формулы</li>
</ul>
</details>
</br>
<details>
<summary><u>Версия 1.4.0.1</u></summary>

Доехало то, что не доехало в 1.4.0.1

</details>
</br>
<details>
<summary><u>Версия 1.4.0.1</u></summary>
<ul>
<li> (bugfix) util.log поправлена коллизия имн с get_logger</li>
<li> (bugfix) queries удалили hiring и актуализировали newbie</li>
</ul>
</details>
</br>
<details>
<summary><u>Версия 1.4.0</u></summary>
<ul>
<li> (breaking) botolib.<b>Bot</b>  у Bot оторвано deprecated поведение, когда в функции send_* первым обязательным аргументом передавался chat_id. Теперь chat_id по дефолту берется из внутренних переменных бота. Если вы передавали неименованные аргументы в методы send_* первый аргумент начнет интерпретироваться как посылаемый объект
<li> (breaking) startreck Переименован файлик startr(A->E)ck.py
<li>  hahn.<b>HahnDataLoader</b> У hahn все функции про бэкапы можно запускать в verbose режиме, когда в лог пишуться все действия. А так же dry_run режим, когда ничего не делается, а только в лог выводится что куда перемещается </li>
<li> greenplum.<b>GreenplumManager</b> Можно выдавать права сразу в replicate. Обновили скрипты с примером</li>
<li> util.basic.<b>Factory</b>  Factory умеет искать детей сразу нескольких базовых классов
<li> (breaking) models.<b>Model</b>  у Model оторваны deprecated методы __main_params__, __params__, load_json, __drop_params__, fit_incity, _prepare_data </li>
<li> (breaking) <b>converter</b> Большой рефакторинг конвертеров. Упрощен интерфейс Converter, values структурно поменялись + dimensions* заменились на index. См пример в README </li>
<li> (breaking) model.<b>MultipleConfigs</b> Большой рефакторинг MultipleConfigs. Тип модели перенесен в параметры,  newbie теперь нет, изменился формат prediction_model_configs, дефолтная модель применяется ко всем измерениям, которые не указаны</li>
<li> (breaking) models.<b>outliers</b>QuantileOutliers изменил интерфейс, StandardDeviationOutliers больше не отбрасывает значения по оси y, которые больше 1.5, новый метод MultipleOutliers, применяет подряд сразу несколько методов отбрасывания выбросов</li>
</ul>
</details>
</br>
<details>
<summary><u>Версия 1.3.54</u></summary>
    <ul>
    <li><b>util:</b> <b>Factory</b> умеет получать типы и объекты из указанной библиотеки</li>
<li>(bugfix) <b>models.anomaly:</b> в <b>AnomalyCorrector</b> там, где не хватает фактических данных, дополняем прогнозом</li>
<li><b>models.anomaly:</b> в <b>AnomalyCorrector</b> можно считать несколько сдвигов по <b>YoY</b> (например, в текущей неделе видеть <b>YoY</b> прошлой)</li>
<li><b>models.anomaly:</b> много доработок по имеющимся правилам, добавилось правило <b>AnyMetricYoYChanges</b> (смотрит на плавность падения YoY)</li>
<li><b>models:</b> появился MultiSeriesModelWrapper, который заворачивает в себя несколько объектов SeriesModels, для разных срезов</li>
<li><b>models.series_models:</b> добавилась новая модель LinearModel(линейная регрессия)</li>
<li><b>models.series_models:</b> <b>YoYSlowdownModel</b> теперь может ограничиваться в росте сверху и снизу</li>
<li><b>startrack:</b> <b>StartreckWrapper.get_attachments</b> может возвращать объекты из <b>Startreck</b></li>
<li><b>gdocs_helper:</b> в метод загрузки таблиц в гуглдоки добавлен флаг <b>with_drop</b></li>
<li><b>util.log:</b> <b>Handler</b> научился отправлять логи на почту и в телеграм</li>
<li><b>hahn:</b> добавлены функции для  <b>ls</b> в папке и работы с бэкапами ls_folder, backup, backup_cleanup, <b>restore_from_backup.</b> С ними пример в <b>common_scripts</b> см. ссылку в <b>readme.md</b></li>
<li><b>util.databases:</b> Функция get_outdated_tables, которая ищет все старые таблички в выбранной директории</li>
<li><b>util.basic:</b> Функция <b>flatten_dict</b> делает из <b>nested_dict</b> одноуровневый</li>
<li>(bugfix) <b>models:</b> в <b>ElasticityModel</b> снова работает предсказание с use_separate_splitting=True</li>
<li><b>greenplum:</b> новый метод replicate_dwh, быстрее перекладывающий большие таблицы</li>
<li><b>util:</b> в декоратор <b>retry</b> добавлена возможность инкрементировать один из аргументов функции</li>
<li><b>models.cluster:</b> классы для разбиения данных на кластеры <b>Cluster</b> (базовый) и <b>FilterCluster</b> (разбивает в зависимости от значений в каждой отдельной строке)</li>
<li><b>models:</b> в <b>ElasticityModel</b> можно добавить к часовым точкам еще и дневные во время <b>fit</b></li>
<li>(bugfix) <b>retention:</b> В <b>IncrementalRetention</b> исправлен баг, из-за которого неправильно рассчитывались продолжения когорт в <b>Cohort</b></li>
<li><b>cohorts:</b> для расширения значений когортной матрицы больше не обязательны параметры <b>cohort_len</b> и <b>ndots_fit</b></li>
<li><b>util:</b> метод <b>to_file</b> заменен на <b>data_to_file.</b> Оба метода data_to_file, <b>data_from_file</b> вынесены из <b>dataframes</b> в basic, и поддерживают любые типы данных</li>
    </ul>
</details>
</br>
<details>
<summary><u>Версия 1.3.53</u></summary>
<ul>
<li>(bugfix) databases.<b>ClickHouseClient</b> не падает при записи пустого датафрейма в таблицу, корректно работает с таблицами, в имени которых передан префиксом  database</li>
<li>(bugfix) hahn.<b>HahnDataLoader</b> и greenplum.<GreenplumManager> (bugfix) Пофиксили падение из-за добавления лишней ; в конец запроса</li>
<li>В util.<b>dataframes</b> добавились полезные функции для проверки датафреймов, series и диктов с ними на произвольные условия. См test_pandas, test_dict</li>
<li>models.series_models.<b>NonLinearModel</b> теперь по умолчанию фитит неубывающую кривую</li>
<li>models.anomaly.<b>AnomalyCorrector</b> научился работать со списком исключений</li>
<li>queries Добавили расчет когорт по первому городу для всего сервиса и отдельно яндекса, расчет миграций для всего сервиса.</li>
</ul>
</details>
</br>
<details>
<summary><u>Версия 1.3.52</u></summary>
<ul>
<li>hahn.<b>HahnDataloader</b> научился читать и запускать запросы из файлов</li>
<li>greenplum.<b>GreenplumManager</b> научился читать и запускать запросы из файлов</li>
<li>(bugfix) databases.<b>ClickHouseClient</b> теперь правильно читает имена колонок датафрейма</li>
<li><b>setup</b> поставили правильные версии colorama и pandas</li>
<li>models.series_models.<b>CopyModel</b> новая модель: вставляет в будущее те же значения, что в прошлом со сдвигом на год и сглаживает переходы</li>
<li>models.series_models.<b>YoYSlowdownModel</b> новая модель: предсказывает по YoY значениеям, с затуханием  роста</li>
</ul>
</details>
</br>
<details>
<summary><u>Версия 1.3.51</u></summary>
<ul>
<li>databases.<b>ClickHouseClient</b> клиент для выполнения запросов к кликхаусу(обертка над вызовом консольного клиента). В databases.<b>transfer_functions</b> добавились функции копирования CH<->YT
<li>(bugfix)hahn.<b>HahnDataloader</b> Поправили баг с неправильно передававшимся syntax_version для yql
<li>util.<b>drop_quantiles</b> Появилась функция, дропающая из датафреймов выбросы
<li>cohort.<b>Cohort</b> научился продлевать ретеншеном когорты вперед на любую длину и по этому считать ltv в том числе
<li>Обновили setup скрипт, теперь он должен протягивать все-все зависимости нашей либы, и, в идеале, ее можно хоть себе на ноут ставить через pip
<li>util.<b>diff_scales</b> может работать с pd.Series
<li>models.<b>AnomalyCorrector</b> Добавили AnomalyCorrector -- объект, умеющий исправлять аномалии в прогнозах, сравнивая факт и прогноз. К ней прилагается набор AnomalyRule -- правил поиска типов аномалий
<li>models.<b>ShiftModel</b> модель корректирует прогноз по уже сбывшейся части
</ul>
</details>
</br>
<details>
<summary><u>Версия 1.3.50</u></summary>
<ul>
<li>hahn.<b>HahnDataloader</b> в __call__ принимает аргументы files и urls, которые аттачат к запросу соответстветственно файл или файл по урлу.</li>
<li>В greenplum объекте connection по дефолту создается не в конструкторе, а при первом вызове какого-нибудь метода. Сильная экономия на времени импорта библиотеки в целом.</li>
<li>В common_scripts добавлен пример расширенный пример работы ScaleConverter (<a href="https://github.yandex-team.ru/rotax/business_models/blob/master/common_scripts/scale_converter_example.ipynb">Пример конвертации скейлов</a>)</li>
<li>В модуль <b>plot</b> добавлены переменые с корпоротивными цветами Яндекса (YANDEX_BLUE, YANDEX_YELLOW, YANDEX_RED)</li>
</ul>
</details>
</br>
<details>
<summary><u>Версия 1.3.49</u></summary>
<ul>
<li>(bugfix)В util.basic.<b>sendmail</b> починили баг с импортами</li>
<li>queries.<b>runner</b> теперь поддерживает обе версии yql. Вся зависимая от версий логика уехала в start_part, который существует в двух версия _v0 и _v1. Сейчас по дефолту подставляется версия 0. Первая включается при передаче run_yql_query `hahn_kwargs={"syntax_version": 1}`</li>
<li>Появилась startrack.<b>Startrack</b> -- обертка над клиентом StartTrack. С ней пример в common_scripts.<b>Startrack example.ipynb</b></li>
<li>hahn.<b>HahnDataloader</b> теперь умеет принимать в __call__ `query_kwargs`, которые пробросятся в `yql.client.query` и `request_kwargs`, которые пробросятся в `request.run`</li>
<li>botolib.<b>bot</b> теперь умеет в конструкторе получать  `default_chat_id`, так что параметр `chat` в методах send_* становится опциональным. Добавили врапперы над всеми методами, чтобы обеспечить обратную совместимость всем, кто передавал в методы неименованный список переменных.
Если вы используете `from botolib import bot`, то ему уже подставлен дефолтный чат `my_telegram_chat` из конфига</li>
<li>queries.<b>reader</b> добавлена возможность читать несколько параметров в одном запросе через read_raw_parameter. Так же доабавятся доверительные интервалы, если они есть и region_id</li>
<li>Появилась util.dataframes.<b>dataframes_close</b> -- функция для сравнения датафреймов с нечетким равенством численных колонок(через np.isclose)  </li>
<li>util.taskmanager.<b>TaskManager</b>  теперь умеет работать с генераторами kwarg</li>
<li>Появился common_scripts.<b>hahn_module_example.ipynb</b> -- ноутбук с примерами на <b>HahnDataLoader</b></li>
<li>(bugfix)В models.seasonality.<b>CohortSeasonality</b> починили исключение про broadcast</li>
<li>В models.<b>YoYForecastModel</b> ускорен forecast</li>
<li>converter.<b>HierarchyConverter</b> оптимизирован, снабжен документацией и в нем появилась возможность получать разбиение на базовые регионы из любого набора region_id</li>
<li>Появилась models.<b>TruncatedCohortModel</b>, которая делает базовый прогноз когортной моделью, выделяет ядро
и предсказывает его отдельно, а потом размазывает прогноз ядра по исходному когортному прогнозу </li>
<li>Появилась models.<b>ActivityCohortModel</b>, которая разделяет активность и головы, предсказывает их отдельно, а потом склеивает в общий прогноз</li>
<li>В models.series_models.<b>NonLinearModel</b> появился флаг, форсящий неубывание подобранной функции</li>
</ul>
</details>
</br>
<details>
<summary><u>Версия 1.3.48</u></summary>
<ul>
<li>(bugfix) Из models удален SplitCityModel, который рушил библиотеку на этапе импорта</li>
</ul>
</details>
</br>
<details>
<summary><u>Версия 1.3.47 (версия содержит критический баг)</u></summary>
    <ul>
    <li>(bugfix) В <b>get_str_date</b> исправлен баг с именованием переменных, из-за которого функция не работала</li>
<li><b>simple_cohorts</b> теперь возвращают путь к созданным таблицам, с помощью аргумента read_table=True можно вернуть созданную таблицу</li>
<li>(bugfix) В <b>BruteForceStrategies</b> исправлен баг, не позволявший вызвать <b>start</b> у только что созданного объекта</li>
<li>Появилась функция <b>run_yql</b> + в <b>queries</b> стали до самого конца пробрасываться <b>hahn_kwargs</b></li>
<li>Новый класс <b>ImportIsolation</b> + под него немного переделан <b>Handler</b></li>
<li>Изолирована большая часть зависимостей в библиотеке, подробности в TAXIANALYTICS-6070</li>
<li><b>GLMModel</b> переименована в GLMCohortModel, вместо нее теперь создана более общая модель</li>
<li>Базовый функционал <b>botolib</b> въехал в библиотеку</li>
<li><b>send_mail</b> въехал в библиотеку</li>
<li><b>change_coding</b> работает также со строками и любыми кодировками</li>
    </ul>
</details>
</br>
<details>
<summary><u>Версия 1.3.46</u></summary>
    <ul>
    <li>Классы в <b>optimize</b> получили возможность делать <b>truncate_to</b></li>
<li>(bugfix) <b>BruteForceStrategies.get_strategy_generator</b> корректно обрабатывает директории</li>
<li>Из основного <b>__init__</b> был собран отдельный модуль <b>utils</b></li>
<li>Глобальные переменные <b>POPULATION_SCOPES</b> и <b>scopes</b> удалены</li>
<li>В <b>HierarchyConverter</b> разбивка параметров теперь основана на <b>agg_management_report</b></li>
<li>В <b>HierarchyConverter</b> можно задать иерархию, которая используется</li>
<li>В <b>CohortModel</b> можно не передавать новых пользователей (или передавать константу)</li>
<li>Появилась новая модель <b>YoyForecastModel</b> , которая вычисляет прогноз по соотношениям год к году</li>
<li>В <b>plot.series_data</b> и <b>plot.frame_data</b> можно передавать <b>kwargs</b> для отрисовки</li>
<li>Внутри библиотеки больше не используются <b>Model.__main_params__</b> и <b>Model.__params__</b></li>
<li>Появился класс <b>ConfigHolder</b> для работы с токенами</li>
<li>В <b>optimize</b> появилось несколько новых методов отбрасывания стратегий, подробнее в тикете TAXIANALYTICS-5955</li>
<li>Из <b>mylib</b> скопированы функции <b>clickhouse_query</b> и <b>get_mongo_df</b> , а также константы <b>CONNECTIONS</b> и <b>MONGO_DATABASES</b></li>
<li><b>BruteForceStrategies</b> научилась сохраняться после каждой итерации и продолжать выполнение после остановки</li>
<li>Глобальный рефакторинг <b>hahn</b> : ушли от зависимости от nile, в <b>call</b> читабельные аргументы, возможность перезаписывать таблицу или аппендить через write_table, возможность не передавать туда <b>types</b></li>
<li>(bugfix) <b>QuantileOutliers</b> строгое неравенство исправлено на нестрогое</li>
<li><b>gdocs_helper</b> при первой авторизации будет отдавать ссылку, по которой нужно перейти, а не перекидывать на нее</li>
<li>В <b>simple_cohorts</b> доступен расчет когорт по неуникальным пользователям (в каждом городе/измерении новичок)</li>
    </ul>
</details>
</br>
<details>
<summary><u>Версия 1.3.45</u></summary>
    <ul>
    <li>Новая модель работы с выбросами: <b>QuantileOutliers</b></li>
<li><b>to_start</b> теперь работает и с векторами тоже</li>
<li>В <b>HALFMILLIONS</b> добавлены названия городов без "+"</li>
<li>В <b>planning</b> добавлены отрисовки графиков <b>YoY</b></li>
<li><b>BruteForceStrategies</b> научился считываться из нескольких файлов</li>
<li>(bugfix) В <b>ElasticityModel</b> исправлен критический баг при расчете эластичности (drop_duplicates)</li>
<li>В <b>GreenPlum</b> появился метод <b>dump</b> (загрузка <b>GP</b> -> <b>YT</b>)</li>
    </ul>
</details>
</br>
<details>
<summary><u>Версия 1.3.44</u></summary>
    <ul>
    <li>Исправлен баг в модели <b>NPreviousScaleMigration</b>: неправильно вычислялась последняя точка факта </li>
    <li>В <b>greenplum</b> добавлена возможность передать <i>user</i> и <i>token</i>, из под которых следует запустить запрос</li>
    <li>Добавлен новый тип кривой <b>DoubleLinearCurve</b> в models.curves </li>
    <li>В <b>hahn</b> и <b>greenplum</b> добавлены предупреждения, когда отсутсвует mylib_config.json</li>
    </ul>
</details>
</br>
<details>
<summary><u>Версия 1.3.43</u></summary>
    <ul>
    <li>(bugfix) в <b>ScaleConverter</b> исправлен баг из-за которого нужно было обязательно передавать и <b>additive</b> и non-additive метрики (иначе все падало)</li>
<li>В рамках тикета <a href=https://st.yandex-team.ru/TAXIANALYTICS-5585>TAXIANALYTICS-5585</a> внесен ряд изменений в модуль <b>optimize</b> (в этой версии он уже полностью работоспособен)</li>
<li><b>TaskManager</b> научился делать перерыв между запусками процессов: <b>sleep_time</b></li>
<li>В <b>plot_many_bars</b> добавлен параметр <b>show_flg</b></li>
<li>Добавлен список <b>HALFMILLIONS</b> - в нем список городов с населением 500К+ (осторожно, там есть города вида "Махачкала + Каспийск", в этом случае город "Махачкала" отсутствует)</li>
<li>В список <b>MILLIONS</b> добавлены города Новосибирск, Нижний Новгород, Волгоград (раньше они были только вместе с "+ др.город")</li>
<li>В классе <b>Greenplum</b> добавлен метод <b>grant</b> - он позволяет дать доступ к таблице. В методы <b>replicate</b> и <b>write_table</b> добавлен соответствующий флаг <b>with_grant</b></li>
<li>В <b>ConfidenceInterval</b> добавлена обработка специфических дат (таких как новогодняя неделя, майские и т.п.)</li>
<li>(bugfix) в <b>split_scale</b> исправлен баг с индексированием разделяемых данных</li>
<li>В <b>MultipleConfigsModel</b> добавлена возможность использования дефолтного конфига для городов, которые не упоминаются ни в одном другом конфиге</li>
<li>(bugfix) в <b>plot.series_data</b> раньше для <b>shift</b> использовался просто slice, перешли на <b>iloc.</b> Это критично, потому что провоцировало ошибки, если индекс является числом</li>
<li>(bugfix) в <b>Trainer</b> выпилили захардкоженные куски, где использовалось 'week' вместо <b>scale</b></li>
    </ul>
</details>
</br>
<details>
<summary><u>Версия 1.3.42</u></summary>
    <ul>
    <li><b>simple_cohorts</b> исправлен баг с регистром as/AS</li>
    <li>Доверительные интервалы группируются по скейлу (раньше по последней точке факта)</li>
    <li>В <b>read_score_parameters</b> 500k+ города теперь не группируются, а рассматриваются индивидуально</li>
    <li>В <b>Trainer</b> появилась возможность получения DataFrame из всех возможных конфигов c результатами их скоринга</li>
    <li>Обработка исключений в <b>TaskManager</b></li>
    <li>Реализация алгоритмов космолета TAXIANALYTICS-5585</li>
    </ul>
</details>
</br>
<details>
<summary><u>Версия 1.3.41</u></summary>
    <ul>
    <li><b>Model</b> теперь можно сохранить в pickle</li>
    <li><b>CohortModel</b> не падает и возвращает пустой датафрейм, когда входные данный оказываются пустыми после фильтрации</li>
    <li><b>ElasticityModel</b> predicted_values is property</li>
    <li><b>ElasticityModel</b> фикс бага при использовании месячного скейла (правка)</li>
    <li>Реализация алгоритмов космолета TAXIANALYTICS-5585</li>
    </ul>
</details>
</br>
<details>
<summary><u>Версия 1.3.40 (версия содержит критические баги)</u></summary>
    <ul>
    <li>Фикс бага в shift_date, когда date не итерируемая переменная</li>
    </ul>
</details>
</br>
<details>
<summary><u>Версия 1.3.39 (версия содержит критические баги)</u></summary>
    <ul>
    <li><b>Model</b> фикс бага, когда date_to не None</li>
    <li>Добавлен новый тип сезонности <b>ClusterSeasonality</b>, который может сглаживать и кластеризовать сезонности, полученные для городов индивидуально другими методами</li>
    <li>Добавлен модуль <b>gdocs_helper</b> для работы с Google Sheets</li>
    <li><b>ElasticityModel</b> фикс бага при использовании месячного скейла</li>
    <li>Реализация алгоритмов космолета TAXIANALYTICS-5585</li>
    </ul>
</details>
</br>
<details>
<summary><u>Версия 1.3.38</u></summary>
    <ul>
    <li>Появились функции для работы с гуглдоками: <b>gdocs_helper</b> (подробнее про них, смотрите в примере использования)</li>
<li>(bugfix) исправлен критический баг: <b>Model</b> игнорировала параметр <b>ndots_fit</b></li>
<li>(bugfix) <b>CohortModel</b> теперь не падает, если в <b>newbie</b> переданы лишние столбцы</li>
<li>в функция для считаывания резуьтатов скоринга вынесена из <b>ConfidenceInterval</b> в <b>reader.read_score_parameters</b></li>
<li>сам класс <b>ConfidenceInterval</b> был сильно упрощен</li>
<li>произошло упрощение объекта <b>optimize.properties.CohortProperties</b> (который изначально был скопирован из planning.properties.PlanObjectProperties)</li>
    </ul>
</details>
</br>
<details>
<summary><u>Версия 1.3.37</u></summary>
    <ul>
    <li>Попытка исправить баг в <b>shift_date</b> #2. Финальная</li>
    </ul>
</details>
</br>
<details>
<summary><u>Версия 1.3.36 (версия содержит критические баги)</u></summary>
    <ul>
    <li>Добавлен модуль <b>confidence_interval</b> для работы с доверительными интервалами</li>
<li>Попытка исправить баг в <b>shift_date</b> #1</li>
    </ul>
</details>
</br>
<details>
<summary><u>Версия 1.3.35 (версия содержит критические баги)</u></summary>
    <ul>
    <li>Исправлен досадный баг связанный с неймингом, из-за которого не работала оконная сезонность: max_diff использовался в нескольких функциях</li>
<li>В <b>queries_config</b> из custom_regions удалена удаленная из иерархии вершина</li>
    </ul>
</details>
</br>
<details>
<summary><u>Версия 1.3.34 (версия содержит критические баги)</u></summary>
    <ul>
    <li>Внесены правки в модуль <b>convert</b>: появился учет новых регионов, добавлен класс для конвертации скейлов</li>
<li>Добавлен новый класс <b>HolidaySeasonality</b>: для метрики в дневном скейле вкупе с производственным календарем можно находить вектор сезонности (эффектов праздников на метрику) </li>
<li><b>greenplum</b> теперь может получать словарь с типами данных <b>dtype</b></li>
<li>Функции работы с датами <b>get_period_list, to_start, days_in_period, shift_date, diff_scales</b> теперь утилизируют функционал pandas (http://pandas.pydata.org/pandas-docs/stable/user_guide/timeseries.html). Основные изменения -- возможность работать с итерируемыми объектами и скорость работы</li>
    </ul>
</details>
</br>
<details>
<summary><u>Версия 1.3.33</u></summary>
    <ul>
    <li><b>FlatNewbieFunction</b> в <b>optimize.money_function</b> заработали</li>
<li><b>MoneyFunction</b> научились искать точку, где достигается верхний предел функции</li>
<li>По ряду причин попали в релиз, но все еще не работаю <b>optimize.properties</b></li>
<li><b>hahn</b> научился обрабатывать параметр <b>syntax_version</b></li>
    </ul>
</details>
</br>
<details>
<summary><u>Версия 1.3.32</u></summary>
    <ul>
    <li>Функция <b>get_diff_scales</b> убрана из <b>seasonality</b> и перенесена в основной init, а работа метода <b>get_scale_number</b> ускорена (больше там не используется apply)</li>
<li>Метод отрисовки <b>plot_many_frames</b> теперь может работать с <b>Series</b></li>
<li>(bugfix) в <b>CohortSeasonality</b> если <b>scale</b> передан в индексе данных и не передан scale_number, то код теперь не будет падать</li>
<li>(bugfix) правильный учет <b>date_to</b> в ElasticityModel.get_fact()</li>
<li><b>Analyser</b> научился считать вклад от каждой метрики в <b>GMV</b> и <b>Trips</b></li>
<li><b>Analyser</b> научился считать расхождения план/факт по нескольким городам</li>
<li>Добавлен модуль <b>convert</b> : в нем содержатся классы для разбиения данных на разные регионы и скейлы</li>
<li>Добавлена функция <b>apply_multiple_factors</b> : она позволяет исправить когортные данные по дневной матрице коэффициентов</li>
<li>Добавлена функция <b>read_table_adjust_factors</b> : читает данные и сразу их исправляет с помощью <b>apply_multiple_factors</b></li>
<li>В <b>optimize</b> появилось несколько <b>money_function</b> (новички в нерабочем состоянии)</li>
    </ul>
</details>
</br>
<details>
<summary><u>Версия 1.3.31</u></summary>
    <ul>
    <li>метод <b>filter_data</b> в <b>Model</b> теперь может фильтровать по fit_scale. Нужно, если fit/forecast используют разные scale</li>
    <li>В <b>ElasticityModel</b> в методе <b>get_changes_for_balance</b> добавлена проверка деления на нулевой баланс</li>
    <li>Функция <b>convert_data_to_scale</b> обогащена опцией разбивки данных с наперед заданной пропорцией</li>
    </ul>
</details>

<details>
<summary><u>Версия 1.3.30</u></summary>
    <ul>
    <li>методы <b>save</b> и <b>load</b> в <b>Model</b> теперь корректно обрабатывают списки и словари, содержащие модели</li>
    </ul>
</details>
</br>
<details>
<summary><u>Версия 1.3.29</u></summary>
    <ul>
    <li>(bugfix) <b>smart_update</b> работает с <b>None</b> (в предыдущей версии из-за этого не работала часть yql-запросов)</li>
<li>(bugfix) в <b>__init__</b> добавлен метод <b>is_string</b> + на него переведена OneParameterModel, где не работала передача параметров через <b>unicode</b></li>
    </ul>
</details>
</br>
<details>
<summary><u>Версия 1.3.28 (версия содержит критические баги)</u></summary>
    <ul>
    <li>было ускорено выполнение <b>split_scale</b> в случае если <b>proportions</b> передаются как <b>np.array</b></li>
<li><b>CurveFitter</b> также был существенно ускорен (за счет перехода на np.array)</li>
<li>расширена документация для Model, OneParameterModel, <b>ElasticityModel</b></li>
<li><b>plot.series_data</b> по-умолчанию изменила значение <b>shift</b> на 0</li>
<li><b>ElasticityModel</b> была переведена под капотом на <b>OneParameterModel</b> и получила некоторое ускорение в работе: подробности можно смотреть в тикете <a href="https://st.yandex-team.ru/TAXIANALYTICS-5304">TAXIANALYTICS-5304</a></li>
<li>функция <b>get_scale_number_in_year</b> перенесена в <b>__init__</b></li>
<li>в <b>LinearBoundedCurve</b> добавлена поддержка передачи в качестве аргумента <b>np.array</b></li>
<li>класс <b>Model</b> получил новое рождение: пока с сохранением обратной совместимости</li>
<li>в классе <b>Model</b> произошли переименования (старые названия работают, но deprecated): <b>__main_params__</b> —> main_parameters, <b>__params__</b> —> external_parameters, fit/forecast_incity —> fit/forecast_dimension</li>
<li>в классе <b>Model</b> методы save/load позволяют сохранять и загружать модели любой вложенности + загрузка сложной модели не требует дополнительных танцев с бубнами</li>
<li>в классе <b>Model</b> методы fit/forecast содержат логику: фильтруют данные и вызывают внутри *_dimension (поэтому не надо больше везде это писать заново). Причем там есть +/- гибкие настройки фильтрации, специфичные например для <b>OneParameterModel</b></li>
<li>(bugfix) в <b>budget_metrics</b> исправлено использование функции <b>NVL</b></li>
<li>в <b>queries.runner</b> добавлены шаблоны для вычисления когорт (simple_cohorts) по группам <b>run_group_cohorts</b> и обычных когорт <b>run_simple_cohorts.</b> Какие-то подробности есть в тикете <a href="https://st.yandex-team.ru/TAXIANALYTICS-5445">TAXIANALYTICS-5445</a></li>
    </ul>
</details>
</br>
<details>
<summary><u>Версия 1.3.27</u></summary>
    <ul>
    <li>обновлен список городов-миллионников (MILLOINS) + добавили соответствие названий вершинам геоиерархии для миллионников (MILLIONS_GEO)</li>
<li>в <b>WindowSeasonality</b> обработка выбросов вынесена в отдельный параметр <b>drop_outliers</b></li>
<li>(bugfix) в <b>CohortSeasonality</b> исправлен баг, требующий наличия строки с нулями в самом начале когорт</li>
<li><b>CurveFitter</b> (и соответственно <b>OneParameterModel</b> ) получил параметр <b>seed_curve</b> (по этой кривой модель предобучается, результат затем используется как x0 для основной кривой)</li>
<li><b>OneParameterModel</b> получила совместимость с методами борьбы с выбросами через параметр <b>outliers</b></li>
<li><b>OneParameterModel</b> может делать прогноз (forecast) для данных без колонки <b>scale</b> (в этом случае прогноз будет делаться просто для всего DataFrame)</li>
<li>в <b>OneParameterModel</b> определен новый метод fast_forecast, который работает только с числами, зато быстро</li>
<li>в <b>ElasticityModel</b> добавлена возможность вычислять demand/supply_change не циклом, а через балансные значения конверсии, через параметр <b>iterative_change</b></li>
<li>по-умолчанию стали доступны загрузки discounts, <b>sub_gmv</b> и <b>commission</b> в таблицу planning/fact</li>
<li>появился вариант загрузки нескольких фактических метрик одним запросом (вместо нескольких маленьких)</li>
<li>в <b>recount_metric</b> появилась возможность самостоятельно задать <b>timeout</b> между запросами</li>
<li>расчеты когорт по <b>SH</b> перешли на <b>driver_session_reduced</b> + изменился порядок джойнов в запросе (все изменения направлены на ускорение расчета)</li>
<li><b>plot_many_scatters</b> научился получать как параметр <b>colormap</b> + общие для всех данных аргументы</li>
<li>Plan.from_excel() научился читать планы, в которых нет всех необходимых листов</li>
<li>добавлен модуль <b>optimize</b> (на данный момент в него вошли только базовые классы + функция эффекта от скидок)</li>
<li>появилась функция <b>describe</b> (она умеет выводить всю документацию по классу)</li>
    </ul>
</details>
</br>
<details>
<summary><u>Версия 1.3.26</u></summary>
    <ul>
<li>добавлен скрипт <b>hourly_metrics_restore</b> который позволяет восстановить данные старого <b>Uber</b> в часовых точках по <b>supply</b> и <b>demand</b></li>
<li>в модуль <b>planning</b> добавлена финальная работающая версия <b>hit_by_retention</b></li>
<li>(несовместимость с предыдущими версиями) из-за обновления иерархии название страны теперь берется из lvl2_name_ru</li>
    </ul>
</details>
</br>
<details>
<summary><u>Версия 1.3.25</u></summary>
    <ul>
    <li><b>OneParameterModel</b> умеет отрисовывать веса точек цветом</li>
<li>добавлен модуль <b>greenplum</b> (по аналогии с hahn) для выполнения запросов на <b>GP</b> и перезаливки данных с <b>YT</b></li>
<li>(критичный bugfix) при переходе на неикрементальный расчет когорт по водительским сессиям данные раньше задваивались (исправлено)</li>
<li>модули <b>hahn</b> и <b>greenplum</b> не нарушают работу библиотеки, если отсутствует токен</li>
<li>в YQL-запросах теперь используется страна из геоиерархии, притянутая в запросе <b>hierarchy</b></li>
<li>в <b>hourly_trips</b> выделены поездки по старому <b>Uber</b></li>
    </ul>
</details>
</br>
<details>
<summary><u>Версия 1.3.24 (некоторые функции обратно несовместимы)</u></summary>
    <ul>
    <li>в расчет бюджетных метрик <b>budget_metrics</b> добавлен <b>NI</b> + структурировали расчет скидок, субсидий и <b>GMV</b></li>
<li>в основной <b>__init__</b> добален декоратор <b>retry</b> : быстрый путь к перезапуску функции, если произошла ошибка</li>
<li>при запуске <b>queries.runner.recount_metric</b> с несколькими метриками, они запускаются с таймаутом в 5 секунд</li>
<li>в <b>Elasticity.get_balance_conversion</b> добавлена возможность вычислять баланс по стоимости (веса на <b>demand</b> и <b>supply</b> )</li>
<li>(несовместимость с предыдущими версиями, для инкрементальных расчетов) в расчет когорт по водителям добавлено разделение на найм и ренайм</li>
<li>модуль <b>planning</b> претерпел некоторые перемены и научился подгонять по ретеншену (но еще с багами)</li>
<li>расчет скрипта <b>surge</b> стал deprecated, теперь он перенесен в <b>budget_metrics</b> и считается по <b>dm_order</b></li>
<li>автоматически в <b>planning.fact</b> начала прогружаться метрика <b>demand_first_city</b></li>
<li>все параметры-исключения (с которыми можно пересчитывать без sub_path) вынесены в основной конфиг</li>
<li>(bugfix) исправлен расчет когорт в конфигурации: астрономические, по первому городу + с обрезанием по 45 дней</li>
<li>(bugfix) после расчета новых пользователей добавлен <b>commit</b> (ошибка сказывалась только на расчете, в котором не было новых водителей)</li>
    </ul>
</details>
</br>
<details>
<summary><u>Версия 1.3.23</u></summary>
    <ul>
<li>Фикс бага в версии 1.3.22</li>
    </ul>
</details>
</br>
<details>
<summary><u>Версия 1.3.22 (баг)</u></summary>
    <ul>
<li>фикс бага в версии 1.3.21</li>
    </ul>
</details>
</br>
<details>
<summary><u>Версия 1.3.21 (баг)</u></summary>
    <ul>
<li>добавлен инкрементальный расчет driver_sessions</li>
    </ul>
</details>
</br>
<details>
<summary><u>Версия 1.3.20</u></summary>
    <ul>
<li>исправлен баг в query расчета surge</li>
<li>в init.py добавлен список городов-миллионников MILLIONS</li>
    </ul>
</details>
</br>
<details>
<summary><u>Версия 1.3.19 (содержит баг в query расчета surge)</u></summary>
    <ul>
<li>инкрементальный расчет surge</li>
<li><i>queries/reader.py:</i> вспомогательная функция convert_to_datetime(), конвертирует колонки с датами-строками в тип datetime</li>
<li><i>queries/runner.py:</i> recount_metric() теперь может запускать YQL запросы для расчета метрик параллельно  </li>
<li><i>fact.yql:</i> не сохраняет старые версии факта при выгрузке</li>
<li><b>queries:</b> реализована возможность считать когорты, не обрезанные по последней неделе, т.е. текущая неделя будет неполная, задается параметром truncate_incomplete_scale</li>
    </ul>
</details>
</br>
<details>
<summary><u>Версия 1.3.18</u></summary>
    <ul>
<li>В модуль <b>curves</b> добавлен класс LinearBoundedCurve</li>
<li>В класс <b>seasonality</b> добавлен метод <i>crop_seasonality()</i> он обрезает сезонность, делая ее такой, чтобы максимальное значение не превышало upper_bound, а минимальное было не меньше lower_bound</li>
<li><b>planning:</b> many retentions saved</li>
<li><b>planning:</b> comparing retention in any period</li>
<li>users_new.yql исправлен баг с подсчетом туристов</li>
<li><b>hit_by_activity:</b> handle None seasonality</li>
<li><b>hit_method:</b> fix bug with comparing error</li>
<li><b>planning:</b> newbie dependencies between cities</li>
<li><b>NPreviousScaleMigration:</b> исправлен баг с копированием модели</li>
    </ul>
</details>
</br>
<details>
<summary><u>Версия 1.3.17</u></summary>
    <ul>
<li><i>budget_metrics.yql:</i> добавлены новые поля</li>
<li>в <b>NPreviousScaleMigration</b> добавлена возможность передавать сырую таблицу с миграциями + исправлены пара багов </li>
<li>в <i>queries/reader.py</i> добавлена read_planning_table() - функция чтения любых таблиц из папки planning на YT</li>
<li>в <i>queries/runner.py</i> добавлена upload_planning_table() - функция выгрузки любого датафрейма в папку planning на YT</li>
<li>исправлен баг в <b>OneParameterModel</b> фикс</li>
<li>в <i>queries/runner.py</i> добавлена функция __convert_dtypes_to_yql__(), преобразующая типы колонок датафрейма в типы YT</li>
<li><b>MultipleConfigs:</b> чтение параметров модели из папки, если вместо самих параметров передан путь</li>
<li>в <i>queries/runner.py</i> реализована возможность выгрузки фактических метрик одним чанком</li>
    </ul>
</details>
</br>
<details>

<summary><u>Версия 1.3.16</u></summary>
    <ul>
<li>Исправлен setup.py файл (папка curves добавлена)</li>
    </ul>
</details>
</br>
<details>
<summary><u>Версия 1.3.15 (версия не работает)</u></summary>
    <ul>
<li>В queries.runner.py в методе upload_forecast.py исправлена бага при инициализации today при scale=='month'</li>
    </ul>
</details>
</br>
<details>
<summary><u>Версия 1.3.14</u></summary>
    <ul>
<li>Версия, не содержащая критических багов</li>
    </ul>
</details>
</br>
<details>
<summary><u>Версия 1.3.13 (версия содержит критические баги)</u></summary>
    <ul>
<li>Были добавлены новые баги исправлены старые</li>
    </ul>
</details>
</br>
<details>
<summary><u>Версия 1.3.12 (версия содержит критические баги)</u></summary>
    <ul>
<li>Были добавлены новые баги исправлены старые</li>
    </ul>
</details>
</br>
<details>
<summary><u>Версия 1.3.11 (версия содержит критические баги)</u></summary>
    <ul>
<li>Были добавлены новые баги исправлены старые</li>
    </ul>
</details>
</br>
<details>
<summary><u>Версия 1.3.10 (версия содержит критические баги)</u></summary>
    <ul>
<li><b>CohortModel</b>: передача скейла в <b><i>continue_retention_curves</b></i></li>
<li>добавлена <b>OneParameterModel</b>: Модель, подбирающая наилучшую кривую, описывающую зависимость одной переменной от другой. Вид кривой может быть задан параметрами модели.</li>
<li>создан отдельный модуль <b>curves</b>, состоящий из классов <b>Curve</b> (класс кривой) и <b>CurveFitter</b> (Подбирает для объекта класса <b>Curve</b> (или его наследника) параметры (вектор чисел), наилучшим образом описывающие переданный ему набор точек на плоскости)</li>
<li>в модели эластичности теперь вместо <b>ConversionCurve</b> используется класс <b>Curve</b></li>
<li>добавлен новый метод <b><i>plot_many_scatters</b></i>  в модуль <b>plot</b>: отрисовка нескольких Series/DataFrame на одном графике с возможностью передачи аргументов отрисовки</li>
<li><b>NPreviousScaleMigration</b> теперь сохраняет входные данные в своем теле</li>
<li>исправлен баг с последней неделей в <b><i>create_full_seasonality</b></i></li>
<li>в модуле <b>queries</b> переписаны запросы инкрементального добавления данных в таблицы через DEFINE ACTION</li>
    </ul>
</details>
</br>
<details>
<summary><u>Версия 1.3.9</u></summary>
    <ul>
<li>исправлен метод <b><i>__deepcopy__</b></i> в классе <b>DictAlikeObject</b></li>
<li>в модуль <b>planning</b> добавлен скрипт форматирования Excel данных</li>
<li>рефакторинг <b>Planner</b></li>
<li>исправлен баг в <b>app_cannibalization.yql</b>, из-за которого дублировались данные</li>
<li><b>planning</b>: added fact diffs in retention list</li>
<li>в модуль <b>queries</b> добавлены запросы для подсчета метрик <b><i>demand/trips/supply</b></i> по любому скейлу</li>
<li>исправлена ошибка сдвига на 3 часа при подсчете метрик <b><i>demand/trips/supply</b></i></li>
<li>исправлен баг <b>series_models.NonLinearModel</b>, из-за которого он падал на некоторых входных параметрах</li>
<li>добавлен новый класс <b>SplittedSourcesElasticityModel</b>: позволяет реализовать возможность предсказания внутри модели эластичности сразу supply и demand в произвольной разбивке. Например, предсказать supply по всем водителям, а demand в разбивке на телефон и онлайн, а потом с учетом суммарного деманда предсказать поездки. Основной моделью (интерфейсом) при этом остается модель эластичности</li>
<li>исправлен баг проброски <b><i>region_id</b></i> из иерархии в таблицы из planning</li>
    </ul>
</details>
</br>
<details>
<summary><u>Версия 1.3.8</u></summary>
    <ul>
<li>в <b>series_models.LinearModel</b> добавлен новый параметр <b><i>start_default_dot</i></b>, теперь <b><i>start_default_dot</i></b> отвечает за то, когда начинать заменять коэффициенты на default значения, а <b><i>start_corrections_dot</i></b> за то, когда ограничивать значения константой</li>
<li>в класс <b>Trainer</b> добавлен метод <b><i>get_closest_models(index, distance)</i></b>, он находит все конфиги, которые отличаются от модели под номером <b><i>index</i></b> на <b><i>distance значений</i></b></li>
    </ul>
</details>
</br>
<details>
<summary><u>Версия 1.3.7</u></summary>
    <ul>
    <li>исправлен баг с логгированием в файл в классе <b>Timer</b></li>
<li>(баг) была попытка исправить баг в <b>NonLinearModel</b> , из-за которого при указании fit_incremental=False код мог падать. В результате был выявлен другой баг, из-за которого при больших <b>non_linear_model_border</b> код падает</li>
<li>в когортной сезонности исправили баг с добавлением 53 недели (в предыдущих версиях сезонность на 52 неделе занижена)</li>
<li>исправлен баг в recount_all_metrics(): изменен алгоритм поиска всех скриптов</li>
<li>в plot.cohorts() добавлена возможность передавать <b>xlims</b> и <b>ylims</b></li>
<li>в расчеты когорт и метрик (по <b>dm_order</b> ) добавлена обработка случая, когда тарифная зона в источнике отсутствует</li>
<li>в <b>LinearModel</b> появился параметр <b>start_corrections_dot</b></li>
<li>в основной <b>init</b> добавлен новый класс DictAlikeObject, который делает наследуемый от него класс похожим на словарь</li>
<li>в основной <b>init</b> добавлена функция <b>get_period_list</b> возвращающая список дат из диапазона</li>
<li>в <b>budget_metrics.yql</b> <b>GMV</b> теперь считается по <b>order_cost</b> вместо <b>user_cost</b></li>
    </ul>
</details>
</br>
<details>
<summary><u>Версия 1.3.6</u></summary>
    <ul>
<li>в <b>city_migration</b> добавлено восстановление данных Убера</i></li>
<li>в таблицах в <b>planning</b> добавлено новое поле - id региона по геоиерархии</li>
<li>вынесен список кастомных вершин иерархии в общие параметры (больше не надо их дублировать) + можно теперь посчитать что-нибудь только по кастомным вершинам</li>
<li>теперь hahn может логировать запускаемые запросы вместе с публичными ссылками на них (по умолчанию отключено)</li>
<li>добавлен запрос <b>budget_metrics.yql</b>, вычисляет основные метрики из бюджета для сравнения план/факт</li>
    </ul>
</details>
</br>
<details>
<summary><u>Версия 1.3.5</u></summary>
    <ul>
<li>исправлен баг версии 1.3.4: в <b>MultipleConfigs</b> не сохранялись некоторые параметры</li>
    </ul>
</details>
</br>
<details>
<summary><u>Версия 1.3.4 (версия содержит критические баги)</u></summary>
    <ul>
<li>в расчет часовых точек добавлена агрегация по глобальному скейлу (загружается в соответсвующие подпапки month/week/day)
<li>изменены дефолтные параметры для расчета когорт: теперь факт заливается из агрегированных часовых точек</li>
<li>добавлена возможность сохранять вложенные модели (когда параметром одной модели является инстанс другой модели)</li>
    </ul>
</details>
</br>
<details>
<summary><u>Версия 1.3.3</u></summary>
    <ul>
    <li>в расчет часовых точек добавлен параметер <i>use_first_city</i></li>
<li>добавлен запрос сохранения текущей таблицы иерархии</li>
<li>изменены дефолтные параметры для расчета когорт: по первому городу, без таймаутов </li>
    </ul>
</details>
</br>
<details>
<summary><u>Версия 1.3.2</u></summary>
    <ul>
    <li>исправлен баг в <b>CohortSeasonality</b>, из-за которого зависал расчет если в данных много нулей</li>
<li>в <b>MultipleConfigs</b> добавлена возможность пропуска ошибок при fit/forecast</li>
<li>добавлены новые вершины иерархии</li>
<li>в <b>runner</b> добавлена возможность пересчитывать часовые точки в любых периодах, не указывая при этом <b>sub_path</b> (параметры <b>first_date_shift</b> и <b>last_date_shift</b>)</li>
    </ul>
</details>
</br>
<details>
<summary><u>Версия 1.3.1</u></summary>
    <ul>
<li>добавлен новый класс <b>MultipleRetention</b>: в нем реализована возможность продлевать не единую кривую ретеншена, а каждую кривую для каждой когорты (его внедрение потребовало изменений в CohortModel, LinearModel)</li>
<li>изменена логика работы LinearModel: теперь она продлевает не одну кривую ретеншена, а матрицу ретеншенов. Работает в связке с <b>MultipleRetention</b></li>
<li>в <b>Trainer</b> добавлен метод сохранения посчитанных конфигов в файлы</li>
<li>расширена документация в <b>trainer.py</b> и <b>NonLinearModel</b></li>
<li>добавлена модель-обертка для использования в пердсказании нескольких конфигов <b>MultipleConfigs</b></li>
<li>создан новый класс <b>NPreviousScaleMigration</b>, раелизующий механику миграций из города в город, имея матрицу миграций и применяя ее к результатам работы другой модели, например, когортной	</li>
<li>в <b>NonLinearModel</b> из кода вынесена константа <b>max_regular_retention</b> , ограничивающая сверху значение ретеншена</li>
<li>в <b>CohortModel</b> добавлен параметр <b>only_add_value_seasonality</b> , который позволяет не вычитать сеонность из истории, а только добавлять ее в конце</li>
<li>в базвый класс <b>Seasonality</b> добавлен атрибут, отвечающий за число периодов в году + метод, позволяющий получить сезонность из единиц <b>empty_season</b></li>
<li>все активные запросы переехали на иерархию: теперь агрегация происходит по единой иерархии https://tableau.taxi.yandex-team.ru/#/views/Geohierarchy/hierarchy?:iid=1 . То есть <b>city</b> теперь берется из тарифной зоны  + иерархии</li>
<li><b>(по техническим причинам не вошло в релиз)</b> добавлены запросы вычисляющие <b>surge</b> и каннибализацию новичков телефона и онлайна</li>
    </ul>
</details>
</br>
<details>
<summary><u>Версия 1.3.0</u></summary>
    <ul>
    <li>(исправлен баг версии 1.2.34) окончательно перешли на поиск региона по названию города</li>
<li>данные убера теперь восстанавливаются в объектах <b>user_info</b> и <b>driver_info</b> , то что раньше называлось в них <b>sessions_with_wait</b> , <b>supply_hours</b> , <b>visited_users</b> , <b>drivers_on_line</b> , <b>trips</b> , <b>rides</b> теперь имеет суффикс <b>_yandex</b></li>
<li>в расчет по приложениям добавлен еще один флаг, а флаг <b>include_application</b> сменил свою роль. Теперь <b>use_application</b> говорит о том, надо ли вообще считать когорты с учетом тарифов, а <b>include_application</b> отвечает за то, хотите вы посчитать когорты по указанному приложению или по всем, <b>кроме</b> него</li>
<li>обновили документацию в <b>recount_all</b> и <b>recount_query</b></li>
<li>добавлена полноценно рабочая версия <b>HitMethod</b> и <b>HitByActivity</b></li>
<li>добавлен расчет метрики каннибализация приложений: <b>app_cannibalization</b></li>
    </ul>
</details>
</br>
<details>
<summary><u>Версия 1.2.37</u></summary>
    <ul>
    <li>пофиксили минорный баг версии 1.2.36 при расширении <b>Score</b></li>
<li>в <b>weight_curves.py</b> добавлена экспоненциальная кривая веса (ExpExpWeightCurve)</li>
<li>в <b>Score</b> добавлен параметр <b>known_future</b> , который позволяет обучать модель на всех данных, а не только до <b>date_to</b> (работает только для когортной модели!)</li>
<li>в расчет миграций добавлены поездки (раньше были только пользовательские сессии)</li>
<li>в <b>Trainer</b> добавлен метод <b>get_config_files</b></li>
<li>в <b>WindowSeasonality</b> добавлена возможность отнормировать сезонность, чтобы в сумме она давала количество периодов</li>
<li>обновлен класс <b>series_models.NonLinearModel</b> (больше не используется <b>scipy.optimize.curve_fit</b> + добавлены разные варианты расчета)</li>
<li>в <b>__init__</b> добавлена функция <b>extend_index</b> , которая позволяет расширить индекс pandas-объекта (например, добавить в индекс содержащий только город, еще и недели из другого pandas-объекта)</li>
<li>в <b>__init__</b> добавлена функция <b>assign_series</b> , которая позволяет присвоить одной колонке в <b>DataFrame</b> или <b>Series</b> значение <b>Series</b> с другим индексом, при этом индекс расширяется до объединения индексов</li>
<li>исправлен минорный баг в <b>CohortModel</b> , из-за которого нельзя было передавать в качестве <b>dimensions</b> список</li>
<li>интерфейс базового класса <b>Model</b> приведен в соответствие с новой реальностью</li>
<li>бета-версия классов <b>HitMethod</b> и <b>HitByActivity</b> добавлена в <b>planning</b> (они позволяют корректировать прогноз с помощью активности новичков, чтобы попасть в цель по поездкам)</li>
<li>теперь в сообщении об ошибке при чтении таблицы будет сообщаться также переданное пользователем название таблицы</li>
<li>при расчете объекта <b>users_new_one_by_phone</b> теперь будет использоваться <b>dttm</b> в качестве <b>expire_from</b> , а не когорта (это позволит не терять сессии)</li>
    </ul>
</details>
</br>
<details>
<summary><u>Версия 1.2.36</u></summary>
    <ul>
    <li>в <b>Score</b> добавлен метод <b>add</b> , который позволяет объединить результаты двух объектов <b>Score</b> (не работает, если один из объектов пустой)</li>
    </ul>
</details>
</br>
<details>
<summary><u>Версия  1.2.35</u></summary>
    <ul>
    <li>в основной  <b>__init__.py</b> добавлена функция  <b>fill_missing_dates</b> , заполняющая пропущенные в когортах данные нулями</li>
<li>в функцию  <b>read_plan</b> добавлено преобразование  <b>value</b> к типу  <b>float</b></li>
<li>в запросе, загружающем прогноз заменили  <b>full</b> <b>join</b> со списком новых городов на  <b>left</b> <b>join</b></li>
<li> <b>Timer</b> научился писать стартовое сообщение</li>
<li>расчет метрики  <b>city_migration</b> теперь рассчитывает миграции из каждого города в каждый</li>
<li>из  <b>__mapping</b> 'ов убрали NULL'ы, чтобы ускорить расчет когорт</li>
<li>в  <b>ElasticityModel</b> параметр  <b>ndots_fact</b> в методе  <b>fit</b> , изменил свое название на  <b>ndots_fit</b></li>
<li>(исправлен баг версии 1.2.34) в той версии была добавлена лишняя строка, из-за которой  <b>ElasticityModel</b> фиттилась ровно для одного города, в этой версии баг исправлен</li>
<li>появился новый класс  <b>TaskManager</b> , который будет отвечать за многопоточность. Сейчас в нем есть один метод, параллельно вычисляющий функцию на нескольких, возможно меняющихся, параметрах</li>
    </ul>
</details>
</br>
<details>
<summary><u>Версия  1.2.34 (версия содержит критические баги)</u></summary>
    <ul>
    <li>функция  <b>fill_gaps_array</b> вынесена в основной  <b>__init__.py</b></li>
<li>(допущена ошибка в реализации) в расчете пользовательских сессий вернулись к определению регионов МО и ЛО по городу</li>
<li>в  <b>ElasticityModel</b> добавлен параметр, позволяющий выкидывать точки, в которых конверсия больше 1 (по-умолчанию он включен)</li>
<li>поездки больше не фильтруются по  <b>fraud_order_flg</b> (ни в когортах, ни в часовых точках)</li>
    </ul>
</details>
</br>
<details>
<summary><u>Версия  1.2.33</u></summary>
    <ul>
    <li>по техническим причинам все еще не в релизе модуль  <b>train</b></li>
<li>в  <b>CohortModel</b> добавлен новый параметр - аномальная сезонность, которая выбрасывается из данных, но не применяется обратно</li>
<li>в  <b>plot</b> добавлен новый метод, позволяющий строить несколько DataFrame-like объектов на одном графике, передавая их вид через параметры</li>
<li>(исправлен баг версии 1.2.31) фича с фильтрацией данных через  <b>read_parameter</b> теперь работает</li>
<li>добавлен модуль  <b>planning</b> , позволяющий планировать поездки и новичков с учетом баланса</li>
    </ul>
</details>
</br>
<details>
<summary><u>Версия  1.2.32</u></summary>
    <ul>
    <li>по техническим причинам все еще не в релизе модуль  <b>train</b></li>
<li>параметры  <b>from_date</b> и  <b>to_date</b> поменяли свой вид, теперь в них передается не дата, а количество дней</li>
    </ul>
</details>
</br>
<details>
<summary><u>Версия  1.2.31</u></summary>
    <ul>
    <li>проведен рефакторинг расчета когорт, исправили баг в расчете user_sessions, из-за которого терялись первые поездки и сессии от этих поездок</li>
<li>добавили в объект  <b>user_phone_id_mapping</b> приложение, к которому относится указанный <b>user_id</b></li>
<li>(фича не работает) добавлена возможность фильтрации данных внутри запроса в функции  <b>read_parameter</b></li>
<li>в расчеты добавили возможность считать когорты по отдельным приложениям</li>
<li>убрали из функции  <b>retention_new_values</b> параметр  <b>limit_extreme</b> , обрезающий ретеншен, и вынесли его в NonLinearModel, где он сразу все обрезает (стало более прозрачно), параметр был переименован на  <b>global_limit_extreme</b></li>
<li>вернули расчет регионов МО и ЛО по-умолчанию</li>
<li>добавили данные для восстановления исторических провалов <b>SH</b> с учетом убера</li>
<li>(по техническим причинам не вошел в релиз) добавили модуль  <b>train</b> , позволяющий перебирать параметры моделей</li>
<li>в  <b>Score</b> добавлено ограничение на количество процессов (при параллельном вычислении)</li>
<li>теперь часовые данные по <b>SH</b> рассчитываются инкрементально (управлять этим можно через параметры  <b>from_date</b> и  <b>to_date</b> )</li>
    </ul>
</details>
</br>
<details>
<summary><u>Версия  1.2.30</u></summary>
    <ul>
    <li>параметры  <b>script_contains</b> и  <b>force_scale_free</b> можно передавать в  runner.recount_all() без указания  <b>sub_path</b></li>
<li>(исправлен баг) больше история значений параметра не затирается, если попробовать передать пустой <b>DataFrame</b> для записи в таблицу palnning/forecast</li>
<li>параметр  <b>newbie</b> теперь не обязательно передавать в конструктор  <b>CohortModel</b> (хотя он все еще является обязательным параметром), этот параметр теперь добавлен в  <b>forecast</b> (через конструктор все тоже работает)</li>
<li>(исправлен баг) откатили расчет пользовательских когорт от первой сессии в силу нескольких критических багов</li>
<li>в класс  <b>Timer</b> теперь можно передавать файл, в который он будет логгировать события</li>
<li>исправлено использование параметра  <b>new_user_filter</b> (отвечает за способ расчета когорт: от первой поездки или сессии), теперь он действительно влияет на расчет</li>
    </ul>
</details>
</br>
<details>
<summary><u>Версия  1.2.29</u></summary>
    <ul>
    <li>(исправлен баг) поправили порядок расчета когорт, до этого  <b>driver_info</b> считалось позже, чем  <b>driver_sessions</b></li>
<li>исправлен баг версии 1.2.28 с расчетом часовых точек по <b>supply</b></li>
    </ul>
</details>
</br>
<details>
<summary><u>Версия  1.2.28 (версия содержит критические баги)</u></summary>
    <ul>
    <li>в файле  <b>start_part.yql</b> функция  $today больше не возвращает NULL, в случае неизвестного скейла возвращает переданный на вход день</li>
<li>очередной фикс параметра  <b>date_to</b> в  <b>ElasticityModel</b> , починен баг возникающий, когда в  <b>forecast</b> не передавали ни  <b>date_to</b> , ни <b>cities</b></li>
<li>по-умолчанию уникальным идентификатором водителя стал  <b>driver_license_normalized</b></li>
<li>(баг) расчет часовых точек по <b>supply</b> перестал работать из-за несовместимости названий идентификаторов водителей</li>
<li>в  <b>NonLinearModel</b> добавлен новый параметр  <b>limit_extreme</b> , обрезающий ретеншен (по-умолчанию он 1.4), все что выше него в кривой ретеншена заменится на 1</li>
    </ul>
</details>
</br>
<details>
<summary><u>Выкачена версия  1.2.27</u></summary>
    <ul>
    <li>hourly-метрики по умолчанию считаются с декабря 2016 года</li>
<li><b>score</b> сохраняет параметры моделей, которые скорит</li>
    </ul>
</details>
</br>
<details>
<summary><u>Версия  1.2.26</u></summary>
    <ul>
    <li>был пофикшен баг с неправильной передачей параметров  <b>use_timed_out_drivers</b> и  <b>driver_timed_out_days</b> . Появился баг в верси  1.2.17</li>
<li>пофикшен баг в <b>hourly_trips</b> из версии  1.2.25</li>
    </ul>
</details>
</br>
<details>
<summary><u>Версия  1.2.25 (версия содержит критические баги)</u></summary>
    <ul>
    <li>В <b>accuracy.init</b> добавлена возможность выгрузить словарь с датами, для оптимального расчета точности</li>
<li>в <b>ElasticityModel</b> при указании <b>date_to</b> не срезались города, которые не существовали до date_to, они возвращались с 0 прогнозом. Теперь они не возвращаются (это критично для расчета ошибки)</li>
<li>в <b>reader</b> разрешено чтение параметров, которые не были добавлены в конфиг (вместо исключения будет warning)</li>
<li>в <b>hourly_trips</b> добавлен средний чек и средний сурж</li>
<li>(баг) расчет <b>hourly_trips</b> падает из-за <b>driver_net_income</b></li>
<li>добавлена возможность расчета когорт пользователей от первой сессии или от первого заказа</li>
<li>мультипроцессинг полностью заработал</li>
    </ul>
</details>
</br>
<details>
<summary><u>Версия  1.2.24</u></summary>
    <ul>
    <li>Добавлен фикс пропущенных в истории <b>SH</b> с учетом убера</li>
<li>исправлен баг версии  1.2.23</li>
    </ul>
</details>
</br>
<details>
<summary><u>Версия  1.2.23 (версия содержит критические баги)</u></summary>
    <ul>
    <li>изменилась первоначальная догадка о минимуме функции в <b>get_supply</b> (из-за перехода на часовой скейл оптимизируемая функция немного поменяла форму)</li>
<li>в модуле <b>cohort</b> изменилась обработка ретеншена, когда переданы <b>split_dimensions</b> (теперь там просто <b>T</b> вместо unstack)</li>
<li>добавлен мультипроцессинг, но он зависает при больших объемах данных</li>
<li>добавлена возможность скопировать модель (необходимость появилась в мультипроцессинге)</li>
<li>расчет когорт по регионам Москва+МО и Санкт-Петербург+ЛО стал опциональным и по умолчанию не делается</li>
<li>вернулись на <b>demand</b> означающий <b>sessions_with_wait</b></li>
<li>(баг) в этой версии случайно был заложен расчет пользовательских когорт по первой сессии</li>
    </ul>
</details>
</br>
<details>
<summary><u>Версия 1.2.22</u></summary>
    <ul>
    <li>загрузки плана/прогноза/факта исправлены в соответствии с новым форматом ods/mdb/city/city</li>
<li>расчеты перешли на новый <b>dm_order_ods_based</b></li>
<li>пофикшен поиск оптимального для города баланса (на часовом скейле поменялась форма минимизируемой функции)</li>
    </ul>
</details>
</br>
<details>
<summary><u>Версия 1.2.21</u></summary>
    <ul>
    <li><b>sub_path</b> работает корректно для вычисления метрик (todo: но почему-то читает их неправильно)</li>
<li>разделение недели на дни индивидуально для каждого города (не потеряна совместимость со старой версией)</li>
<li>в <b>warning</b> о том, что кривая ретеншена не зафиттилась добавлено название города</li>
<li>исправлены <b>nan</b> значения в расчете info, когда не было поездок в ЯТ</li>
    </ul>
</details>
</br>
<details>
<summary><u>Версия 1.2.20 (версии 18 и 19 нерабочие)</u></summary>
    <ul>
    <li><b>SH</b> убера восстанавливаем по rides, а не <b>trips</b></li>
<li>убрали странный параметр <b>scale_fun</b> из yql-запросов</li>
<li>переделали расчет часовых данных: <b>elasticity</b> обобщено до metrics, убраны костыли</li>
<li>добавлено сохранение продленного ретеншена в когортной модели</li>
<li>добавили расчет когорт, где все атрибуцируется к городу первой поездки (в этом случае нет расчета по сложным регионам)</li>
<li>добавили вычисление метрик с миграциями поездок, водителей и пользователей между городами</li>
    </ul>
</details>
</br>
<details>
<summary><u>Версия 1.2.17</u></summary>
    <ul>
    <li>небольшой фикс в конфиге, чтобы часовые данные считались</li>
<li>в <b>init</b> добавила функцию, которая разбивает данные в <b>series</b> из большего скейла в меньший в некоторой пропорции (например, из недель в дни): называется  <b>split_scale</b></li>
<li>в эластичности появились методы, которые отдают конверсию в балансе и восстанавливают <b>supply</b> из <b>demand</b> и <b>trips</b></li>
<li>убрала суммирование регионов мск+МО и спб+ЛО в <b>_total_</b> в нашем отчете</li>
<li>избавилась от грязного хака в сессиях для поиска этих регионов, теперь они берутся из <b>last_attr_regions</b></li>
<li>добавила в когорты вариант расчета когорт, когда все относится к городу первой поездки</li>
<li>когорты теперь можно считать по произвольному полю: ну то есть можно вместо <b>user_phone</b> в конфиге подставить user_phone_id, например (комменты забыла в этом месте добавить)</li>
    </ul>
</details>
</details>


