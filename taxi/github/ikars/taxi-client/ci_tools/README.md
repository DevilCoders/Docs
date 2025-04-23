# ci_tools
## Package installation
Package is already installed at `analytics-cron-sas-01.taxi.tst.yandex.net`. For local installation clone the repository, go to `taxi-client/ci_tools` and run `python setup.py install --user`.

## Description
Для минимального мониторинга наших процессов нужно использовать декоратор `report_decorator.py`. Для этого весь исполняемый код внутри скрипта нужно обернуть в одну функцию `main(...)`, которая будет вызываться при запуске скрипта.

### Как им пользоваться?

Декоратор имеет следующие параметры:
```python
report(
    author,
    file_name,
    file_path=None,
    suppress_exception=False,
    tg_bot=False,
    tg_login=None)
```

`author` - ваш логин на стаффе

`file_name` - имя скрипта, который запускается

`file_path` - путь к скрипту внутри репозитория

`suppress_exception` - флаг для подавления исключений; лучше его оставлять `False`

`tg_bot` - объект телеграм бота, которому будут присылаться ошибки; если поставить `client` все будет слаться в чатик `"taxi-client сломался"`

`tg_login` - ваш логин в телеграмме, для призыва в чатике в случае ошибки

Пример использования:
```python
from ci_tools import report

@report('ikars', 'report_decorator.py', tg_bot='client', tg_login='my_login')
def main():
    # your code here

if __name__ == '__main__':
    main()
```

### Что он сделает?

Для каждого запуска он в `stdout` напишет автора скрипта `author`, имя скрипта `file_name` и время выполнения. Это позволит в кроновских письмах быстро отыскивать нужные письма, понимать, какой скрипт сломался, и кто его автор. В случае, если функция `main` поднимет исключение, в чатик `"taxi-client сломался"` прилетит алерт с эксепшеном и будет призван `tg_login`; при этом весь `stdout` и `stderr` будет проброшен в кроновское письмо (как и было до этого).

Использование декоратора избавит вас от принтов логинов и имен файла - все произойдет автоматически!

## Tools description
TODO
