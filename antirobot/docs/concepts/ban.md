# Бан, блокировка и амнистия

## Бан {#ban}

Бан (забанивание) — возврат страницы капчи в ответ на запрос.

Антиробот забанит запрос пользователя, если будут выполнены условия:
- идентификатор пользователя находится в списке забаненных (роботных) идентификаторов во внутренней базе Антиробота или во флагах бана [ЕББ](cbb.md);  
- на запрос можно вернуть капчу (см. раздел [Разметка по типам запросов](markup.md)).

Список забаненных — список идентификаторов пользователей, которые признаны роботами в результате расчетов процесора. Обновляется при каждом запросе к процессору.

При корректном вводе капчи пользователь получит куку spravka и, таким образом, приобретет новую идентификацию. Старая идентификация при этом не удаляется, а хранится во внутренней базе Антиробота до наступления [амнистии](#amnesty).

spravka — уникальная кука, которую Антиробот выставляет пользователю при прохождении капчи. Справка считается отдельным идентификатором, а пользователь с ней — отдельным пользователем. Справка дает пользователю несколько гарантированных запросов, за которые он не будет забанен, даже если Антиробот признает пользователя роботом.

Если пользователь решит не вводить капчу, он ее снова получит на следующий запрос (при условии, что на запрос можно вернуть капчу.

Для обучения классификатора Антиробот использует случайные баны, которые выполняются на каждый десятитысячный запрос. При этом возвращаемая на запрос страница капчи будет отличаться от обычной.

{% note info %}

Используйте принудительный вызов страницы капчи, чтобы посмотреть как она выглядит. Инструкцию см. в разделе [Проверка верстки](check-layout.md).

{% endnote %}


## Блокировка {#block}

Блокировка — редирект запроса на страницу блокировки (HTTP-код 403) в случае, если пользователь попал под критерии блокировки в ЕББ.

Текст на странице сообщает пользователю, что ему запрещен доступ к сервисам Яндекса. Пользователь не сможет ввести капчу и снять блокировку, но сможет написать в службу поддержки сервиса.

## Амнистия {#amnesty}

Забаненные IP-адреса автоматически удаляются из внутренней базы кэшера через час после добавления.

Весь список забаненных идентификаторов пользователей удаляется из кэшера каждый понедельник в 03:30.

