# Интеграционные тесты

Все тесты написанны на 3 питоне. Чтобы у вас появился свежий интерпретатор, который может разрешать импорты аркадии
без проблем, нужно поставить аркадийный питон в виртульное окружение:
```bash
username@host:~$ cd /arcadia/market/mars/
username@host:~/arcadia/market/mars/$ ya ide venv --venv-root=/home/username/venv-mars
```

## Подготовка к запуску

Сейчас в каталоге `/home/username/venv-mars/bin` лежит интерпретатор питона, через который можно запускать скрипты поштучно в каталоге для марса.

Чтобы это сделать, в IDE можно прописать путь до существующего venv или прописать alias в ~/.bashrc.

## Запуск единичных тестов

### Запуск через интерпретатор

Теперь, когда свежий интерпретатор точно есть, можно запускать тесты как через ya make, так и вызывая отдельный тест, в том числе с дебагом:

```bash
username@host:~/arcadia/market/mars/$ python lite/mt/test_dsp.py -t test_dsp_offline -d
```

### Запуск через ya make

Также конкретный тест можно запустить через `ya make`

```bash
username@host:~/arcadia/market/mars/$ ya make -t -F test_dsp.py::T::test_dsp_offline
```

## Запуск всех тестов

Сейчас для запуска всех тестов можно использовать только `ya make`

```bash
username@host:~/arcadia/market/mars/$ ya make -tt
```
