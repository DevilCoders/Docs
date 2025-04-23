# Ymod_python

## Описание

Это модуль yplatform для использования python как встроенной среды.

Для чего?

- Возможность быстрого прототипирования функционала приложения без длительных итераций
- Возможность расширенной отладки во время работы приложения
- Возможность динамической реконфигурации логики и поведения приложения без пересборки и редеплоя     

## Использование

### Вызов питон-кода

* sync_run - выполняет переданную функцию в потоке питон-интерпретатора синхронно
* async_run - выполняет переданную функцию в потоке питон-интерпретатора асинхронно

В лямбде, переданной в sync/async_run можно временно отпустить GIL. Для этого туда нужно передать функцию,
которая принимает функцию, которая принимает функцию :)

Пример:

    namespace py = boost::python;

    void cpp_some_function(py::str file_name, py::object py_callback) {
        get_current_python()->async_run([=](auto release_GIL_and_do){
            py::extract<const char*> str(file_name);
            if (str.check()) {
                py::object result;
                FILE* f = fopen(str(), "r");
                const char *text;
                release_GIL_and_do([&]{
                    // get file size
                    // malloc text
                    // read all file to text
                });
                result = py::str(text);
                free(text);
                py::call<void>(py_callback.ptr(), result);
            }
        });
    }

sync_run нельзя вызывать из C++ кода, который был вызван из питона, иначе будет дедлок.
Так же sync_run нельзя вызывать из пула потоков питона (есть вероятность дедлока).
в async_run нельзя использовать синхронизацию с вызывающим кодом (иначе получится sync_run со всеми
вытекающими последствиями). Без синхронизации с плюсовым кодом async_run полностью безопасен.

Модель работы ymod_python рассчитана исключительно на асинхронную работу через колбэки.

Если планируется использовать долгие IO в плюсовом коде, вызываемом из питона, с временным
освобождением GIL, то лучше всего тогда использовать для питона реактор с одним пулом и
многими io потоками.

Так же ничего не мешает использовать PyEval_SaveThread/PyEval_RestoreThread функции python C API.
Но тут нужно хорошо понимать как всё работает, чтобы не получить проблем.

### Python asyncio и threading

ymod_python нормально работает с python.threading и python.asyncio при соблюдении пары моментов:

1. При создании потока threading.Thread, нужно будет в начале потока вызвать метод set_as_current() у
   объекта класса ymod_python_sys.current_python. Это нужно для того, чтобы C++ функции вызываемые из
   питоновского потока получали правильный ymod_python реактор через функцию get_current_python().
   Иначе они будут получать реактор по-умолчанию - реактор самого первого ymod_python.

2. asyncio event loop должен быть запущен в отдельном threading.Thread потоке, который не принадлежит
   пулу потоков реактора какого либо ymod_python. Иначе поток реактора будет заблокирован.

Пример:

    import asyncio
    import aiosmtpd
    from aiosmtpd.controller import Controller
    import threading
    from ymod_python_sys import current_python
    from ymod_python_json import TJsonValue
    from qmgr_dispatcher import process_job
    
    global ymod_python
    ymod_python = current_python()
    
    class ExampleHandler:
        async def handle_RCPT(self, server, session, envelope, address, rcpt_options):
            # Check address in blackbox
            envelope.rcpt_tos.append(address)
            return '250 OK'
    
        async def handle_DATA(self, server, session, envelope):
            print('Message from %s' % envelope.mail_from)
            print('Message for %s' % envelope.rcpt_tos)
            print('Message data:\n')
            print(envelope.content.decode('utf8', errors='replace'))
            print('End of message')
            job = TJsonValue()
            job.AsObject = envelope
            process_job(job)
            return '250 Message accepted for delivery'
    
    async def amain(loop):
        controller = Controller(ExampleHandler())
        controller.start()
    
    def server():
        global ymod_python
        ymod_python.set_as_current()
        try:
            loop = asyncio.new_event_loop()
            asyncio.set_event_loop(loop)
            loop.create_task(amain(loop=loop))
            loop.run_forever()
        except Exception as e:
            print("Error of smtp server: " + str(e))
    
    srv = threading.Thread(target=server, name="smtp")
    srv.start()

### Регистрация своих модулей

Можно (даже нужно!) использовать стандартные boost::python механизмы.

*get_current_python()* - получение текущего ymod_python::python в C++ функциях, вызываемых из питона.

Рекомендую для TLS посмотреть на PyThreadState_GetDict() функцию, но лучше к TLS в плюсовом коде не привязываться,
так как плюсовый код из питона может быть вызван в произвольном потоке реактора с произвольным PyThreadState.

## Конфигурация

    modules:
        module:
        -   _name: mod_python
            system:
                name: mod_python
                factory: ymod_python::impl
            configuration:
                reactor: python
                program_name: my_python
                python_home: .
                python_path: .:/usr/lib/python
                load: "module1.py"

Пояснение относительно поля **load**. Модуль, указанный в этом поле, загружается на этапе start ymod_python.
И перезагружается при вызове reload, по сигналам SIGHUP.

## ВНИМАНИЕ!

Нужно быть внимательными с работой со счётчиком ссылок у объектов Python в асинхронном коде.
По умолчанию, функции C++ вызываемые из питона получают объекты без предварительного INCREF, то есть
они объектами не владеют! И если вы запоминаете эти объекты в каком-нибуть колбэке, который должен быть вызван
асинхронно, уже после выхода из C++ функции, которая установила колбэк, обратно в питон, то может получится так,
что к моменту вызова колбэка, объект уже будет уничтожен.

Советую использовать PyObjectShared класс, так как стандартный бустовый object не оборачивает INCREF/DECREF вызовы
в GIL и иногда от этого бывает больно.

Пример работы с объектами и колбэками можно посмотреть в *deadline_timer* в libs/sys/src/sys.cc.

Настоятельно рекомендую питоновские объекты протаскивать через замыкания лямбд ввиде PyObjectShared.

Например:

    namespace py = boost::python

    void deadline_timer(py::object id, long time, py::object cb)
    {
        auto python = get_current_python();
        auto& io = python->get_io_service();
        auto timer = std::make_shared<boost::asio::deadline_timer>(io, boost::posix_time::milliseconds(time));
        timer->async_wait([id, cb, timer, python](const boost::system::error_code& ec){
            if (!ec) {
                python->async_run([cb, id] {
                    cb(id);
                });
            }
        });
    }

    BOOST_PYTHON_MODULE(mod)
    {
        def("timer", deadline_timer);
    }

Вот так будет всё хорошо:

    from mod import timer

    def cb(i):
        print(i)

    timer(None, 100, cb)

А вот так будут проблемы:

    from mod import timer

    def cb(i):
        print(i)

    timer(None, 100, lambda x: cb(x))

Вот так тоже всё взорвётся:

    from mod import timer

    def cb(i):
        print(i)

    timer((1,2,3), 100, cb)

И вот так бабахнет:

    from mod import timer

    def cb(i):
        print(i)

    timer(None, 100, cb)

    del cb


## Ещё раз ВНИМАНИЕ!

Если оборачиваете с помощью boost::python свои объекты для использования в питоне и эти объекты создаются в питоне
с политикой return_value_policy<manage_new_object>(), то в деструкторе ~object(), когда будет уничтожаться ваш
объект и ассоциированный с ним PyObject (внутри boost::python::object), будет вызван Py_DECREF()!

Подробнее про проблему можно посмотреть в дискуссии: https://github.com/boostorg/python/pull/11

Ничего страшного не будет, если это произойдёт в питон-коде (либо в коде выполняемым из async_run/sync_run).
Но! Если этот объект был замкнут в колбэке в каком-либо реакторе, то деструктор (и соотв. Py_DECREF) могут быть вызваны
асинхронно по отношению к питоновскому интерпретатору, даже (и скорее всего) в потоке без питоновского контекста.

И тут могут быть весьма неприятные последствия (segfault чаще всего).

Поэтому, для того чтобы не было подобных проблем, сделан файл ymod_python/boost_python.h, которые подменяет бустовые
функции работы с Py_INCREF/Py_DECREF на безопасные, обёрнутые в GIL.

Если делаете boost::python обёртки над своими объектами, которые могут жить в замыканиях лямбд колбэков, то настоятельно рекомендую
вместо boost/python.hpp подключать ymod_python/boost_python.h. И подключать его нужно до ymod_python/object.h и любых других,
которые могут подключить boost/python.hpp.

В целом, стоит использовать boost::python объекты только в коде, который вызывается в async_run/sync_run. Если нужно сохранить объекты
в замыкании лямбд колбэков, то стоит использовать PyObjectShared из ymod_python/include/object.h, подробнее использование
можно глянуть в ymod_python/libs/sys/src/sys.cc.

ymod_python/boost_python.h - это очень хрупкие костыли, которых стоит избегать по-максимуму.

Если известно, что shared_ptr<T>, созданный в питоне, может быть уничтожен в плюсовом коде, который будет выполнен не в
питоновском потоке (под GIL), то лучше скопировать объект ```make_shared<T>(*t)```. Это ресурсоёмко, конечно, но питон в
yplatform предполагается для прототипирования в основном, поэтому это вполне приемлемо.

## TODO

 0. Добавить тестов.
 1. Добавить возможность повесить хук на stop() основного питоновского процесса
 2. Добавить хук на reload(), чтобы можно было управлять процессом перезагрузки конфигов
