# Команда отправки комментария в задачу

Команда позволяет отправить комментарий в задачу в стартреке о статусе проверки.
Возможна отправка комментариев трёх типов:
* Успешное завершение
* Завершение с ошибкой
* Пользовательская информация о выполнении


## Установка

Команда является частью утилиты `release-cli`.

```bash
npm install -g @yandex-int/si.ci.release-cli  --registry https://npm.yandex-team.ru
```


## Использование

Для работы необходима environment-переменная `STARTREK_TOKEN`.

```
release issue comment

Send comment to release issue rendered by specified template

Positionals:
  issue-key  startrek issue key, e.g. SEAREL-1                          [string]

Comment template
  --template  Comment message template type
                        [string] [required] [choices: "success", "fail", "info"]
  --message   User additional text in comment message                   [string]

Links
  --restart-url  Url to restart failed check                            [string]
  --report-url   Url to view check's report                             [string]
  --logs-url     Url to job logs                                        [string]
  --custom-link  Pair of link display name and url address: e.g. name=href
                                                                         [array]

Options:
  --help, -h     Show help                                             [boolean]
  --version, -v  Show version number                                   [boolean]
  --check-name   Check display name                          [string] [required]
  --optional     Adds label for optional check        [boolean] [default: false]
  --job-name     Name of the job under which the check was performed    [string]

Examples:
  issue comment FEI-12688 --template fail --restart-url https://ya.ru
  --report-url https://ya.ru --check-name "small tests"
```


### Примеры

#### Комментарий об успешном завершении проверки 'Some tests'

Тип шаблона: `--type success`.

`release issue comment --issue-key FEI-12688 --template success --check-name 'Some tests' --report-url https://come-sandbox-report`

![success](./assets/success.png)


#### Комментарий о завершении проверки 'Some tests' с ошибкой

Тип шаблона: `--type fail`.

`release issue comment --issue-key FEI-12688 --template fail --check-name 'Some tests' --report-url https://come-sandbox-report --job-name "My job" --restart-url https://some-sandbox-task --message 'Печалька'`

![fail](./assets/fail.png)


#### Комментарий с пользовательской информацией

Тип шаблона: `--type info`.

`release issue comment --issue-key FEI-12688 --template info --message "Проверка запущена." --check-name 'Some tests'`
![info](./assets/info.png)

Для всех типов комментариев может быть добавлено дополнительное сообщение (опция `--message`). Для комментария с пользовательской информацией она является обязательной.

Для всех типов комментариев могут быть добавлены ссылки:
* сыылка на отчёт (опция `--report-url`)
* ссылка на перезапуск Job (опция `--report-url`, если имя job передано через опцию `--job-name`, оно будет указано в названии ссылки )
* ссылка на логи опция (`--report-url`)
