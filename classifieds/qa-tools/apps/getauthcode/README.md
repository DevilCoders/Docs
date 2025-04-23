**Скрипт для поиска последнего кода аутентификации для пользователя.**

* Нужен jq и  mysql-client. Для mac-os можно установить через brew:
```
brew install mysql-client jq
```
для bash (после добавления строчки необходим перезапуск консоли): 
```
echo 'export PATH="/usr/local/opt/mysql-client/bin:$PATH"' >> ~/.bash_profile
```
для zsh (после добавления строчки необходим перезапуск консоли):  
```
echo 'export PATH="/usr/local/opt/mysql-client/bin:$PATH"' >> ~/.zshrc
```

* Нужен h2p скрипт (версия 1.4 и выше):
```
brew tap YandexClassifieds/vertis git@github.com:YandexClassifieds/homebrew-vertis.git
brew update
brew install h2p
```

подробнее про h2p - https://wiki.yandex-team.ru/vertis-admin/h2p/

* Можно искать как по номеру телефона, так и по почте
* Для поиска на проде нужен доступ к базке passport-api через h2p

**Использование:**
 * ```./get_code.sh```   ищем на тестинге для номера телефона захардкоженного в переменной searchPattern
 * ```./get_code.sh -u 1234567```  ищем последний код для пользователя 1234567
 * ```./get_code.sh -s prod -n 123456```  Ищем в проде для номера содержащего 123456
 * ```./get_code.sh -s prod -n rr.rr```  Ищем в проде для почты содержащей rr.rr