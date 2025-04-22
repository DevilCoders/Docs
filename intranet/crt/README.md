Сборка и выкладка
------------

Используем releaser:

> ya tool releaser release

Команда выше соберет образ, запушит в registry и задеплоит в тестинг

При выкладке в продакшн создаем релизный тикет в st с привязанными к нему тикетами. Нужно помнить, что продакшн-релизы CRT проходят стадию "Согласование с HelpDesk" по соответствующей кнопке в st. Когда согласование завершено, можно двинуть собранное в production:

> ya tool releaser deploy -e crt-prod -v \<version\> -dcf="https://st.yandex-team.ru/CERTOR-\<KEY\>"

Как сгенерировать миграцию:
------------

Собираем основной бинарик:

> ya make -j6 wsgi/

Запускаем собранный бинарик с нужными переменными окружения:
> Y_PYTHON_ENTRY_POINT="intranet.crt.manage:django_main" DJANGO_SETTINGS_MODULE=intranet.crt.settings YENV_TYPE=development.migration YENV_NAME=intranet ./wsgi/crt.wsgi makemigrations

`YENV_TYPE=development.migration` нужен для подхватывания конфига базы с бэкендом sqlite


Запуск тестов:
------------

> ya make -j6 -ttt .


Шифрование приватных ключей
------------
Ключи шифруются стандартным для x509 способом.

Чтобы создать новый ключ шифрования, необходимо позвать `cryptography.fernet.Fernet.generate_key()`. Полученный
ключ нужно положить **первым** в листе `settings.CRT_PRIVATE_KEY_PASSWORDS`. Если в этой настройке находится несколько
ключей, то данные шифруются первым ключом, а для расшифровки пробуются все ключи по очереди.

Если текущий ключ скомпрометирован, то нужно сделать следующее:
* Выкатить датасорсы с `private_key_passwords = ['new_key', 'old_key']`
* Перезапустить приложение
* В shell в цикле пересохранить все сертификаты
* Выкатить датасорсы с `private_key_passwords = ['new_key']`
* Перезапустить приложение
