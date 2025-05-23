Правила попадания блоков и доработок в Лего
-------------------------------------------

Все блоки, которые попадают в Лего из вне, условно можно разделить на две группы, в зависимости от источника.

##1. Портальные блоки

Блоки, согласованные и одобренные заказчиком и сервисами, для использования на всем портале.

У портальных блоков есть:

 - конкретный заказчик (ответственный менеджер);
 - известные сроки внедрения;
 - список сервисов-пользователей Лего, где блок будет внедряться.

##2. Блоки сервисов

Это могут быть:

 - портальные блоки, доработанные дизайнерами сервиса, для решения конкретных частных случаев, которые возникают при взаимодействии с пользователями сервиса;
 - собственные блоки сервисов, которые разрабатывались для решения специфических задач.

Такие блоки могут пригодиться в других сервисах и частично распространиться по порталу.

У блоков сервиса нет конкретного заказчика, в лице ответственного менеджера, и установленных дедлайнов на портирование — есть только разработчики сервисов, заинтересованные в передаче поддержки и дальнейшего развития этих блоков в Лего.

Принимая во внимание эту условную градацию, правила портирования блоков и доработок в общепортальные библиотеки Лего выглядят следующим образом.

##Условия добавления и поддержки блоков в Лего

###Портальные блоки
1. Блоки планируются на работу в следующий квартал согласно [процедуре квартального планирования](planning.md).
1. Если у блока есть конкретный заказчик (ответственный менеджер) и сроки внедрения, которые согласованы с пользователями Лего, то приоритет разработки такого блока будет выше, чем у остальных блоков, участвующих в квартальном планировании.

**Способ добавления кода** — отправка PR в Лего со стороны разработчиков сервиса, либо разработка блока силами команды Лего.

###Блоки сервисов
1. Количество команд сервисов, где уже используется блок **>=2**.
1. Дизайн блока стабилизировался (текущий дизайн блока присутствует в последней версии дизайнерских гайдов, либо это подтверждают портальные менеджеры).
1. У блока есть подтвержденные потенциальные потребители, помимо текущих, запланировавшие внедрение блока после его появления в Лего.

**Способ добавления кода** — отправка PR в Лего и доведение его до финала силами разработчиков сервиса при консультациях команды Лего (для этого в Лего подготовлена необходимая инфраструктура и написан подробный [contribution guide](contribute.md)).

На среднесрочные планы команды Лего всегда можно повлиять, участвуя в процессе [квартального планирования Лего](planning.md).
