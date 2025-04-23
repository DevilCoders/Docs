# Настройка репозитория
Для запуска скриптов рекомеендуется создать вирутальное окружение с `python3.7`. 

## Пример настройки с использованием [`virtualenv`](https://virtualenv.pypa.io/en/stable/userguide/)

1. Создайте виртуальное окружение `virtualenv -p python3.7 <path_to_dir_where_env_will_be_stored>`
2. Активируйте  `source <path_to_the_dir/bin/activate>` (для windows: `<path_to_the_dir\Scripts\activate>`), для выхода используйте команду `deactivate` 
3. Установите необходимые пакеты запустив `pip install -i https://pypi.yandex-team.ru/simple/ -e ./` из корня репозитория

## Jupyter Notebook
Большая часть кода написана в [`jupyter notebook`](https://jupyter.org/install) (нужные пакеты указаны в файле requirements.txt).
Нужно поднять сервер Jupyter Notebook. 

1. Выполните команду `jupyter notebook --port 3040 --port-retries=0 --ip='*' --no-browser`. Теперь вы можете зайти в браузере на страницу [http://localhost:3040/tree](http://localhost:3040/tree) и увидеть проводник. Корневой папкой будет та, находясь в которой, вы выполнили команду запуска.
2. Добавьте в `jupyter notebook` созданное ранее виртуальное окружение как новый `Kernel`.
Находясь в виртуальном окружении в терминале выполните команду
`python -m IPython kernel install --user --name=<name_of_kernel>`.  
Теперь вы можете переключиться на нужное ядро через `Kernel` > `Change kernel` прямо в открытом ноутбуке с кодом.
Рекомендуемое название для ядра -- `goab_kernel`
