# Юнит-тесты в релизах

В релиза наших java-приложений мы прогоняем юнит-тесты кода, запуская их в виде Sandbox-таски.
Скрипт dt-launch-sandbox-tests-in-release пишет комментарий в тикет с тем, прошли (SUCCESS) тесты или нет (FAILURE) и оставляет ссылку на задачу в Sandbox.

При некоторых поломках наша автоматика не в силах написать комментарий о том, какие именно тесты не прошли.

## Как читать отчет о запуске
Для начала нужно открыть ссылку на запуск в Sandbox, там найти ссылку на красивый отчет (See Human-readable colored build errors: **output_1.html**)

![no alt](_assets/sandbox-report-hr-log.png "ссылка на красивый отчет")

или простой текст (**<span style="color:red">stderr</span>**: **ya_make.err.txt**).

![no alt](_assets/sandbox-report-err-log.png "ссылка на простой текстовый лог")

Почти в самом конце отчета (примерно на страницу выше) будет суммарная статистика о прохождении:
```
Total 272 suites:
    269 - GOOD
    2 - FAIL
    1 - TIMEOUT
Total 7573 tests:
    7462 - GOOD
    2 - FAIL
    36 - NOT_LAUNCHED
    1 - TIMEOUT
    72 - SKIPPED
```
Вначале идет статистика по модулям и типам тестов:
- 269 прошло
- 2 зафейлились
- в 1 прогон тестов затаймаутился

Потом статистика по самим тестам:
- 7462 прошло
- 2 не прошло
- 36 тестов **запущено не было**, так как они не уложились в таймаут модуля на прогон тестов (это 60 для SMALL или 600 секунд для MEDIUM тестов)
- 1 тест вывалился по таймауту
- 72 теста пропущено (у них в коде стоит аннотация `@Ignore`)

При наличии TIMEOUT в сьютах или NOT_LAUNCHED или TIMEOUT в тестах — нельзя считать прогон успешным, так как могут быть сломаны не сами тесты а код. 
Тесты нужно перепрогонять до прохождения или эскпертным путем определять причину таймаутов (например, TIMEOUT может возникать из-за ошибок при запуске параметризованного теста). 

## Как найти проблемный тест в отчете
Поиском по `[fail] ` — это префикс строк с именем упавшего теста.

{% cut "лог с падением" %}

```
direct/libs/async-http/ut <java> [size:medium]
------ sole chunk ran 15 tests (total:49.27s - test:49.23s)
[good] ru.yandex.direct.asynchttp.FetcherTest::cpuConsumeTest[0] [default-linux-x86_64-release] (9.04s)
Log: http://proxy.sandbox.yandex-team.ru/2459331952/direct/libs/async-http/ut/test-results/async-http-ut/testing_out_stuff/ru.yandex.direct.asynchttp.FetcherTest.cpuConsumeTest[0].log
Logsdir: http://proxy.sandbox.yandex-team.ru/2459331952/direct/libs/async-http/ut/test-results/async-http-ut/testing_out_stuff
[good] ru.yandex.direct.asynchttp.FetcherTest::cpuConsumeTest[1] [default-linux-x86_64-release] (4.10s)
Log: http://proxy.sandbox.yandex-team.ru/2459331952/direct/libs/async-http/ut/test-results/async-http-ut/testing_out_stuff/ru.yandex.direct.asynchttp.FetcherTest.cpuConsumeTest[1].log
Logsdir: http://proxy.sandbox.yandex-team.ru/2459331952/direct/libs/async-http/ut/test-results/async-http-ut/testing_out_stuff
[good] ru.yandex.direct.asynchttp.FetcherTest::errorCodeTest[0] [default-linux-x86_64-release] (0.74s)
Log: http://proxy.sandbox.yandex-team.ru/2459331952/direct/libs/async-http/ut/test-results/async-http-ut/testing_out_stuff/ru.yandex.direct.asynchttp.FetcherTest.errorCodeTest[0].log
Logsdir: http://proxy.sandbox.yandex-team.ru/2459331952/direct/libs/async-http/ut/test-results/async-http-ut/testing_out_stuff
[good] ru.yandex.direct.asynchttp.FetcherTest::errorCodeTest[1] [default-linux-x86_64-release] (0.24s)
Log: http://proxy.sandbox.yandex-team.ru/2459331952/direct/libs/async-http/ut/test-results/async-http-ut/testing_out_stuff/ru.yandex.direct.asynchttp.FetcherTest.errorCodeTest[1].log
Logsdir: http://proxy.sandbox.yandex-team.ru/2459331952/direct/libs/async-http/ut/test-results/async-http-ut/testing_out_stuff
[fail] ru.yandex.direct.asynchttp.FetcherTest::failFastTest[0] [default-linux-x86_64-release] (7.76s)
The following assertion failed:
1) 
Expecting:
 <PT7.736717658S>
to be less than:
 <PT2S> 
at FetcherTest.lambda$failFastTest$14(FetcherTest.java:328)

org.assertj.core.api.SoftAssertionError: 
The following assertion failed:
1) 
Expecting:
 <PT7.736717658S>
to be less than:
 <PT2S> 
at FetcherTest.lambda$failFastTest$14(FetcherTest.java:328)

    at org.assertj.core.api.SoftAssertions.assertAll(SoftAssertions.java:133)
    at org.assertj.core.api.SoftAssertions.assertSoftly(SoftAssertions.java:162)
    at ru.yandex.direct.asynchttp.FetcherTest.failFastTest(FetcherTest.java:325)
    at java.base/jdk.internal.reflect.NativeMethodAccessorImpl.invoke0(Native Method)
    at java.base/jdk.internal.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:62)
    at java.base/jdk.internal.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)
    at java.base/java.lang.reflect.Method.invoke(Method.java:566)
    at org.junit.runners.model.FrameworkMethod$1.runReflectiveCall(FrameworkMethod.java:50)
    at org.junit.internal.runners.model.ReflectiveCallable.run(ReflectiveCallable.java:12)
    at org.junit.runners.model.FrameworkMethod.invokeExplosively(FrameworkMethod.java:47)
    at org.junit.internal.runners.statements.InvokeMethod.evaluate(InvokeMethod.java:17)
    at org.junit.internal.runners.statements.RunBefores.evaluate(RunBefores.java:26)
    at org.junit.runners.ParentRunner.runLeaf(ParentRunner.java:325)
    at org.junit.runners.BlockJUnit4ClassRunner.runChild(BlockJUnit4ClassRunner.java:78)
    at org.junit.runners.BlockJUnit4ClassRunner.runChild(BlockJUnit4ClassRunner.java:57)
    at org.junit.runners.ParentRunner$3.run(ParentRunner.java:290)
    at org.junit.runners.ParentRunner$1.schedule(
..[snippet truncated]..
27)
    at org.junit.runners.ParentRunner$3.run(ParentRunner.java:290)
    at org.junit.runners.ParentRunner$1.schedule(ParentRunner.java:71)
    at org.junit.runners.ParentRunner.runChildren(ParentRunner.java:288)
    at org.junit.runners.ParentRunner.access$000(ParentRunner.java:58)
    at org.junit.runners.ParentRunner$2.evaluate(ParentRunner.java:268)
    at org.junit.internal.runners.statements.RunBefores.evaluate(RunBefores.java:26)
    at org.junit.internal.runners.statements.RunAfters.evaluate(RunAfters.java:27)
    at org.junit.runners.ParentRunner.run(ParentRunner.java:363)
    at org.junit.runners.Suite.runChild(Suite.java:128)
    at org.junit.runners.Suite.runChild(Suite.java:27)
    at org.junit.runners.ParentRunner$3.run(ParentRunner.java:290)
    at org.junit.runners.ParentRunner$1.schedule(ParentRunner.java:71)
    at org.junit.runners.ParentRunner.runChildren(ParentRunner.java:288)
    at org.junit.runners.ParentRunner.access$000(ParentRunner.java:58)
    at org.junit.runners.ParentRunner$2.evaluate(ParentRunner.java:268)
    at org.junit.runners.ParentRunner.run(ParentRunner.java:363)
    at org.junit.runner.JUnitCore.run(JUnitCore.java:137)
    at org.junit.runner.JUnitCore.run(JUnitCore.java:115)
    at ru.yandex.devtools.test.Runner.executeTests(Runner.java:150)
    at ru.yandex.devtools.test.AbstractRunner.run(AbstractRunner.java:70)
    at ru.yandex.devtools.test.AbstractRunner.run(AbstractRunner.java:109)
    at ru.yandex.devtools.test.Runner.main(Runner.java:367)
Log: http://proxy.sandbox.yandex-team.ru/2459331952/direct/libs/async-http/ut/test-results/async-http-ut/testing_out_stuff/ru.yandex.direct.asynchttp.FetcherTest.failFastTest[0].log
Logsdir: http://proxy.sandbox.yandex-team.ru/2459331952/direct/libs/async-http/ut/test-results/async-http-ut/testing_out_stuff
[good] ru.yandex.direct.asynchttp.FetcherTest::failFastTest[1] [default-linux-x86_64-release] (1.10s)
Log: http://proxy.sandbox.yandex-team.ru/2459331952/direct/libs/async-http/ut/test-results/async-http-ut/testing_out_stuff/ru.yandex.direct.asynchttp.FetcherTest.failFastTest[1].log
Logsdir: http://proxy.sandbox.yandex-team.ru/2459331952/direct/libs/async-http/ut/test-results/async-http-ut/testing_out_stuff
[good] ru.yandex.direct.asynchttp.FetcherTest::nonOkAnswersPropagation[0] [default-linux-x86_64-release] (0.25s)
Log: http://proxy.sandbox.yandex-team.ru/2459331952/direct/libs/async-http/ut/test-results/async-http-ut/testing_out_stuff/ru.yandex.direct.asynchttp.FetcherTest.nonOkAnswersPropagation[0].log
Logsdir: http://proxy.sandbox.yandex-team.ru/2459331952/direct/libs/async-http/ut/test-results/async-http-ut/testing_out_stuff
[good] ru.yandex.direct.asynchttp.FetcherTest::nonOkAnswersPropagation[1] [default-linux-x86_64-release] (0.25s)
Log: http://proxy.sandbox.yandex-team.ru/2459331952/direct/libs/async-http/ut/test-results/async-http-ut/testing_out_stuff/ru.yandex.direct.asynchttp.FetcherTest.nonOkAnswersPropagation[1].log
Logsdir: http://proxy.sandbox.yandex-team.ru/2459331952/direct/libs/async-http/ut/test-results/async-http-ut/testing_out_stuff
[good] ru.yandex.direct.asynchttp.FetcherTest::softRetriesCountedOnlyWhenFreeSlotsExist[0] [default-linux-x86_64-release] (4.21s)
Log: http://proxy.sandbox.yandex-team.ru/2459331952/direct/libs/async-http/ut/test-results/async-http-ut/testing_out_stuff/ru.yandex.direct.asynchttp.FetcherTest.softRetriesCountedOnlyWhenFreeSlotsExist[0].log
Logsdir: http://proxy.sandbox.yandex-team.ru/2459331952/direct/libs/async-http/ut/test-results/async-http-ut/testing_out_stuff
[good] ru.yandex.direct.asynchttp.FetcherTest::softRetriesCountedOnlyWhenFreeSlotsExist[1] [default-linux-x86_64-release] (5.60s)
Log: http://proxy.sandbox.yandex-team.ru/2459331952/direct/libs/async-http/ut/test-results/async-http-ut/testing_out_stuff/ru.yandex.direct.asynchttp.FetcherTest.softRetriesCountedOnlyWhenFreeSlotsExist[1].log
Logsdir: http://proxy.sandbox.yandex-team.ru/2459331952/direct/libs/async-http/ut/test-results/async-http-ut/testing_out_stuff
[good] ru.yandex.direct.asynchttp.FetcherTest::testMultipleRequests[0] [default-linux-x86_64-release] (0.82s)
Log: http://proxy.sandbox.yandex-team.ru/2459331952/direct/libs/async-http/ut/test-results/async-http-ut/testing_out_stuff/ru.yandex.direct.asynchttp.FetcherTest.testMultipleRequests[0].log
Logsdir: http://proxy.sandbox.yandex-team.ru/2459331952/direct/libs/async-http/ut/test-results/async-http-ut/testing_out_stuff
[good] ru.yandex.direct.asynchttp.FetcherTest::testMultipleRequests[1] [default-linux-x86_64-release] (0.78s)
Log: http://proxy.sandbox.yandex-team.ru/2459331952/direct/libs/async-http/ut/test-results/async-http-ut/testing_out_stuff/ru.yandex.direct.asynchttp.FetcherTest.testMultipleRequests[1].log
Logsdir: http://proxy.sandbox.yandex-team.ru/2459331952/direct/libs/async-http/ut/test-results/async-http-ut/testing_out_stuff
[good] ru.yandex.direct.asynchttp.FetcherTest::testSoftTimeout[0] [default-linux-x86_64-release] (0.44s)
Log: http://proxy.sandbox.yandex-team.ru/2459331952/direct/libs/async-http/ut/test-results/async-http-ut/testing_out_stuff/ru.yandex.direct.asynchttp.FetcherTest.testSoftTimeout[0].log
Logsdir: http://proxy.sandbox.yandex-team.ru/2459331952/direct/libs/async-http/ut/test-results/async-http-ut/testing_out_stuff
[good] ru.yandex.direct.asynchttp.FetcherTest::testSoftTimeout[1] [default-linux-x86_64-release] (0.41s)
Log: http://proxy.sandbox.yandex-team.ru/2459331952/direct/libs/async-http/ut/test-results/async-http-ut/testing_out_stuff/ru.yandex.direct.asynchttp.FetcherTest.testSoftTimeout[1].log
Logsdir: http://proxy.sandbox.yandex-team.ru/2459331952/direct/libs/async-http/ut/test-results/async-http-ut/testing_out_stuff
[good] ru.yandex.direct.asynchttp.RequestDataTest::noExceptionOnConcurrentAccess [default-linux-x86_64-release] (5.05s)
Log: http://proxy.sandbox.yandex-team.ru/2459331952/direct/libs/async-http/ut/test-results/async-http-ut/testing_out_stuff/ru.yandex.direct.asynchttp.RequestDataTest.noExceptionOnConcurrentAccess.log
Logsdir: http://proxy.sandbox.yandex-team.ru/2459331952/direct/libs/async-http/ut/test-results/async-http-ut/testing_out_stuff
------ FAIL: 14 - GOOD, 1 - FAIL direct/libs/async-http/ut
```

{% endcut %}

Здесь видно, что в модуле **direct/libs/async-http/ut** не прошел тест **ru.yandex.direct.asynchttp.FetcherTest::failFastTest[0]** и ниже идет ошибка, с которой тест зафейлился.


Поиском по `[not_launched] ` можно определить имена тестов которые не были запущены. Имя модуля написано выше.

{% cut "лог с not_launched" %}

```
direct/libs/hourglass-ydb/ut <java>
------ sole chunk ran 37 tests (total:103.53s - recipes:40.16s test:62.58s recipes:0.48s)
Killed by timeout (60 s)
Suite exceeded 60s timeout and was killed
Log: http://proxy.sandbox.yandex-team.ru/2459331952/direct/libs/hourglass-ydb/ut/test-results/hourglass-ydb-ut/run_test.log
Logsdir: http://proxy.sandbox.yandex-team.ru/2459331952/direct/libs/hourglass-ydb/ut/test-results/hourglass-ydb-ut/testing_out_stuff
Stderr: http://proxy.sandbox.yandex-team.ru/2459331952/direct/libs/hourglass-ydb/ut/test-results/hourglass-ydb-ut/testing_out_stuff/stderr
[not_launched] ru.yandex.direct.hourglass.ydb.storage.ScheduleUpdateTest::setNewSchedule_NeedRescheduleNotResetTest() [default-linux-x86_64-release] (0.00s) Test was not launched, because other tests have used all allotted time (60 s)
Logsdir: http://proxy.sandbox.yandex-team.ru/2459331952/direct/libs/hourglass-ydb/ut/test-results/hourglass-ydb-ut/testing_out_stuff
[not_launched] ru.yandex.direct.hourglass.ydb.storage.ScheduleUpdateTest::setNewSchedule_OnlyWhenDifferentScheduleSumUpdateTest() [default-linux-x86_64-release] (0.00s) Test was not launched, because other tests have used all allotted time (60 s)
Logsdir: http://proxy.sandbox.yandex-team.ru/2459331952/direct/libs/hourglass-ydb/ut/test-results/hourglass-ydb-ut/testing_out_stuff
[not_launched] ru.yandex.direct.hourglass.ydb.storage.ScheduleUpdateTest::setNewSchedule_OnlyDifferentVersionUpdateTest() [default-linux-x86_64-release] (0.00s) Test was not launched, because other tests have used all allotted time (60 s)
Logsdir: http://proxy.sandbox.yandex-team.ru/2459331952/direct/libs/hourglass-ydb/ut/test-results/hourglass-ydb-ut/testing_out_stuff
[not_launched] ru.yandex.direct.hourglass.ydb.storage.ScheduleUpdateTest::setNewSchedule_UnArchiveTaskTest() [default-linux-x86_64-release] (0.00s) Test was not launched, because other tests have used all allotted time (60 s)
Logsdir: http://proxy.sandbox.yandex-team.ru/2459331952/direct/libs/hourglass-ydb/ut/test-results/hourglass-ydb-ut/testing_out_stuff
[not_launched] ru.yandex.direct.hourglass.ydb.storage.ScheduleUpdateTest::setNewSchedule_InsertNewTask() [default-linux-x86_64-release] (0.00s) Test was not launched, because other tests have used all allotted time (60 s)
Logsdir: http://proxy.sandbox.yandex-team.ru/2459331952/direct/libs/hourglass-ydb/ut/test-results/hourglass-ydb-ut/testing_out_stuff
[not_launched] ru.yandex.direct.hourglass.ydb.storage.ScheduleUpdateTest::setNewSchedule_ArchiveTaskTest() [default-linux-x86_64-release] (0.00s) Test was not launched, because other tests have used all allotted time (60 s)
Logsdir: http://proxy.sandbox.yandex-team.ru/2459331952/direct/libs/hourglass-ydb/ut/test-results/hourglass-ydb-ut/testing_out_stuff
[not_launched] ru.yandex.direct.hourglass.ydb.storage.ScheduleUpdateTest::setNewSchedule_StatusNotChangedTest() [default-linux-x86_64-release] (0.00s) Test was not launched, because other tests have used all allotted time (60 s)
Logsdir: http://proxy.sandbox.yandex-team.ru/2459331952/direct/libs/hourglass-ydb/ut/test-results/hourglass-ydb-ut/testing_out_stuff
[not_launched] ru.yandex.direct.hourglass.ydb.storage.ScheduleUpdateTest::setNewSchedule_InsertSeveralTimesNewTask() [default-linux-x86_64-release] (0.00s) Test was not launched, because other tests have used all allotted time (60 s)
Logsdir: http://proxy.sandbox.yandex-team.ru/2459331952/direct/libs/hourglass-ydb/ut/test-results/hourglass-ydb-ut/testing_out_stuff
[not_launched] ru.yandex.direct.hourglass.ydb.storage.YdbScheduleUpdaterTest::allTaskHasStorageVersion_NotAllTasks() [default-linux-x86_64-release] (0.00s) Test was not launched, because other tests have used all allotted time (60 s)
Logsdir: http://proxy.sandbox.yandex-team.ru/2459331952/direct/libs/hourglass-ydb/ut/test-results/hourglass-ydb-ut/testing_out_stuff
[not_launched] ru.yandex.direct.hourglass.ydb.storage.YdbScheduleUpdaterTest::concurrentAddNewTasksTest() [default-linux-x86_64-release] (0.00s) Test was not launched, because other tests have used all allotted time (60 s)
Logsdir: http://proxy.sandbox.yandex-team.ru/2459331952/direct/libs/hourglass-ydb/ut/test-results/hourglass-ydb-ut/testing_out_stuff
[not_launched] ru.yandex.direct.hourglass.ydb.storage.YdbScheduleUpdaterTest::allTaskHasStorageVersion_EmptyScheduleTest() [default-linux-x86_64-release] (0.00s) Test was not launched, because other tests have used all allotted time (60 s)
Logsdir: http://proxy.sandbox.yandex-team.ru/2459331952/direct/libs/hourglass-ydb/ut/test-results/hourglass-ydb-ut/testing_out_stuff
[not_launched] ru.yandex.direct.hourglass.ydb.storage.YdbScheduleUpdaterTest::allTaskHasStorageVersion() [default-linux-x86_64-release] (0.00s) Test was not launched, because other tests have used all allotted time (60 s)
Logsdir: http://proxy.sandbox.yandex-team.ru/2459331952/direct/libs/hourglass-ydb/ut/test-results/hourglass-ydb-ut/testing_out_stuff
[not_launched] ru.yandex.direct.hourglass.ydb.storage.YdbScheduleUpdaterTest::allTaskHasStorageVersion_AllTasksAnotherVersion() [default-linux-x86_64-release] (0.00s) Test was not launched, because other tests have used all allotted time (60 s)
Logsdir: http://proxy.sandbox.yandex-team.ru/2459331952/direct/libs/hourglass-ydb/ut/test-results/hourglass-ydb-ut/testing_out_stuff
[not_launched] ru.yandex.direct.hourglass.ydb.storage.ExpiredJobsTest::findTest() [default-linux-x86_64-release] (0.00s) Test was not launched, because other tests have used all allotted time (60 s)
Logsdir: http://proxy.sandbox.yandex-team.ru/2459331952/direct/libs/hourglass-ydb/ut/test-results/hourglass-ydb-ut/testing_out_stuff
[not_launched] ru.yandex.direct.hourglass.ydb.storage.ExpiredJobsTest::updateTest() [default-linux-x86_64-release] (0.00s) Test was not launched, because other tests have used all allotted time (60 s)
Logsdir: http://proxy.sandbox.yandex-team.ru/2459331952/direct/libs/hourglass-ydb/ut/test-results/hourglass-ydb-ut/testing_out_stuff
[not_launched] ru.yandex.direct.hourglass.ydb.storage.NeedRescheduleTest::findTest() [default-linux-x86_64-release] (0.00s) Test was not launched, because other tests have used all allotted time (60 s)
Logsdir: http://proxy.sandbox.yandex-team.ru/2459331952/direct/libs/hourglass-ydb/ut/test-results/hourglass-ydb-ut/testing_out_stuff
[not_launched] ru.yandex.direct.hourglass.ydb.storage.NeedRescheduleTest::updateTest() [default-linux-x86_64-release] (0.00s) Test was not launched, because other tests have used all allotted time (60 s)
Logsdir: http://proxy.sandbox.yandex-team.ru/2459331952/direct/libs/hourglass-ydb/ut/test-results/hourglass-ydb-ut/testing_out_stuff
[not_launched] ru.yandex.direct.hourglass.ydb.storage.ExecutingJobsTest::executingToReadyTest() [default-linux-x86_64-release] (0.00s) Test was not launched, because other tests have used all allotted time (60 s)
Logsdir: http://proxy.sandbox.yandex-team.ru/2459331952/direct/libs/hourglass-ydb/ut/test-results/hourglass-ydb-ut/testing_out_stuff
[not_launched] ru.yandex.direct.hourglass.ydb.storage.ExecutingJobsTest::findTest() [default-linux-x86_64-release] (0.00s) Test was not launched, because other tests have used all allotted time (60 s)
Logsdir: http://proxy.sandbox.yandex-team.ru/2459331952/direct/libs/hourglass-ydb/ut/test-results/hourglass-ydb-ut/testing_out_stuff
[not_launched] ru.yandex.direct.hourglass.ydb.storage.ExecutingJobsTest::updateTest() [default-linux-x86_64-release] (0.00s) Test was not launched, because other tests have used all allotted time (60 s)
Logsdir: http://proxy.sandbox.yandex-team.ru/2459331952/direct/libs/hourglass-ydb/ut/test-results/hourglass-ydb-ut/testing_out_stuff
[not_launched] ru.yandex.direct.hourglass.ydb.storage.ReadyJobsTest::findTest() [default-linux-x86_64-release] (0.00s) Test was not launched, because other tests have used all allotted time (60 s)
Logsdir: http://proxy.sandbox.yandex-team.ru/2459331952/direct/libs/hourglass-ydb/ut/test-results/hourglass-ydb-ut/testing_out_stuff
[not_launched] ru.yandex.direct.hourglass.ydb.storage.ReadyJobsTest::updateTest() [default-linux-x86_64-release] (0.00s) Test was not launched, because other tests have used all allotted time (60 s)
Logsdir: http://proxy.sandbox.yandex-team.ru/2459331952/direct/libs/hourglass-ydb/ut/test-results/hourglass-ydb-ut/testing_out_stuff
[not_launched] ru.yandex.direct.hourglass.ydb.storage.ReadyJobsTest::findRescheduleTest() [default-linux-x86_64-release] (0.00s) Test was not launched, because other tests have used all allotted time (60 s)
Logsdir: http://proxy.sandbox.yandex-team.ru/2459331952/direct/libs/hourglass-ydb/ut/test-results/hourglass-ydb-ut/testing_out_stuff
[not_launched] ru.yandex.direct.hourglass.ydb.schedulerinstances.YdbScheduleInstancesRepositoryTest::getSchedulerInstancesInfoTest() [default-linux-x86_64-release] (0.00s) Test was not launched, because other tests have used all allotted time (60 s)
Logsdir: http://proxy.sandbox.yandex-team.ru/2459331952/direct/libs/hourglass-ydb/ut/test-results/hourglass-ydb-ut/testing_out_stuff
[not_launched] ru.yandex.direct.hourglass.ydb.schedulerinstances.YdbScheduleInstancesRepositoryTest::markInstanceAsMainTest_isMainChanged() [default-linux-x86_64-release] (0.00s) Test was not launched, because other tests have used all allotted time (60 s)
Logsdir: http://proxy.sandbox.yandex-team.ru/2459331952/direct/libs/hourglass-ydb/ut/test-results/hourglass-ydb-ut/testing_out_stuff
[not_launched] ru.yandex.direct.hourglass.ydb.schedulerinstances.YdbScheduleInstancesRepositoryTest::isLeaderTest_OneIsNotMain() [default-linux-x86_64-release] (0.00s) Test was not launched, because other tests have used all allotted time (60 s)
Logsdir: http://proxy.sandbox.yandex-team.ru/2459331952/direct/libs/hourglass-ydb/ut/test-results/hourglass-ydb-ut/testing_out_stuff
[not_launched] ru.yandex.direct.hourglass.ydb.schedulerinstances.YdbScheduleInstancesRepositoryTest::isLeader_LoaderBorderReachedTest() [default-linux-x86_64-release] (0.00s) Test was not launched, because other tests have used all allotted time (60 s)
Logsdir: http://proxy.sandbox.yandex-team.ru/2459331952/direct/libs/hourglass-ydb/ut/test-results/hourglass-ydb-ut/testing_out_stuff
[not_launched] ru.yandex.direct.hourglass.ydb.schedulerinstances.YdbScheduleInstancesRepositoryTest::isLeaderTest() [default-linux-x86_64-release] (0.00s) Test was not launched, because other tests have used all allotted time (60 s)
Logsdir: http://proxy.sandbox.yandex-team.ru/2459331952/direct/libs/hourglass-ydb/ut/test-results/hourglass-ydb-ut/testing_out_stuff
[not_launched] ru.yandex.direct.hourglass.ydb.schedulerinstances.YdbScheduleInstancesRepositoryTest::isLeaderTest_EmptyCandidates() [default-linux-x86_64-release] (0.00s) Test was not launched, because other tests have used all allotted time (60 s)
Logsdir: http://proxy.sandbox.yandex-team.ru/2459331952/direct/libs/hourglass-ydb/ut/test-results/hourglass-ydb-ut/testing_out_stuff
[not_launched] ru.yandex.direct.hourglass.ydb.schedulerinstances.YdbScheduleInstancesRepositoryTest::isLeaderTest_TwoPossibleCandidates() [default-linux-x86_64-release] (0.00s) Test was not launched, because other tests have used all allotted time (60 s)
Logsdir: http://proxy.sandbox.yandex-team.ru/2459331952/direct/libs/hourglass-ydb/ut/test-results/hourglass-ydb-ut/testing_out_stuff
[not_launched] ru.yandex.direct.hourglass.ydb.schedulerinstances.YdbScheduleInstancesRepositoryTest::isLeader_LeaderWithLessVersionTest() [default-linux-x86_64-release] (0.00s) Test was not launched, because other tests have used all allotted time (60 s)
Logsdir: http://proxy.sandbox.yandex-team.ru/2459331952/direct/libs/hourglass-ydb/ut/test-results/hourglass-ydb-ut/testing_out_stuff
[not_launched] ru.yandex.direct.hourglass.ydb.schedulerinstances.YdbScheduleInstancesRepositoryTest::isLeader_ExpiredHeartbeatIsSkippedTest() [default-linux-x86_64-release] (0.00s) Test was not launched, because other tests have used all allotted time (60 s)
Logsdir: http://proxy.sandbox.yandex-team.ru/2459331952/direct/libs/hourglass-ydb/ut/test-results/hourglass-ydb-ut/testing_out_stuff
[not_launched] ru.yandex.direct.hourglass.ydb.schedulerinstances.YdbScheduleInstancesRepositoryTest::isLeader_LoaderBorderNotReachedTest() [default-linux-x86_64-release] (0.00s) Test was not launched, because other tests have used all allotted time (60 s)
Logsdir: http://proxy.sandbox.yandex-team.ru/2459331952/direct/libs/hourglass-ydb/ut/test-results/hourglass-ydb-ut/testing_out_stuff
[not_launched] ru.yandex.direct.hourglass.ydb.schedulerinstances.YdbScheduleInstancesRepositoryTest::IsActiveTest() [default-linux-x86_64-release] (0.00s) Test was not launched, because other tests have used all allotted time (60 s)
Logsdir: http://proxy.sandbox.yandex-team.ru/2459331952/direct/libs/hourglass-ydb/ut/test-results/hourglass-ydb-ut/testing_out_stuff
[not_launched] ru.yandex.direct.hourglass.ydb.schedulerinstances.YdbScheduleInstancesRepositoryTest::getPingInstanceTest() [default-linux-x86_64-release] (0.00s) Test was not launched, because other tests have used all allotted time (60 s)
Logsdir: http://proxy.sandbox.yandex-team.ru/2459331952/direct/libs/hourglass-ydb/ut/test-results/hourglass-ydb-ut/testing_out_stuff
[not_launched] ru.yandex.direct.hourglass.ydb.schedulerinstances.YdbScheduleInstancesRepositoryTest::markInstanceAsNotMainTest() [default-linux-x86_64-release] (0.00s) Test was not launched, because other tests have used all allotted time (60 s)
Logsdir: http://proxy.sandbox.yandex-team.ru/2459331952/direct/libs/hourglass-ydb/ut/test-results/hourglass-ydb-ut/testing_out_stuff
[not_launched] ru.yandex.direct.hourglass.ydb.schedulerinstances.YdbScheduleInstancesRepositoryTest::isLeaderTest_ExpiredInstancesRemovedTest() [default-linux-x86_64-release] (0.00s) Test was not launched, because other tests have used all allotted time (60 s)
Logsdir: http://proxy.sandbox.yandex-team.ru/2459331952/direct/libs/hourglass-ydb/ut/test-results/hourglass-ydb-ut/testing_out_stuff
------ TIMEOUT: 37 - NOT_LAUNCHED direct/libs/hourglass-ydb/ut
```

{% endcut %}

Здесь видно, что не были запущены тесты в модуле **direct/libs/hourglass-ydb/ut**.

Поиском по `[timeout] ` можно определить имена тестов которые не закончились в отведённое время. Имя модуля написано выше.


{% cut "лог с timeout" %}

```
direct/web/ut <java> [size:medium] nchunks:4
------ [0/4] chunk ran 428 tests (total:683.73s - setup:0.64s recipes:77.60s test:601.59s recipes:3.61s)
Suite exceeded 600s timeout and was killed

  PART OF THE LOG WAS DELETED TO KEEP COMPACT ENOUGH FOR THE DOC

Log: http://proxy.sandbox.yandex-team.ru/2463218148/direct/web/ut/test-results/web-ut/chunk0/testing_out_stuff/ru.yandex.direct.web.entity.uac.controller.UacCampaignTargetStatusControllerTest.startUacNonDraftCampaignForbidden_WithDirectId.log
Logsdir: http://proxy.sandbox.yandex-team.ru/2463218148/direct/web/ut/test-results/web-ut/chunk0/testing_out_stuff
[good] ru.yandex.direct.web.entity.uac.controller.UacCampaignTargetStatusControllerTest::stopUacNonDraftCampaignSuccess_WithDirectId [default-linux-x86_64-release] (11.23s)
Log: http://proxy.sandbox.yandex-team.ru/2463218148/direct/web/ut/test-results/web-ut/chunk0/testing_out_stuff/ru.yandex.direct.web.entity.uac.controller.UacCampaignTargetStatusControllerTest.stopUacNonDraftCampaignSuccess_WithDirectId.log
Logsdir: http://proxy.sandbox.yandex-team.ru/2463218148/direct/web/ut/test-results/web-ut/chunk0/testing_out_stuff
[not_launched] ru.yandex.direct.web.entity.uac.controller.UacCampaignUpdateControllerTest::updateEmptyCampaignName [default-linux-x86_64-release] (0.00s)
Test was not launched, because other tests have used all allotted time (600 s)
List of the tests involved in the launch:
ru.yandex.direct.web.entity.uac.controller.UacCampaignUpdateControllerTest::updateTooManyMinusKeywords (good) duration: 67.24s
ru.yandex.direct.web.entity.uac.controller.UacCampaignUpdateControllerTest::updateStartedCampaign_IsObsoleteIsTrue (good) duration: 35.82s
ru.yandex.direct.web.entity.uac.controller.UacCampaignControllerCreateUcTest::create uc campaign with contents (good) duration: 23.37s
ru.yandex.direct.web.entity.uac.controller.UacCampaignCreateControllerTest::createUacCampaignTest_WithoutRegionsTextsAndTitles (good) duration: 22.68s
ru.yandex.direct.web.entity.uac.controller.UacCampaignUpdateControllerTest::updateModeratingCampaignWithoutBanners_IsObsoleteIsFalse (good) duration: 21.31s
ru.yandex.direct.web.entity.uac.controller.UacCampaignGrutUpdateControllerTest::updateTooManyMinusKeywords (good) duration: 19.23s
ru.yandex.direct.web.entity.uac.controller.UacCampaignControllerUpdateUcTest::update campaign permalink become unavailable with USE_BANNERS_ADD_UAC_TGO_UPDATE_PREVALIDATION property (good) duration: 18.12s
ru.yandex.direct.web.entity.uac.controller.UacCampaignControllerUpdateUcTest::update uc campaign without contents (good) duration: 16.85s
ru.yandex.direct.web.entity.uac.controller.UacCampaignUpdateControllerTest::updateEmptyTitles (timeout) duration: 14.94s
ru.yandex.direct.web.entity.inventori.service.CampaignInfoCollectorPageIdsTest::getModeratedPagesAndBanners_1000AdGroups_AllModerated (good) duration: 13.68s
333 more tests with 185.57s total duration are not listed.
Logsdir: http://proxy.sandbox.yandex-team.ru/2463218148/direct/web/ut/test-results/web-ut/chunk0/testing_out_stuff
[timeout] ru.yandex.direct.web.entity.uac.controller.UacCampaignUpdateControllerTest::updateEmptyTitles [default-linux-x86_64-release] (14.94s)
Killed by timeout (600 s)
List of the tests involved in the launch:
ru.yandex.direct.web.entity.uac.controller.UacCampaignUpdateControllerTest::updateTooManyMinusKeywords (good) duration: 67.24s
ru.yandex.direct.web.entity.uac.controller.UacCampaignUpdateControllerTest::updateStartedCampaign_IsObsoleteIsTrue (good) duration: 35.82s
ru.yandex.direct.web.entity.uac.controller.UacCampaignControllerCreateUcTest::create uc campaign with contents (good) duration: 23.37s
ru.yandex.direct.web.entity.uac.controller.UacCampaignCreateControllerTest::createUacCampaignTest_WithoutRegionsTextsAndTitles (good) duration: 22.68s
ru.yandex.direct.web.entity.uac.controller.UacCampaignUpdateControllerTest::updateModeratingCampaignWithoutBanners_IsObsoleteIsFalse (good) duration: 21.31s
ru.yandex.direct.web.entity.uac.controller.UacCampaignGrutUpdateControllerTest::updateTooManyMinusKeywords (good) duration: 19.23s
ru.yandex.direct.web.entity.uac.controller.UacCampaignControllerUpdateUcTest::update campaign permalink become unavailable with USE_BANNERS_ADD_UAC_TGO_UPDATE_PREVALIDATION property (good) duration: 18.12s
ru.yandex.direct.web.entity.uac.controller.UacCampaignControllerUpdateUcTest::update uc campaign without contents (good) duration: 16.85s
ru.yandex.direct.web.entity.uac.controller.UacCampaignUpdateControllerTest::updateEmptyTitles (timeout) duration: 14.94s
ru.yandex.direct.web.entity.inventori.service.CampaignInfoCollectorPageIdsTest::getModeratedPagesAndBanners_1000AdGroups_AllModerated (good) duration: 13.68s
333 more tests with 185.57s total duration are not listed.
Logsdir: http://proxy.sandbox.yandex-team.ru/2463218148/direct/web/ut/test-results/web-ut/chunk0/testing_out_stuff
[good] ru.yandex.direct.web.entity.uac.controller.UacCampaignUpdateControllerTest::updateModeratingCampaignWithoutBanners_IsObsoleteIsFalse [default-linux-x86_64-release] (21.31s)
Log: http://proxy.sandbox.yandex-team.ru/2463218148/direct/web/ut/test-results/web-ut/chunk0/testing_out_stuff/ru.yandex.direct.web.entity.uac.controller.UacCampaignUpdateControllerTest.updateModeratingCampaignWithoutBanners_IsObsoleteIsFalse.log
Logsdir: http://proxy.sandbox.yandex-team.ru/2463218148/direct/web/ut/test-results/web-ut/chunk0/testing_out_stuff
[good] ru.yandex.direct.web.entity.uac.controller.UacCampaignUpdateControllerTest::updateStartedCampaign_IsObsoleteIsTrue [default-linux-x86_64-release] (35.82s)
Log: http://proxy.sandbox.yandex-team.ru/2463218148/direct/web/ut/test-results/web-ut/chunk0/testing_out_stuff/ru.yandex.direct.web.entity.uac.controller.UacCampaignUpdateControllerTest.updateStartedCampaign_IsObsoleteIsTrue.log
Logsdir: http://proxy.sandbox.yandex-team.ru/2463218148/direct/web/ut/test-results/web-ut/chunk0/testing_out_stuff
[good] ru.yandex.direct.web.entity.uac.controller.UacCampaignUpdateControllerTest::updateTooManyMinusKeywords [default-linux-x86_64-release] (67.24s)
Log: http://proxy.sandbox.yandex-team.ru/2463218148/direct/web/ut/test-results/web-ut/chunk0/testing_out_stuff/ru.yandex.direct.web.entity.uac.controller.UacCampaignUpdateControllerTest.updateTooManyMinusKeywords.log
Logsdir: http://proxy.sandbox.yandex-team.ru/2463218148/direct/web/ut/test-results/web-ut/chunk0/testing_out_stuff
[not_launched] ru.yandex.direct.web.entity.uac.controller.UacContentCreateImageControllerTest::testUploadByFile [default-linux-x86_64-release] (0.00s)
Test was not launched, because other tests have used all allotted time (600 s)
List of the tests involved in the launch:
ru.yandex.direct.web.entity.uac.controller.UacCampaignUpdateControllerTest::updateTooManyMinusKeywords (good) duration: 67.24s
ru.yandex.direct.web.entity.uac.controller.UacCampaignUpdateControllerTest::updateStartedCampaign_IsObsoleteIsTrue (good) duration: 35.82s
ru.yandex.direct.web.entity.uac.controller.UacCampaignControllerCreateUcTest::create uc campaign with contents (good) duration: 23.37s
ru.yandex.direct.web.entity.uac.controller.UacCampaignCreateControllerTest::createUacCampaignTest_WithoutRegionsTextsAndTitles (good) duration: 22.68s
ru.yandex.direct.web.entity.uac.controller.UacCampaignUpdateControllerTest::updateModeratingCampaignWithoutBanners_IsObsoleteIsFalse (good) duration: 21.31s
ru.yandex.direct.web.entity.uac.controller.UacCampaignGrutUpdateControllerTest::updateTooManyMinusKeywords (good) duration: 19.23s
ru.yandex.direct.web.entity.uac.controller.UacCampaignControllerUpdateUcTest::update campaign permalink become unavailable with USE_BANNERS_ADD_UAC_TGO_UPDATE_PREVALIDATION property (good) duration: 18.12s
ru.yandex.direct.web.entity.uac.controller.UacCampaignControllerUpdateUcTest::update uc campaign without contents (good) duration: 16.85s
ru.yandex.direct.web.entity.uac.controller.UacCampaignUpdateControllerTest::updateEmptyTitles (timeout) duration: 14.94s
ru.yandex.direct.web.entity.inventori.service.CampaignInfoCollectorPageIdsTest::getModeratedPagesAndBanners_1000AdGroups_AllModerated (good) duration: 13.68s
333 more tests with 185.57s total duration are not listed.
Logsdir: http://proxy.sandbox.yandex-team.ru/2463218148/direct/web/ut/test-results/web-ut/chunk0/testing_out_stuff
[not_launched] ru.yandex.direct.web.entity.uac.controller.UacContentCreateVideoControllerTest::testUploadByUrl [default-linux-x86_64-release] (0.00s)
Test was not launched, because other tests have used all allotted time (600 s)
List of the tests involved in the launch:
ru.yandex.direct.web.entity.uac.controller.UacCampaignUpdateControllerTest::updateTooManyMinusKeywords (good) duration: 67.24s
ru.yandex.direct.web.entity.uac.controller.UacCampaignUpdateControllerTest::updateStartedCampaign_IsObsoleteIsTrue (good) duration: 35.82s
ru.yandex.direct.web.entity.uac.controller.UacCampaignControllerCreateUcTest::create uc campaign with contents (good) duration: 23.37s
ru.yandex.direct.web.entity.uac.controller.UacCampaignCreateControllerTest::createUacCampaignTest_WithoutRegionsTextsAndTitles (good) duration: 22.68s
ru.yandex.direct.web.entity.uac.controller.UacCampaignUpdateControllerTest::updateModeratingCampaignWithoutBanners_IsObsoleteIsFalse (good) duration: 21.31s
ru.yandex.direct.web.entity.uac.controller.UacCampaignGrutUpdateControllerTest::updateTooManyMinusKeywords (good) duration: 19.23s
ru.yandex.direct.web.entity.uac.controller.UacCampaignControllerUpdateUcTest::update campaign permalink become unavailable with USE_BANNERS_ADD_UAC_TGO_UPDATE_PREVALIDATION property (good) duration: 18.12s
ru.yandex.direct.web.entity.uac.controller.UacCampaignControllerUpdateUcTest::update uc campaign without contents (good) duration: 16.85s
ru.yandex.direct.web.entity.uac.controller.UacCampaignUpdateControllerTest::updateEmptyTitles (timeout) duration: 14.94s
ru.yandex.direct.web.entity.inventori.service.CampaignInfoCollectorPageIdsTest::getModeratedPagesAndBanners_1000AdGroups_AllModerated (good) duration: 13.68s
333 more tests with 185.57s total duration are not listed.
Logsdir: http://proxy.sandbox.yandex-team.ru/2463218148/direct/web/ut/test-results/web-ut/chunk0/testing_out_stuff
[not_launched] ru.yandex.direct.web.entity.uac.controller.UacContentDeleteControllerTest::deleteNonValidMoreThanUint64IdTest [default-linux-x86_64-release] (0.00s)
Test was not launched, because other tests have used all allotted time (600 s)
List of the tests involved in the launch:
ru.yandex.direct.web.entity.uac.controller.UacCampaignUpdateControllerTest::updateTooManyMinusKeywords (good) duration: 67.24s
ru.yandex.direct.web.entity.uac.controller.UacCampaignUpdateControllerTest::updateStartedCampaign_IsObsoleteIsTrue (good) duration: 35.82s
ru.yandex.direct.web.entity.uac.controller.UacCampaignControllerCreateUcTest::create uc campaign with contents (good) duration: 23.37s
ru.yandex.direct.web.entity.uac.controller.UacCampaignCreateControllerTest::createUacCampaignTest_WithoutRegionsTextsAndTitles (good) duration: 22.68s
ru.yandex.direct.web.entity.uac.controller.UacCampaignUpdateControllerTest::updateModeratingCampaignWithoutBanners_IsObsoleteIsFalse (good) duration: 21.31s
ru.yandex.direct.web.entity.uac.controller.UacCampaignGrutUpdateControllerTest::updateTooManyMinusKeywords (good) duration: 19.23s
ru.yandex.direct.web.entity.uac.controller.UacCampaignControllerUpdateUcTest::update campaign permalink become unavailable with USE_BANNERS_ADD_UAC_TGO_UPDATE_PREVALIDATION property (good) duration: 18.12s
ru.yandex.direct.web.entity.uac.controller.UacCampaignControllerUpdateUcTest::update uc campaign without contents (good) duration: 16.85s
ru.yandex.direct.web.entity.uac.controller.UacCampaignUpdateControllerTest::updateEmptyTitles (timeout) duration: 14.94s
ru.yandex.direct.web.entity.inventori.service.CampaignInfoCollectorPageIdsTest::getModeratedPagesAndBanners_1000AdGroups_AllModerated (good) duration: 13.68s
333 more tests with 185.57s total duration are not listed.
Logsdir: http://proxy.sandbox.yandex-team.ru/2463218148/direct/web/ut/test-results/web-ut/chunk0/testing_out_stuff
[not_launched] ru.yandex.direct.web.entity.uac.controller.UacContentGetControllerTest::getContentSuccessfulTest_WithImageHash [default-linux-x86_64-release] (0.00s)
Test was not launched, because other tests have used all allotted time (600 s)

  PART OF THE LOG WAS DELETED TO KEEP COMPACT ENOUGH FOR THE DOC

Logsdir: http://proxy.sandbox.yandex-team.ru/2463218148/direct/web/ut/test-results/web-ut/chunk3/testing_out_stuff
[not_launched] ru.yandex.direct.web.validation.ValidationResultConversionServiceTest::pathNotChangedIfNoConverterRegistered [default-linux-x86_64-release] (0.00s)
Test was not launched, because other tests have used all allotted time (600 s)
List of the tests involved in the launch:
ru.yandex.direct.web.entity.uac.controller.UacCampaignUpdateControllerTest::updateEmptyTitles (good) duration: 67.87s
ru.yandex.direct.web.entity.uac.controller.UacCampaignUpdateControllerTest::updateStartedCampaign_IsObsoleteIsTrue (good) duration: 37.31s
ru.yandex.direct.web.entity.uac.controller.UacCampaignControllerUpdateUcTest::update uc campaign without contents (good) duration: 27.44s
ru.yandex.direct.web.entity.uac.controller.UacCampaignTargetStatusControllerTest::startUacNonDraftCampaignForbidden_WithDirectId (good) duration: 23.43s
ru.yandex.direct.web.entity.uac.controller.UacCampaignGetDirectControllerTest::getDirectCampaignNoRightsTest (good) duration: 20.04s
ru.yandex.direct.web.entity.uac.controller.UacCampaignUpdateControllerTest::updateModeratingCampaignWithoutBanners_IsObsoleteIsFalse (good) duration: 19.94s
ru.yandex.direct.web.entity.uac.controller.UacCampaignUpdateControllerTest::updateTooManyMinusKeywords (good) duration: 15.22s
ru.yandex.direct.web.entity.uac.controller.UacCampaignControllerUpdateUcTest::update campaign permalink become unavailable with USE_BANNERS_ADD_UAC_TGO_UPDATE_PREVALIDATION property (good) duration: 14.78s
ru.yandex.direct.web.entity.uac.controller.UacCampaignTargetStatusControllerTest::stopUacNonDraftCampaignSuccess_WithDirectId (good) duration: 14.17s
ru.yandex.direct.web.entity.uac.controller.UacCampaignUpdateControllerTest::updateEmptyCampaignName (timeout) duration: 13.92s
328 more tests with 198.21s total duration are not listed.
Logsdir: http://proxy.sandbox.yandex-team.ru/2463218148/direct/web/ut/test-results/web-ut/chunk3/testing_out_stuff
------ TIMEOUT: 1384 - GOOD, 1 - FAIL, 266 - NOT_LAUNCHED, 4 - TIMEOUT, 14 - SKIPPED direct/web/ut
```

{% endcut %}


При этом сам тест помеченный [timeout] не обязательно самый проблемный, скорее дело в том, что в совокупности тесты потратили слишком много времени. Для диагностики выводится список тестов которые заняли наибольшее кол-во времени обратно отсортированный по времени выполнения. Здесь больше всех работал тест **UacCampaignUpdateControllerTest::updateTooManyMinusKeywords (good) duration: 67.24s** и это первый кандидат для диагностики.

Поиском по `Exception: `. Так можно найти падения при попытках запуска теста (которые в `TOTAL` могут быть помечены как `TIMEOUT`).

{% cut "лог с падением при попытке запуска" %}

```java
java.lang.IllegalStateException: While trying to create object of class class ru.yandex.direct.core.entity.strategy.type.withcustomperiodbudgetandcustombid.StartPreValidatorTest$Companion$TestData could not find constructor with arguments matching (type-wise) the ones given in parameters.
	at junitparams.internal.InvokeParameterisedMethod.createObjectOfExpectedTypeBasedOnParams(InvokeParameterisedMethod.java:85)
	at junitparams.internal.InvokeParameterisedMethod.castParamsFromObjects(InvokeParameterisedMethod.java:67)
	at junitparams.internal.InvokeParameterisedMethod.<init>(InvokeParameterisedMethod.java:38)
	at junitparams.internal.ParameterisedTestClassRunner.buildMethodInvoker(ParameterisedTestClassRunner.java:124)
	at junitparams.internal.ParameterisedTestClassRunner.parameterisedMethodInvoker(ParameterisedTestClassRunner.java:118)
	at junitparams.JUnitParamsRunner.methodInvoker(JUnitParamsRunner.java:448)
	at org.junit.runners.BlockJUnit4ClassRunner.methodBlock(BlockJUnit4ClassRunner.java:273)
	at junitparams.JUnitParamsRunner.runChild(JUnitParamsRunner.java:417)
	at junitparams.JUnitParamsRunner.runChild(JUnitParamsRunner.java:386)
	at org.junit.runners.ParentRunner$3.run(ParentRunner.java:290)
	at org.junit.runners.ParentRunner$1.schedule(ParentRunner.java:71)
	at org.junit.runners.ParentRunner.runChildren(ParentRunner.java:288)
	at org.junit.runners.ParentRunner.access$000(ParentRunner.java:58)
	at org.junit.runners.ParentRunner$2.evaluate(ParentRunner.java:268)
	at org.junit.runners.ParentRunner.run(ParentRunner.java:363)
	at org.junit.runners.Suite.runChild(Suite.java:128)
	at org.junit.runners.Suite.runChild(Suite.java:27)
	at org.junit.runners.ParentRunner$3.run(ParentRunner.java:290)
	at org.junit.runners.ParentRunner$1.schedule(ParentRunner.java:71)
	at org.junit.runners.ParentRunner.runChildren(ParentRunner.java:288)
	at org.junit.runners.ParentRunner.access$000(ParentRunner.java:58)
	at org.junit.runners.ParentRunner$2.evaluate(ParentRunner.java:268)
	at org.junit.runners.ParentRunner.run(ParentRunner.java:363)
	at org.junit.runner.JUnitCore.run(JUnitCore.java:137)
	at org.junit.runner.JUnitCore.run(JUnitCore.java:115)
	at ru.yandex.devtools.test.Runner.executeTests(Runner.java:150)
	at ru.yandex.devtools.test.AbstractRunner.run(AbstractRunner.java:70)
	at ru.yandex.devtools.test.AbstractRunner.run(AbstractRunner.java:109)
	at ru.yandex.devtools.test.Runner.main(Runner.java:367)
Caused by: java.lang.NoSuchMethodException: ru.yandex.direct.core.entity.strategy.type.withcustomperiodbudgetandcustombid.StartPreValidatorTest$Companion$TestData.<init>(java.lang.String, ru.yandex.direct.core.entity.strategy.type.withcustomperiodbudgetandcustombid.StartPreValidatorTest$Companion$TestData)
	at java.base/java.lang.Class.getConstructor0(Class.java:3349)
	at java.base/java.lang.Class.getConstructor(Class.java:2151)
	at junitparams.internal.InvokeParameterisedMethod.createObjectOfExpectedTypeBasedOnParams(InvokeParameterisedMethod.java:82)
	... 28 more
  ```

{% endcut %}

Здесь видно, что упал запуск теста **ru.yandex.direct.core.entity.strategy.type.withcustomperiodbudgetandcustombid.StartPreValidatorTest**.

TODO: Чем отличаются [timeout] от [not_launched] ? Верно ли что [timeout] - это тест, который успели запустить, но в процессе его выполнения закончилось время и поэтому он был killed, а [not_launched] - это тест, который и не пытались запускать, потому что время уже истекло?

## Как перезапустить тесты определенных модулей
Для этого нужно:
1. склонировать (кнопкой clone) упавшую задачу
   ![sandbox screenshot](_includes/clone.png "кнопка clone" =728x247)
1. найти `Targets (semicolon separated)(targets):`, вписать туда через точку с запятой имена модулей, в которых нужно запускать тесты.
   На примере тестов из предыдущего абзаца это будет:
   ```
   direct/libs/async-http/ut;direct/libs/hourglass-ydb/ut
   ```
1. нажать слева-снизу кнопку **Run**

## Критерий приёмки

Все FAIL, TIMEOUT, NOT_LAUNCHED и SKIPPED тесты должны быть разобраны.

### Разбор SKIPPED тестов

SKIPPED тесты требуют разбора, только если есть надпись "SOME TESTS DIDN'T RUN DUE TO BUILD ERRORS". 

Тест может попасть в SKIPPED по двум причинам

1. он не скомпилировался (и в таком случае будет надпись "SOME TESTS DIDN'T RUN DUE TO BUILD ERRORS")
1. он помечен Ignored

Если есть тесты, которые не скомпилировались, нужно понять почему так случилось и критично ли это для релиза.
