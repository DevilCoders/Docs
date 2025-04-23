#|
|| **Редактировать заявку** | ((${ samadhiUrl } ${ experimentId })) ||
<% if (parentTicketUrl) { %>
|| **Родительский эксперимент** | ((${ parentTicketUrl })) ||
<% } %>
|| **Графы** |<% _.forEach(workflows, function(f) { %><%- f %>
<% }); %>||
<% if (resultsUrl) { %>
|| **Результаты** | ((${ resultsUrl } Посмотреть)) ||
<% } %>
|#

Про технические проблемы (граф упал, прототип криво обработался и т.д) пишите на ((mailto:sbs-dev@yandex-team.ru sbs-dev@)) со ссылкой на тикет и граф.
