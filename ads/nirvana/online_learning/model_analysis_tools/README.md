Данная папка предназначена для удобной отрисовки графиков моделей 
после подсчета метрик с помощью online_learning_factoreval. Она позволяет 
выбирать некоторое подмножество моделей по какой-то сетке параметров и рисовать 
красивые графики.

Как пользоваться, если вы работаете на удаленном сервере:
1. На сервере вызываем команду jupyter notebook --no-browser --port=<<port>>
2. На ноутбуке: ssh -N -f -L localhost:<<port>>:localhost:<<port>> <<username>>@<<server_name>>
3. Открываем любой браузер и вбиваем в поисковую строку localhost:<<port>>

Пример:
1. Сервер (bsmr-dev01i.yandex.net): jupyter notebook --no-browser --port=8999
2. Ноутбук: ssh -N -f -L localhost:8999:localhost:8999 alxmopo3ov@bsmr-dev01i.yandex.net
3. Браузер localhost:8999

Если разрабатываете на ноуте, то просто вызовите jupyter notebook в этой папке

После того, как вы открыли notebook, вбейте:

    %matplotlib inline
    from model_analysis_tools import *

Пользуйтесь.