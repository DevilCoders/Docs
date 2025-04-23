Implementation of simple Mobile API client for testing and debugging purposes.

### Как посылать письма пользователю

- Устанавливаем PyCharm, открываем в нем этот проект
- Устанавливаем последний Python 3, например, через Homebrew http://osxdaily.com/2018/06/13/how-install-update-python-3x-mac/
- Создаем виртуальное окружение Preferences -> Project Interpreter -> шестеренка -> Add -> New invironment -> 
В качестве Base interpreter выбираем Python 3.x -> ОК
- Устанавливаем зависимость requests через requirements.txt - можно нажать внизу Terminal и набрать там 

        pip install -r requirements.txt
  
- Открываем send_mail.py, указываем OAuth токен пользователя, от имени которого будем посылать письма
- Пкм на send_mail.py -> Run