Библиотека для запуска внешних процессов. Запуск производится из отдельного сервисного процесса, что позволяет избежать потенциальных проблем при одновременном использовании pthreads и fork.

См. примеры использования в подкаталоге examples:
1. Синхронный запуск внешней команды с указанием данных для stdin и записью выдачи в stdout.
2. Асинхронный запуск.
3. Получение файловых хэндлов для стандартных потоков ввода/вывода.

Q. Как выполнить команду через shell?
A. Запустить /bin/sh и передать нужную команду в TStartProcessParams::StdIn

Q. Как поменять лимиты для запускаемого процесса?
A. Указать адрес функции в TStartProcessParams::PreExecFn, внутри функции выполнить setrlimit(). PreExecFn будет выполнена в дочернем процессе непосредственно перед exec.
