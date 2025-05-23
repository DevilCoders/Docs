Тулза для массового грепанья логов по трассировкам.

```
ya make
./trace2log grep 1587125768560/fb52ea43dfebad0d9fe1ac6d6e53bbeb
```

Смысл:
1. Получить трассировку
2. Найти там все хосты
3. Погрепать там нужные строчки лога
4. **killer-фича**: погрепать на уровне "событий", т.е. если есть стэктрейс или ещё строчки - то покажет его

Делает всё это через вызовы ssh. Трассировку получает через вызов ssh на public-е, чтобы сходить в КХ.

Использование
---------
Для удобного и быстрого использования создайте алиас:
```bash
# запишите строку в ваш .bashrc файл
alias trace2log="ya make $ARCADIA_ROOT/market/mbo/scripts/trace2log && $ARCADIA_ROOT/market/mbo/scripts/trace2log/trace2log"
# далее можно вызывать его уже из любого места как
trace2log grep 1587125768560/fb52ea43dfebad0d9fe1ac6d6e53bbeb
```

Использование под Windows
---------
Тут специфика что нужно либо настроить стандартный виндовый ssh клиент на аутентификацию приватным ключем, либо использовать например Git bash. Второй путь проще.
Также под виндой бинари не появляются в папке, где запускается билд.
Поэтому в Git Bash переходим в папку с проектом и делаем следующее:

```
ya make -o ../../../../
./trace2log grep {request_id}
```

Доп. фичи
---------
Можно посмотреть последние трассировки по модулю (но по сути за последний час-два). Полезно для ответа на вопрос "что-то но пятисотит".

Настройки
---------
Новые модули нужно добавлять в `known_modules_config.py`. Локальных настроек не требует, кроме беспарольного `ssh` в консоли.

Под вопросом/что можно улучшить
-------------------------------
- сейчас смотрится и source и target для трассировок, возможно достаточно одного
- грепать логи не на инстансах, а на logview.market.yandex.net как это предлагает tsum (чтобы можно было оочень старые трассировки смотреть)

Как открыть в IDEA
------------------
```
cd arcadia-root
ya ide idea --with-content-root-modules --local --iml-in-project-root --directory-based --project-root ~/idea-projects/trace2log market/mbo/scripts/trace2log
```
