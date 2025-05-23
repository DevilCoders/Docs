В этом документе описаны основные этапы и правила разработки данного проекта:

* [Определение целей спринта](#goals)
* [Планирование и оценка](#sprint)
* [Выбор задачи](#choose)
* [Оформление pull-реквестов](#pulls)
* [Код-ревью и тестирование](#codereview)

<a name="goals"></a>
## Цели спринта

Цели спринта — высокоуровневые «задачи», которые должны быть решены к концу спринта. Цели определяют состав задач спринта и позволяют их приоритезировать. Именно цели позволяют приоритезировать задачи в первом приближении.

<a name="sprint"></a>
## Планирование и оценка

До начала спринта его цели транслируются в задачи:

1. **Цели разбиваются на задачи**. Первый этап декомпозиции. После этого этапа, вместо абстрактных целей должен появиться список конкретных задач.

2. **Проработка требований задач**. Должно быть четкое понимание, чего требует каждая задача. Должен быть однозначный и понятный критерий выполнения задачи. Должны быть проработаны и согласованы с менеджерами все крайние кейсы. При необходимости, у задачи должны быть все необходимые, и обязательно утверждённые макеты. Дизайны утверждает Максим Сапронов (последнее слово за ним).

3. **Декомпозиция и оценка**. После проработки требований, задачи меняются в размерах (обычно увеличиваются и обрастают зависимостями). Крупные задачи должны быть разбиты на мелкие, не более 3-4 сторипоинтов на задачу.
*[`Storypoint`](https://agilefaq.wordpress.com/2007/11/13/what-is-a-story-point/) — абстрактная единица времени, в нашем контексте примерно равная 3 часам чистого рабочего времени. Таким образом, время выполнения любой конечной задачи не должно превышать 2 рабочих дней.*

4. **Приоритезация**. После получения плоского списка всех задач в оценённом виде, задачи, согласованно с командой и менеджером, приоритезируются. Например, слишком выросшие и непонятные задачи могут быть задвинуты в конец очереди, а наиболее понятные и проработанные — поставлены в начало.

Все задачи заводятся в [startrek](https://st.yandex-team.ru/DIR), в очереди «DIR: Директори.Я». Задаче необходимо выставить теги (новые теги заводить крайне нежелательно!) и текущий спринт. Продуктовые задачи заводит менеджер, технические — разработчик, баги заводят все.

<a name="choose"></a>
## Выбор задачи

В любой момент времени у одного разработчика в работе должно быть не больше одной задачи. После завершения любой очередной задачи, следующей выбирается задача с наивысшим приоритетом. Приоритезация у задач такая:

1. **Задачи текущего спринта**. Внутри спринта задачи так же могут быть приоритезированы при помощи поля «приоритет».
2. **Задачи, решающие цели текущего спринта**. Может оказаться, что какая-то задача оказалась вне спринта, или вообще не была заведена, но решает какую-то конкретную цель спринта.
3. **Прочие задачи**. Если план спринта выполнен досрочно, допускается взятие в работу внеспринтовых задач.

Взятие в работу любых внеспринтовых задач должно быть явно обозначено и согласновано с командой и менеджером.

<a name="pulls"></a>
## Оформление пулреквестов

Пулреквест должен состоять из одного комита. Commit-message этого комита должен ёмко отражать суть выполненных работ. Важно помнить, что из них собирается changelog, по которому будут ориентироваться многие люди, лишённые контекста выполненных задач, и, возможно, целей спринта.

Если в процессе стало ясно, что задача больше запланированного, её нужно декомпозировать на несколько подзадач и решать их независимо. Пулреквесты на несколько сотен строк должны быть исключением, а не правилом.

Пулреквест для данной задачи не может содержать мержкомитов, временных комитов, комитов из других задач.

<a name="codereview"></a>
## Код-ревью и тестирование

Все пулреквесты проходят код-ревью. Для этого, задача в трекере переводится в статус «codereview», а исполнителем назначается человек, который будет его выполнять. После этого кодревьювер сам решает, переводить ли задачу в тестирование, либо возвращать на доработку.

После перевода задачи в статус «решён», соответствующий ей пулреквест мержится в develop средствами github. Если во время тестирования в задаче находятся баги, она переоткрывается, а баги правятся в этой же ветке, но уже отдельным пулреквестом. После тестирования, если багов не осталось, задача закрывается, а ветка удаляется.
