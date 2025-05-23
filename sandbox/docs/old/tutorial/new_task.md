Вам предстоит добавить в Sandbox новую задачу под названием `HELLO_%LOGIN%` где `%login%` — ваш логин на Стаффе. Она принимает на вход логин человека и создаёт ресурс с Markdown файлом, в котором приветствует этого человека.

Запустите команду:

```bash
arcadia$ sandbox/scripts/tutorial/start
```

В репозитории будет создана директория с кодом новой задачи. Файловую структуру и сам код мы внимательно рассмотрим в следующих разделах. Пока же вам нужно просто закоммитить новый код в репозиторий.

Добавьте код новой задачи в вашу VCS и создайте pull request с автокоммитом:

* Arc: `arc pr create --push -A`
* SVN: `ya pr create -A`

После выполнения прекоммитных тестов, код будет автоматически закоммичен в Аркадию. Дождитесь, пока ревизия кода задач в подвале интерфейса Sandbox не станет большей или равной ревизии вашего коммита:

![revision ui](https://wiki.yandex-team.ru/users/mkznts/sandbox-tutorial/.files/screenshot2019-09-09at01.50.17.png)

В интерфейсе Sandbox выберите *Create → Task* и найдите в саджесте новую задачу:

![task suggest](https://jing.yandex-team.ru/files/mkznts/Screenshot%202019-11-03%20at%2016.14.06.png)

{% note "Совет" %}
Если задача не находится, попробуйте очистить кэш: *клик по аватару → Settings → Clear cache*, после чего перезагрузите страницу.
{% endnote %}

Создайте задачу и сразу запустите её кнопкой *Run*. Через некоторое время задача должна перейти в статус SUCCESS. На вкладке *Resources* появится новый ресурс. Проверьте его содержимое кликнув на иконку в разделе *Links*:

![resource list](https://jing.yandex-team.ru/files/mkznts/Screenshot%202019-11-03%20at%2016.24.10.png)

На этой тренировочной задаче мы будем демонстрировать основные возможности Sandbox. По ходу руководства мы научим эту задачу превращать Markdown в HTML (несколькими способами), получать дополнительные данные по введённому логину, и кое-что ещё **TODO**.
