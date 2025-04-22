#|
|| **Редактировать заявку** | ((${ samadhiUrl } ${ experimentId })) ||
|| **Описание эксперимента** | ${ description } ||
<% if (parentTicketUrl) { %>
|| **Родительский эксперимент** | ((${ parentTicketUrl })) ||
<% } %>
|| **Страна, платформа** | ${ region }, ${ device } ||
|| **Системы** |
<% _.forEach(systems, function(o, i) { %><%- i %>:  **<%- o.title  %>**<% if(o.type !== 'external') { %> [((<%= o.fdbUrl %> <%- o.query %>))]<% } else { %> ⏱ <%} %>
<% }); %>||
|| **Ханипоты** |
<% _.forEach(honeypots, function(o, i) { %>${ honeypotsStartIndex + i }:  **<%- o.title  %>** [((<%= o.fdbUrl %> <%- o.query %>))]
<% }); %>||
|| **В одном задании** | ${ tasksuiteComposition.val.goodTasksCount } real + ${ tasksuiteComposition.val.badTasksCount } gs ||
|| **Запросов на пару систем** | <% _.forEach(crossesList, function(cross) { %><%- cross %>
<% }); %>||
|| **Графы** |<% _.forEach(workflows, function(f) { %><%- f %>
<% }); %>||
<% if (resultsUrl) { %>
|| **Результаты** | ((${ resultsUrl } Посмотреть)) ||
<% } %>
|#

Про технические проблемы (граф упал, фильтр/плагин не сработал и т.д) пишите на ((mailto:sbs-dev@yandex-team.ru sbs-dev@)) со ссылкой на тикет и граф.
