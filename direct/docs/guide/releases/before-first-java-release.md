# Перед первым релизом java‑приложения Директа

Предполагается, что перед своим первым релизом новый релиз-инженер послушал рассказ
кого-нибудь опытного на тему "что такое релизы в Директе и как к ним относиться".

{% note info %}

В Директе с релизами работают с разработческих серверов.

В этой и других инструкциях: при запуске команд или работе с файлами подразумевается,
что это нужно делать на [ppcdev](../../glossary/glossary.md#ppcdev)'е
(если явно не указаного другого).

{% endnote %}

Подготовительные действия заключаются в раскладывании токенов и регистрации в нужной группе Sandbox'а.

## Ключи и токены { #keys-and-tokens }

### Sandbox
Открой [ссылку](https://sandbox.yandex-team.ru/oauth),
разреши доступ,
создай папку `mkdir ~/.sandbox` и затем
сохрани токен в файл `~/.sandbox/token`.

_В [интерфейсе Sandbox](https://sandbox.yandex-team.ru) эту ссылка можно найти в меню **More** → **OAuth**._

### Трекер
Проверь, может быть токен уже лежит в файле `~/.startrek_client_token`.

Если файла нет, запусти однострочник:  
```
perl -MStartrek::Client::Easy -le 'print Startrek::Client::Easy->new()->get(key => "DIRECT-1000")->{summary};'
```  
Спросят доменный пароль, после этого токен появится где надо. 

### SSH
Проверь, что твой ssh-ключ доступен на ppcdev.  
Выполни команду `svn info svn+ssh://arcadia.yandex.ru/arc` и сравни её вывод с примером:

{% list tabs %}

- всё хорошо
  
  ```
  Path: arc
  URL: svn+ssh://arcadia.yandex.ru/arc
  Relative URL: ^/
  Repository Root: svn+ssh://arcadia.yandex.ru/arc
  Repository UUID: 41d65440-b5be-11dd-afe3-b2e846d9b4f8
  Revision: 7148332
  Node Kind: directory
  Last Changed Author: tolya-baranov
  Last Changed Rev: 7148332
  Last Changed Date: 2020-07-27 11:24:03 +0300 (Mon, 27 Jul 2020)
  ```

- есть проблемы

  ```
  svn: E210002: Unable to connect to a repository at URL 'svn+ssh://arcadia.yandex.ru/arc'
  svn: E210002: To better debug SSH connection problems, remove the -q option from 'ssh' in the [tunnels] section of your Subversion configuration file.
  svn: E210002: Network connection closed unexpectedly
  ```

{% endlist %}

Инструкция по созданию и раскладыванию ключей [на вики](https://wiki.yandex-team.ru/direct/Development/first-steps/?from=%252Fdirekt%252Fdevelopment%252Ffirst-steps%252F#sgenerirovatirazlozhitssh-kljuchi).

## Группа в Sandbox
Проверь, что твой логин есть в [составе группы DIRECT](https://sandbox.yandex-team.ru/admin/groups?name=DIRECT&limit=1).

Если его там не оказалось, попроси руководителя или знакомого коллегу из списка добавить тебя.


## Инструменты

### screen | tmux
Команды `direct-release` следует запускать из-под **screen** или **tmux**.  
Это позволит процессу не упасть из-за проблем с сетью или при засыпании ноутбука.
Потренируйся в работе с этими утилитами до сборки релиза.

Про **screen** есть [инструкция](../basics/howto_screen.md).

Базовая инструкция для **tmux**:

- выполни в терминале `tmux`, дальше действуй как обычно
- если прервалось или случайно отключилось: подключись заново к тому же ppcdev и выполни `tmux attach`
- для включения режима скроллинга нажми `ctrl+b, [`. Для выхода из режима скроллинга нажми `Esc`
- для выхода из **tmux** выполни `exit`


