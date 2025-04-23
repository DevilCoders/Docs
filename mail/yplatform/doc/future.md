## yplatform::future

Шаблон для реализации идеи отложенного выполнения задачи, альтернатива колбэкам. Представляет из себя пару {future, promise} работающую следующим образом:
```c++
typedef future<int> future_int;
typedef promise<int> promise_int;

future_int do ()
{
  /* результатом вычисления станет либо число типа int, либо исключение */
  promise_int prom;
  /* в данном случае устанавливаем результат заранее, в реальной программе задача вычисления может быть передана другому потоку */
  prom.set (0);
  /* promise приводится к future, и в результате образуется пара */
  return prom;
}

void bar (future_int fres)
{
  /* проверяем наличие исключения. если оно имеется, можно его повторно возбудить вызвав метод get() */
  if (fres.has_exception ())
    std::cout << "exception found!\n";
  else
    std::cout << "result: " << fres.get () << "\n";
}

void foo ()
{
  future_int fres = do ();
  /* callback будет вызван тогда, когда завершится вычисление результата. поток, в котором он будет вызван не определен */
  fres.add_callback (boost::bind (&bar, fres));
}
```

