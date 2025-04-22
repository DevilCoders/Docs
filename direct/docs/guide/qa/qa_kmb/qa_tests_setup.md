# Установка тулов для работы с автотестами и асессорами

## Установить IDE
Можно любую, которая вам нравится. Несколько примеров:
* [Webstorm](https://www.jetbrains.com/ru-ru/webstorm/)
* [Idea](https://www.jetbrains.com/ru-ru/idea/download)
* [VS Code](https://code.visualstudio.com/download)

## Arcadia для Mac и Ubuntu
Для работы с тестами, асессорами и кодом через Аркадию необходимо установить всё необходимое.
[Официальный Guide](https://docs.yandex-team.ru/devtools/intro/quick-start-guide)

## Arcadia для Windows. Решение проблем
Для работы с тестами, асессорами и кодом через Аркадию необходимо установить всё необходимое. Во всех пунктах выбрать раздел "Windows"
[Официальный Guide](https://docs.yandex-team.ru/devtools/intro/quick-start-guide)


### Решение наиболее популярных проблем

**Не удается включить ProjFS, скачать Arc**<br>

Убедитесь, что вы открыли PowerShell под администратором. <br>

**Консоль ругается на проблемы с ключом**<br>

Скорее всего какие-то проблемы с файлом *token*. Варианты их решения:<br>
- проблемы с кодировкой в системе. Проверить кодировку:<br>
`chcp` <br>
Проставить кодировку UTF-8<br>
`chcp 65001` <br>
- Неправильно сгенерировался файл *token* <br>
Откройте на просмотр файл *token*. В нем должен быть только токен, без всяких дополнительных подписей типа "ARC_TOKEN="
- Неправильная кодировка файла *token* <br>
Откройте файл (через текстовый редактор или через IDE). Уберите лишние переносы строк и пробелы, сохраните с кодировкой UTF-8 <br>

**'arc mount -m arcadia' завершается ошибкой**<br>

Скорее всего дело в отключенных длинных путях в Windows. Чуть подробнее описано [здесь](https://wiki.yandex-team.ru/arcadia/arc/faq/#proizoshlavnutrennjajaoshibkaimontirovanieupalo) <br>
Как решить проблему - описано [здесь](https://docs.microsoft.com/en-us/windows/win32/fileio/maximum-file-path-limitation?tabs=powershell#enable-long-paths-in-windows-10-version-1607-and-later) <br>
### 

## Локальный запуск e2e автотестов
Для локального запуска тестов на системах Mac, Ubuntu можно воспользоваться стандартной консолью. Для Windows рекомендуется пользоваться встроенной в нее системой "Ubuntu" из Microsoft Store ([пример подходящей убунты на 15.03.2022](https://www.microsoft.com/en-gb/p/ubuntu-20044-lts/9mttcl66cpxj?activetab=pivot:overviewtab)) или DualBoot, которую настраивали выше

0) Если у вас Windows. Заводя нового пользователя в установленной Ubuntu, необходимо указать имя пользователя, совпадающее с вашим доменным логином. Иначе будет проблемы с ключами.

1) Если у вас Windows(для macOS и отдельной Ubuntu делать не нужно), то зайдя в "Ubuntu" необходимо разложить ключи как в [инструкции](https://wiki.yandex-team.ru/users/jensenspb/sshformac/) <br>
Или вместо этого из консоли Ubuntu:<br>
По сути, их нужно скопировать из текущего места, где они лежат (как правило, в корне своего пользователя в системе Windows). Положить нужно в папку .ssh внутри Ubuntu <br>
`scp /mnt/c/Users/sudar/.ssh/id_rsa ~/.ssh` <br>
`scp /mnt/c/Users/sudar/.ssh/id_rsa.pub ~/.ssh` <br>
`cd .ssh` <br>
`chmod 700 ~/.ssh; chmod 600 ~/.ssh/id_rsa; chmod 644 ~/.ssh/id_rsa.pub` <br>

После этого закрываем и открываем консоль ubuntu <br>

2) Необходимо установить nodejs и pnpm версий, поддерживаемых в проекте автотестов. Ниже пример, как это можно сделать, используя консоль операционной системы или "Ubuntu" для Windows.

 Установить nvm <br>
Windows | Ubuntu: <br>
`wget -qO- https://raw.githubusercontent.com/creationix/nvm/v0.33.5/install.sh | bash` <br>
MacOS: <br>
`brew install nvm`<br>
После этого закрываем и открываем консоль ubuntu<br>

2) Установить nodejs необходимой версии. Текущая версия - 16.13.2. Также нужно сделать ее используемой по умолчанию <br>
`nvm install 16.13.2` <br>
`nvm use alias default 16.13.2` <br>
После этого закрываем и открываем консоль ubuntu

3) Установить pnpm необходимой версии. Текущая версия - 6.32.3 <br>
`npm install --registry=https://npm.yandex-team.ru --global pnpm@6.32.3` <br>

4) Если еще не установлен JDK, то установить его из [инструкции](https://www.digitalocean.com/community/tutorials/how-to-install-java-with-apt-on-ubuntu-20-04-ru)

5) Если Arcadia не замунчена, то маунтим `arc mount -m arcadia`<br>

6) Переходим в директорию с тестами например `cd arcadia/adv/frontend/services/dna` и выполняем <br>
`pnpm i` <br>
**или** последовательно в 2 команды <br>
`pnpm run clean-deps` <br>
`pnpm run install:deps` <br>
Добавлю, что на Windows вторая команда по установке может падать при выполнении процесса. Повторный запуск, как правило, помогает. Иногда нужно выполнить несколько раз, в итоге с какой-то итерации успешно проходит. <br>
В процессе выполнения может возникнуть ошибка `Git not found`<br>
Выполняем `sudo apt install git`, а затем `pnpm i --filter {.}...`<br>

6) Для Ubuntu и MacOs устанавливаем браузер Сhrome версией не позднее чем 86. На MacOS не забыть отключить автообновление браузера! <br>

7) Открываем новое окно в терминале и выполняем `npm run selenium`. В первый раз команда выполнит установку нужной версии Селениума <br>

8) Для локального запуска автотестов должно быть открыто два окна терминала <br>
В первом выполняем команду `npm run selenium`<br>
Во втором `npm run hermione:standalone gui` <br>

Для Windows есть проблемы с запуском standalone, можно попробовать из директории dna запустить тесты удаленно:
`pnpm run hermione gui -- --grep='Поиск клиента по логину'`

Основные команды для работы с тестами можно найти [здесь](https://a.yandex-team.ru/arc_vcs/adv/frontend/services/dna/docs/functional-tests.md#zapustitь-vse-testy-v-interaktivnom-rezhime) <br>

Страничка с вопросами и ответами по автотестам [здесь](https://wiki.yandex-team.ru/users/ayevttukh/test-education)

{% note tip %}

Если при вводе `nvm [something]` появляется ошибка вида `command not found`, следует в файл ~/.bash_profile добавить следующее:<br>
`export NVM_DIR="$HOME/.nvm"`<br>
`[ -s "/usr/local/opt/nvm/nvm.sh" ] && \. "/usr/local/opt/nvm/nvm.sh"  # This loads nvm`<br>
`[ -s "/usr/local/opt/nvm/etc/bash_completion.d/nvm" ] && \. "/usr/local/opt/nvm/etc/bash_completion.d/nvm"  # This loads nvm bash_completion`

После перезагружаем терминал или запускаем команду `source ~/.nvm/nvm.sh`

{% endnote %}

--
<br>
В случае неактуальности информации на данной странице можно обращаться к [Олегу Судареву](https://staff.yandex-team.ru/sudar)
