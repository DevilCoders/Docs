# Экспорт C++ в неаркадийный PyTorch
Библиотека для экспорта C++ кода в неаркадийный python пакет для использования в нейросетевых обучалках. Мы специально написали "PyTorch", потому что неаркадийный C++ заточен на то, что он будет грузиться торчовыми примитивами jit компиляции. Аркадийный же код может деплоиться в любой неаркадийный питон.

## Встраивание C++ в питон. pybind11
Начнем мы с общих вещей, а именно инструмента встраивания C++ кода в питон. В целом, известны следующие способы:
1. Ручное программирование с импортом кишочков CPython и последующая сборка .so, которая автоматом становится модулем. Лютый хардкор, ручное слежение за всеми Py_DecRef и тд. По такому пути сначала шел PyTorch, но с течением времени они все-таки оторвали бОльшую часть "нативной" интеграции в питон в пользу подхода C++ + pybind11.
2. [cffi](https://cffi.readthedocs.io/en/latest/) - подходит для небольших функций без зависимостей, для больших проектов не годится.
3. Cython. Достаточно популярный инструмент, который, тем не менее, для подавляющего большинства пользователей занимается "магией" и является самостоятельным языком программирования. Учитывая, что люди не тратят всю свою карьеру на написание биндингов, их познания этого отдельного языка программирования всегда оставляют желать лучшего, из-за чего многие действия делаются криво/переусложненно/велосипедятся.
4. pybind11. Самый современный инструмент, являющийся просто библиотекой на C++. Весь код биндингов в питон делается целиком на C++ без "магии отдельного языка программирования". Поддержаны все фишки питона (pickle/unpickle, magic методы, buffer protocol с zero-copy stringview из C++ в питон и тд)
5. Arcadia PyBind. Требует на порядок больше boilerplate чем любой из описанных выше подходов, из-за чего биндинги больших библиотек на C++ превращаются в астрономическую боль

Мы остановились на pybind11, потому что:
1. Только его поддерживает pytorch
2. Он намного удобнее cython (наше оценочное суждение, но мы правы, инфа 100%). Авторы писали большие биндинги и на cython, и на pybind11
3. Вам нужно изучить всего один инструмент и использовать его как для аркадийного, так и для неаркадийного C++

## Основные функции библиотеки

## Неаркадийный C++
Выше мы уже сказали, что неаркадийный C++ для pytorh **обязан** использовать pybind11. Для начала предлагаем вашему вниманию библиотечку [nonarcadia_example_package](TODO ССЫЛКА).

Что у нас тут есть:
* setup.py - к нему вернемся в последнюю очередь
* пакет nonarcadia_example_package c файлом `__init__.py`, импортирующим C++ модуль, и собственно код модуля `module.cpp`.

Для начала взглянем на код модуля, в нем всего две тривиальные функции, чтобы ничто не отвлекало наше внимание:
```cpp
#include <pybind11/pybind11.h>

uint64_t GetStaticInteger() noexcept {
    return 42;
}

// Python Module building
PYBIND11_MODULE(TORCH_EXTENSION_NAME, m) {
    m.def("GetStaticInteger", &GetStaticInteger);
    m.def("Add42ToInteger", [](uint64_t value) { return value + 42; });
}
```

Теперь перейдем к `__init__.py`. Вообще, в pytorch можно деплоить C++ код двумя способами:
1. Компилировать его в setup.py на виртуалке. с которой вы запускаете, и отправлять .whl в Нирвану/yt
2. Ничего не компилировать, а просто собирать исходники и компилировать уже на машинке средствами `torch.utils.load_cpp_extension`

Мы выбрали второй способ, потому что:
1. PyTorch сам следит за тем, чтобы ваш код скомпилировался и слинковался с теми библиотеками, которые используются в самом торче, и гарантирует вам что скомпилированный код будет работать с торчом
2. PyTorch снимает с вас всю нагрузку по поиску инклудов/LD_PRELOAD'ов на все множество нужных зависимостей
3. В 99.99% случаев пользователи запускают обучение с виртуалок в граф Нирваны и с виртуалок же грузят туда код. Если вы компилируете ваш C++ код на виртуалке, вы обязаны следить за консистентностью библиотек на вашей VM с контейнером в Нирване. Для JIT компиляции требования гораздо мягче
4. При локальной отладке не нужно постоянно пересобирать-переустанавливать пакет с помощью setup.py, а можно пользоваться кешом сборки ninja (система сборки под капотом `torch.utils.load_cpp_extension`). В этом случае, flow разработки практически не отличается от разработки в аркадийной сборке

Вернемся к `__init__.py`. Чтобы собрать неаркадийный C++ модуль и проимпортировать его, надо вызвать `cached_load_torch_cpp_extension`:
```python
import os
from cpp_extension_tools import (
    cached_load_torch_cpp_extension,
    get_cpp_sources_list_from_folder,
    get_default_cpp_cflags
)

cpp_module_nonarcadia = cached_load_torch_cpp_extension(
    # имя модуля. В целом, может быть любым, главное - уникальным top-level именем package
    name="example_nonarcadia_package",
    # Функция, которая берет путь до папочки и выгрепывает все файлы с расширениями .cpp, .c и .cu
    # В нашем случае, мы положили C++ код туда же, куда и __init__.py
    sources=get_cpp_sources_list_from_folder(folder=os.path.dirname(__file__)),
    # Если вы в ваш C++ код засовываете внешние зависимости с relative инклюдами, вам потребуется
    # прописывать пути для поиска include файлов. Аналог ADDINCL в ya.make, если кроме ya.make вы ни с чем не работали
    extra_include_paths=[],
    # Всякая дефолтная всячина вроде -Wall, -O3, etc. Ознакомьтесь с ним. Если вы жертва аркадии - внезапно, для C++ важно проставлять флаги компиляции.
    # Обратите особое внимание на флаг -march=native - прямое следствие того, что мы компилируем код всегда
    # на той машине, на которой запускаем. Иначе пришлось бы руками прописывать всякие -mavx и тд
    extra_cflags=get_default_cpp_cflags(),
    verbose=True
)
```

Остался последний штрих - кеш сборки. Кеш нужен и для локального запуска, и для запуска в Нирване:
1. Для локального запуска нужен по понятным причинам - не пересобирать заново кучу кода с зависимостями
2. В Нирване уже менее очевидно - большинство обучалок так или иначе используют multiprocessing. cuda не работает с fork и работает только с forkserver/spawn контекстами. Не вдаваясь в технические детали, они оба стартуют "чистый" новый процесс и передают туда запикленную функцию. Это значит, что кеш импорта модулей в питоне сбрасывается и каждый процесс будет пытаться компилировать ваш код заново, в лучшем случае сильно замедляя старт, в худшем - получая кривую сборку, если вдруг блокировки разных процессов на одну и ту же папку сборки не сработают. Чтобы делать кеш сборки в spawn, мы дополнительно автоматически проставляем правильные переменные окружения внутри процесса.

Чтобы заиметь персистентный кеш, можно выставить переменную `CACHED_CPP_EXTENSION_BUILD_DIR`. Для каждого модуля здесь будет своя подпапка, т.к. можно один раз в `.bashrc` проставить эту переменную и забыть про нее, все будет работать для разных C++ модулей без коллизий.

Если переменная `CACHED_CPP_EXTENSION_BUILD_DIR` не выставлена, то кеш едет в подпапочку текущей `cwd`. Для локальной разработки подход не годится, для Нирваны в самый раз.

## Аркадийный C++
### Структура C++ кода
Настоятельно рекомендуется сегрегировать ваш код в чисто C++ библиотеку с юнит-тестами на плюсах и отдельный модуль `export`. Использование `pybind` должно быть локализовано строго в этом модуле `export`.
Пример:
* C++ библиотека [embedding_model](https://a.yandex-team.ru/arc/trunk/arcadia/ads/pytorch/embedding_model/cpp_lib)
* Чисто C++ тесты в [ut](https://a.yandex-team.ru/arc/trunk/arcadia/ads/pytorch/embedding_model/ut)
* Модуль на экспорт [export](https://a.yandex-team.ru/arc/trunk/arcadia/ads/pytorch/embedding_model/export)

### Написание модуля на экспорт. Сборка
Сам код модуля пишется ровно по тем же правилам, что и в неаркадийных плюсах с использванием `pybind11` [пример](https://a.yandex-team.ru/arc/trunk/arcadia/ads/pytorch/embedding_model/export/module.cpp), в этом смысле все здорово.

А вот для сборки потребуется уже куда больше магии, чем для неаркадийного кода. Для начала - пишем специальный [symlist](https://a.yandex-team.ru/arc/trunk/arcadia/ads/pytorch/embedding_model/export/my_symlist) файл. Необязательно знать, зачем он нужен, содержание можно получить таким кодом:
```python
fmt = """
{
    global: PyInit_{module_name}; init_{module_name};
    local: *;
};
"""

# Напечатает нужное содержимое файла. module_name определим ниже
print(fmt.format(module_name="pytorch_embedding_model_arcadiacpp"))
```

Затем - пишем ya.make
```
# обязан быть таким же, как в symlist. Это же имя мы потом будем использовать для импорта:
# import pytorch_embedding_model_arcadiacpp
# Тип артефакта должен быть PY3MODULE
PY3MODULE(pytorch_embedding_model_arcadiacpp)

EXPORTS_SCRIPT(my_symlist)  # ссылаемся на наш магический файл. Больше он нам нигде не потребуется

OWNER(alxmopo3ov)

PEERDIR(
    contrib/libs/pybind11  # обязательный peerdir на аркадийный pybind11
    # ну и все остальные ваши пирдиры
    ads/pytorch/embedding_model/cpp_lib
)

SRCS(
    module.cpp
)

END()
```

С аркадийной частью пока все, перейдем к использованию кода. Здесь у нас появляется куда более явное различие между локальной отладкой на виртуалке и работой в Нирване. Для работы в Нирване, нам недоступна опция jit сборки кода, а значит, мы начинаем страдать от вопросов совместимости библиотек.

Хорошая новость заключается в том, что аркадия - монолит, в ней единственная версия cuda/cudnn/etc. и примерно все контейнеры для запуска нейросетевых обучалок совместимы с версиями библиотек из аркадии.

Плохая новость заключается в том, что модуль на экспорт собирается специальной ya.make командой, которая линкуется **не с аркадийным питоном, а с внешним**. В коде это выражено так [TODO ссылка](FAILLOL). Это значит, что вам на машинке, на которой вы собираете, нужен такой же питон, который будет в контейнере. Разжиться голым питоном несложно, достаточно поставить [anaconda](https://www.anaconda.com/) нужной версии.

Перейдем теперь к импорту аркадийного кода. Будем рассматривать сразу "боевой пример" embedding_model. Импорт устроен так:
```python
from cpp_extension_tools import cached_load_arcadia_extension
import os

# Третье (!) место, в котором мы должны консистентно указать нужный нам module_name
ARCADIA_MODULE_NAME = "pytorch_embedding_model_arcadiacpp"
# Путь от корня аркадии до папочки с export модулем
ARCADIA_MODULE_RELATIVE_PATH = "ads/pytorch/embedding_model/export"
# Пример для анаконды: /home/alxmopo3ov/anaconda3/include/python3.8
# ОБЯЗАН быть != None на машине, на которой вы собираете код
# None допускается только если вы устанавливаете колесо .whl с предкомпилированной аркадийной .so
PYTHON_INCLUDE_PATH = os.environ.get("PYTORCH_EMBEDDING_PYTHON_INCLUDE_PATH", None)
# Путь до папочки, в которую setup.py сложит предкомпилированную .so, чтобы при ее наличии
# проимпортировать именно ее
EXTERNAL_PREBUILDED_PATH = os.path.join(os.path.dirname(__file__), "prebuilded_arcadia")

# Помимо кешей аркадии, имеется аналогичный кеш с переменными окружения для кеширования в spawn multiprocessing context
cpp_module_arcadia = cached_load_arcadia_extension(
    external_prebuilded_path=EXTERNAL_PREBUILDED_PATH,
    arcadia_module_name=ARCADIA_MODULE_NAME,
    library_path_relative_to_arcadia_root=ARCADIA_MODULE_RELATIVE_PATH,
    python_include_path=PYTHON_INCLUDE_PATH,
    need_cuda=True  # Если True, то ваша библиотека еще должна делать PEERDIR(build/platform/cuda)
)
```

Если вы локально дебажите или разрабатываете ваш код, то **не рекомендуется** устанавливать его setup.py в ваше окружение. Рекомендуется прописать до него путь в PYTHONPATH. В таком случае, на каждый импорт будет запускаться команда ya.make, все ваши свежие изменения всегда будут подтягиваться. Flow разработки не отличается от аркадийного.

С локальным использованием модуля мы закончили, перейдем к деплою в Нирвану. Для этого нужно написать правильный `setup.py`:
```python
from __future__ import unicode_literals
from setuptools import setup, find_packages

import os
import distutils
import distutils.log
from setuptools.command.build_py import build_py
from pytorch_embedding_model.cpp_lib import (
    ARCADIA_MODULE_NAME,
    ARCADIA_MODULE_RELATIVE_PATH,
    PYTHON_INCLUDE_PATH,
    EXTERNAL_PREBUILDED_PATH
)
from cpp_extension_tools import cached_load_arcadia_extension


class BuildPyCommand(build_py):
    def run(self):
        build_py.run(self)

        # This will definetely build it inside relative path
        self.announce(f'Building arcadia module: {ARCADIA_MODULE_NAME}', level=distutils.log.INFO)

        # Используем ту же самую функцию для сборки модуля
        arc_module = cached_load_arcadia_extension(
            external_prebuilded_path=None,
            arcadia_module_name=ARCADIA_MODULE_NAME,
            library_path_relative_to_arcadia_root=ARCADIA_MODULE_RELATIVE_PATH,
            python_include_path=PYTHON_INCLUDE_PATH,
            need_cuda=True
        )

        # А вот здесь место, в котором мы пока не сделали красивой схемы
        # Вы должны мувнуть собранный модуль в путь, который при импорте будет равен EXTERNAL_PREBUILDED_PATH
        move_path = os.path.join(self.build_lib, "pytorch_embedding_model", "cpp_lib", "prebuilded_arcadia")
        if not os.path.exists(move_path):
            os.makedirs(move_path)

        arc_module_file = arc_module.__file__
        self.move_file(
            arc_module_file,
            os.path.join(move_path, os.path.basename(arc_module_file))
        )


setup(
    name='pytorch_embedding_model',  # Required
    version='1.0.0',  # Required
    author='@alxmopo3ov',  # Optional
    packages=find_packages(exclude=['tests', 'bin', 'tests_lib']),  # Required
    cmdclass={"build_py": BuildPyCommand},  # Новое изменение
    include_package_data=True
)
```

### Аллокаторы
Если коротко, то с аркадийными аллокаторами беда. Использовать их "в лоб" в ya.make export библиотеки нельзя, так как биндинги будут передавать аркадийные объекты, обернутые в питон и созданные в аркадийной .so, а удаляться они могут уже в неаркадийном питоне, который ничего не знает про внутренний аллокатор .so. TCMALLOC в таком сетапе даже не импортируется, падает на старте. Остальные, вроде LF/J/HU/etc., работают до первого сегфолта с удалением C++ объекта в питон обертке.

Кроме того, эту проблему нельзя надежно решить с помощью LD_PRELOAD в неаркадийный питон. Во-первых, у нас оно не взлетело. Во-вторых, даже если у вас таки получится завести это для одной библиотеки, то тогда вам потребуется во всех возможных библиотеках трекать, чтобы там везде был один и тот же аллокатор.

Для ads/pytorch/embedding_model мы немножко порвались и пробросили руками hu аллокатор во все контейнеры библиотеки и во аллокации. Мы смогли так сделать, потому что у нас было минимум зависимостей.

В остальных случаях хорошее решение пока неизвестно :( Разве что все-таки удастся подружиться с ALLOCATOR в ya.make.
