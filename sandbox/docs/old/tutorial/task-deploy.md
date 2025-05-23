Далее в руководстве вам предстоит изменять код `HELLO_%LOGIN%`, добавляя в неё новую функциональность. Но изменения кода задач из Аркадии не попадают в Sandbox мгновенно, сначала они должны протестироваться и задеплоиться.

Здесь мы рассмотрим **классический деплой архива задач**: исторически первый и [на ноябрь 2019] самый популярный способ. С ним вы уже неявно столкнулись в разделе *[Добавление новой задачи](new_task.md)*.

> Слово *классический* здесь используется как противовес к более современным *[бинарным задачам](./binary-tasks.md)*, деплой которых отличается от описанного здесь.

На каждый коммит в `sandbox/projects` автоматически запускается системная задача BUILD_SANDBOX_TASKS, которая:

* собирает пакет со всеми задачами из исходников, достижимых по графу сборки. Это обычный (не бинарный) [Python-пакет](https://docs.python.org/2.7/tutorial/modules.html#packages) `sandbox.projects`. Файлы не упомянутые в `ya.make` в пакет не попадают;
* выполняет множество тестов для проверки, что код задач пригоден к исполнению в Sandbox;
* упаковывает и отправляет код задач на хосты Sandbox.

**Тесты кода задач** среди прочего проверяют что:

* новые задачи пишутся с использованием SDK2;
* все модули импортируются без ошибок в базовом виртуальном окружении (см. также *[Окружение исполнения задачи](./task-environment.md#python)*);
* у всех классов задач и ресурсов уникальные имена;
* объявления параметров используют валидные аргументы;
* не содержит других ошибок, которые могут вывести Sandbox из строя.

Статус тестирования и деплоя коммитов можно отслеживать в [Testenv](https://beta-testenv.yandex-team.ru/project/sandbox-trunk/job/BUILD_SANDBOX_TASKS/history). После успешной проверки код в течение 1-2 минут доезжает до Sandbox, а номер коммита появляется в подвале интерфейса Sandbox:

![revision ui](https://wiki.yandex-team.ru/users/mkznts/sandbox-tutorial/.files/screenshot2019-09-09at01.50.17.png)

Если кто-то всё же сломает тесты, деплой последующих коммитов остановится пока ошибку не починят, либо не откатят ломающий коммит:

![testenv](https://jing.yandex-team.ru/files/mkznts/Screenshot%202019-09-15%20at%2022.20.23.png)

Каждая такая поломка тормозит разработку всем пользователям Sandbox. Чтобы такого не происходило:

* старайтесь не коммитить в код задач напрямую (используя `SKIP_CHECK`);
* делая pull request, всегда дожидайтесь прохождения тестов в плашке прекоммитных проверок и внимательно изучайте любые новые поломки в тестах с префиксом `sandbox/` (см. [пример](https://jing.yandex-team.ru/files/mkznts/Screenshot%202019-10-08%20at%2017.56.14.png) плашки с ошибкой в коде задач).

Итого, попадание кода в Sandbox таким способом может занять от 35 минут: 20 минут на прекоммитные проверки + 10 минут на сборку после коммита + 3-5 минут на то чтобы архив попал на хосты Sandbox. При этом каждая стадия может занять больше времени из-за высокой нагрузки, а если кто-то до вас сломал код задач, придётся дождаться ещё и выкатки фикса.

Для ближайших заданий вам придётся использовать именно классический деплой. Позже будут рассмотрены и другие способы деплоя, лучше соответствующие методологии [Changing Stuff and Seeing What Happens](https://miro.medium.com/max/600/1*gCWUibmQ8rszKxI3G19KmA.jpeg).
