#|
|| **Редактировать заявку** | ((${ samadhiUrl } ${ experimentId })) ||
|| **Описание эксперимента** | ${ description } ||
<% if (parentTicketUrl) { %>
|| **Родительский эксперимент** | ((${ parentTicketUrl })) ||
<% } %>
|| **Системы** |
<% _.forEach(systems, function(s, i) { %><%- i %>:  **<%- s  %>**
<% }); %>||
|| **В одном задании** | ${ goodTasks } real + ${ badTasks } gs ||
|| **Шаблонный пулл** | ${ poolTitle } ||
|| **Графы** |<% _.forEach(workflows, function(f) { %><%- f %>
<% }); %>||
<% if (resultsUrl) { %>
|| **Результаты** | ((${ resultsUrl } Посмотреть)) ||
<% } %>
|#

Про технические проблемы (граф упал, в предпросмотре что-то странное и т.д) пишите на ((mailto:sbs-dev@yandex-team.ru sbs-dev@)) со ссылкой на тикет и граф.
