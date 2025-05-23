# Async Executor library
Библиотека для асинхронных запросов

Позволяет, имея некий синхронный "решатель" ([SyncExecutor](https://a.yandex-team.ru/arc/trunk/arcadia/maps/libs/async_executor/include/components.h?rev=r8109058#L12)), построить сервис, обрабатывающий запросы асинхронно и распределенно на кластере.
 - для очереди запросов и глобального состояния нужна распределенная БД. Реализована поддержка [mongoDb](https://wiki.yandex-team.ru/mdb/), есть возможность написать кастомный драйвер базы данных ([Database](https://a.yandex-team.ru/arc/trunk/arcadia/maps/libs/async_executor/include/components.h?rev=r8109058#L26))
 - результаты вычислений загружаются в распределенный сторадж. Реализована поддержка [S3-MDS](https://wiki.yandex-team.ru/mds/s3-api/) и ["чистого" MDS](https://wiki.yandex-team.ru/mds/dev/protocol/). Можно добавлять кастомный драйвер [Uploader-а](https://a.yandex-team.ru/arc/trunk/arcadia/maps/libs/async_executor/include/components.h?rev=r8109058#L52)
 - поддерживается **политика репликации** с заданным коэффицентом - полученные запросы будут исполняться несколькими узлами параллельно в разных ДЦ
 - интегрирована с **ratelimiter**: возможно квотировать вычислительное время по пользователям

Сценарий работы:
  - Задаем запрос, в ответ получаем **токен**. Запрос при этом помещается в БД и стартует его асинхронное исполнение на машинах с достаточным количеством ресурсов.
  - В случае успешного исполнения запроса воркер загружает результат в storage и записывает **URI результата** в базу данных, а также изменяет там статус задачи на "успех" (либо "ошибка", если что-то пошло не так)
  - Поллим по токену статус задачи. Когда он переходит в статус "успех", получаем URI результата
  - Скачиваем сериализованный результат из стораджа по URI

### Типы данных
 - [Request](https://a.yandex-team.ru/arc/trunk/arcadia/maps/libs/async_executor/include/types.h?rev=r8109058#L23) - запрос, сериализованный в строку.
 - [Result](https://a.yandex-team.ru/arc/trunk/arcadia/maps/libs/async_executor/include/types.h?rev=r8109058#L25) - абстрактный интерфейс для результата вычислений. Пользователь должен имплементировать метод для сериализации запроса в `std::ostream`.
 - [Token](https://a.yandex-team.ru/arc/trunk/arcadia/maps/libs/async_executor/include/types.h?rev=r8109058#L19) - уникальный идентификатор задачи в системе. Выдается при  асинхронном запросе и используется для получения состояния задачи.
 - [TaskState](https://a.yandex-team.ru/arc/trunk/arcadia/maps/libs/async_executor/include/task.h?rev=r8109058#L18) - структура, содержащая информацию о состоянии задачи в системе.
 - [TaskStatus](https://a.yandex-team.ru/arc/trunk/arcadia/maps/libs/async_executor/include/task.h?rev=r8109058#L10) - enum для статуса задачи:
   * `InProgress` - задача исполняется - следует перечитать состояние задачи черз какое-то время;
   * `Succeeded`  - задача успешно выполнена, в `TaskState` лежит URI результата;
   * `Failed` - произошла ошибка и исполнение задачи остановлено (финальное состояние).
 
### Использование библиотеки

Основной класс - [AsyncExecutor](https://a.yandex-team.ru/arc/trunk/arcadia/maps/libs/async_executor/include/async_executor.h?rev=r8109058#L33).

1. Реализуем интерфейс для результатов вычислений ``Result``
2. Реализуем интерфейс синхронного решателя - ``SyncExecutor``: здесь должна оказаться пользовательская бизнес-логика. В случае ошибки следует кидать исключение, наследующееся от `std::exception`.
3. Инициализируем драйверы БД и аплоадера ([см. ниже](#настройка-mongodb-и-s3-mds)).
4. Инициализируем с помощью вышеперечисленного ``AsyncExecutor``

Далее доступны два метода:

 - ``executeAsync`` - начать асинхронное исполнение запроса
 - ``asyncTaskState`` - получить статус асинхронной задачи 

Их скорее всего мы и захотим обернуть в ручки своего **yacare**-сервиса.

### Настройка MongoDB и s3-mds

#### MDB
Библиотека тестировалась и используется с [облачным MDB](https://wiki.yandex-team.ru/mdb/).
Квоты на свой ABC-сервис получают [тут](https://dispenser.yandex-team.ru/db/projects)
Далее по [стандартной инструкции](https://docs.yandex-team.ru/cloud/managed-mongodb/quickstart):
  - создаем кластера Managed Service for MongoDB. Скорее всего хватит минимальных настроек хоста, но крайне рекомендуется создать по хосту в каждом своем ДЦ для отказоустойчивости.
  - рекомендуется создавать по кластеру на каждый свой стейджинг (production, testing, etc.)
  - создаем базу данных, пользователя c правами read/write и пароль

Для работы библиотеки с mongo предусмотрен драйвер, который создается с помощью [createDatabaseMdb](https://a.yandex-team.ru/arc/trunk/arcadia/maps/libs/async_executor/include/database_mdb.h?rev=r8109058#L31).

Настройки:
  - `connectionUrl` - стандартный mongoDb url вида `mongodb://<user>:<password_url_and_slash_encoded>@<hostname1>:<port1>,...,<hostnameN>:<portN>/<dbname>`
  - `collection` - строчка - имя коллекции в базе
  - `initialize_collections_on_start` - создать коллекцию, если она еще не создана (для первых запусков на кластере)
  - `expiration_time` - при создании задать время жизни документов.

Код библиотеки не чистит таски, полагаясь на `expiration_time`, поэтому задать его при создании коллекции необходимо.

Можно создать коллекцию и отдельно, позвав функцию [initializeCollections](https://a.yandex-team.ru/arc/trunk/arcadia/maps/libs/async_executor/include/database_mdb.h?rev=r8109058#L33).

#### S3
В качестве объектного хранилища для результатов используем S3-MDS. Его так же как и mdb можно настраивать с помощью [панели Yandex.Cloud](https://yc.yandex-team.ru/).

Действуем по [инструкции](https://wiki.yandex-team.ru/mds/s3-api/faq/#kakmnenachatpolzovatsjas3-apimds).
  - рекомендуется создавать по бакету на каждый из стеиджингов (production, testing, etc.)
  - аутентификацию можно сделать по accessKey+secretKey, а можно с помощью `tvm2`
  - в настройках бакета *доступ на чтение объектов* ставим *публичный* (если планируется давать пользователям доступ к результатам асинхронных вычислений)
  - в разделе *жизненный цикл* бакета создаем правило, чистящее старые объекты (например, через сутки) - сама библиотека не чистит объекты

Далее в библиотеке используем функцию [createS3Uploader](https://a.yandex-team.ru/arc/trunk/arcadia/maps/libs/async_executor/include/uploader_s3.h?rev=r8109058#L30)

Настройки:
  - `host` - скорее всего, `s3.mds.yandex.net`
  - `bucket` - имя вашего бакета
  - `contentType` - (необязательно) тип результата. На практике это - значение HTTP-заголовка `Content-Type:`, который будут получать скачивающие результаты. Пример: `application/x-protobuf`
  - `accessKey` и `secretKey` - в случае аутентификации по паре логин-пароль
  - `s3TvmAlias` - (при аутентификации по `tvm2`) - алиас s3mds из конфига [tvmtool](https://wiki.yandex-team.ru/passport/tvm2/tvm-daemon/#ispolzovaniepsevdonimov) (его туда нужно добавить)
  - `selfTvmAlias` - (при аутентификации по `tvm2`) - алиас вашего прилажения из того же конфига (он тоже должен быть в конфиге)

#### "Чистый" MDS
Для нового проекта скорее всего вам подойдет [S3](#s3) :)

### Ratelimiter

Предполагается, что время выполнения асинхронных задач (и потребляемый ими ресурс) может сильно варьироваться в зависимости от запроса.
В таких условиях квотировать просто число запросов в единицу времени (rps) может быть неэффективно.

Поэтому в библиотеке предусмотрена возможность квотировать *миллисекунды CPU*, потраченные непосредственно на вычисления (время ожидания в очередях не учитывается).

Для того, чтобы включить квотирование нужно:
  - прописать в конфигах ratelimiter лимиты для некоторого своего resourceId
  - в `AsyncExecutor::Config` добавить опцию `rlResourceId` с именем этого ресурса
  - в `AsyncExecutor::Config` добавить опцию `rlSpenderUrl` с ручкой, в которую будет ходить библиотека, "тратя" квоту (дефолтное значение - "spend_ratelimiter_budget")
  - в своем yacare-сервисе с помощью макроса `ASYNC_EXECUTOR_ADD_RATELIMITER_SPENDER_HANDLER_DEF` (или `ASYNC_EXECUTOR_ADD_RATELIMITER_SPENDER_HANDLER(custom_spender_url)`) добавить ручку, взаимодействующую с ratelimiter-ом
  - библиотека не реджектит запросы в случае ухода квоты в минус, поэтому нужно навесить проверку лимитов на свои yacare-ручки (YCR_LIMIT_RATE), принимающие асинхронные запросы (из бюджета пользователя таким образом будет сниматься 1 миллисекунда вначале, и время исполнения запроса потом).


В момент получения запроса из БД воркер создает специальный guard, который считает время и в фоне дергает ручку `http://localhost/spend_ratelimiter_budget` указывая tvmId пользователя, resource id рейтлимитера и размер очередного интервала времени, потраченного на исполнение запроса.

Бюджет пользователя может уходить в минус, так как мы только проверяем его неотрицательность перед приемом запроса. Можно считать, что величина burst таким образом немного больше, чем то, что мы укажем в конфиге ratelimiter-а.

