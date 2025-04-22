# Tools

## [reregister-fr.ipynb](./reregister-fr.ipynb)

Jupyter Notebook с утилитой для автоматической перерегистрации касс.

Требуются разнообразные и экзотические зависимости:

```sh
mkvirtualenv -p python2 fiscal-jupyter
pip install jupyter
pip install -r ~/work/repos/darkspirit/requirements.txt
pip install -e ~/work/repos/darkspirit/
```

## [fill_cash_registers_ds_state.py](./fill_cash_registers_ds_state.py)

Скрипт миграции логического состояния касс из legacy данных.
Запускать скрипт нужно из virtualenv darkspirit.