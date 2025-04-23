# Классификация аварий (sev-levels)

## Что такое severity { #motivation }

Severity — это шкала тяжести проблем в сервисе.
Уровни severity удобны и полезны для того, чтобы было проще обсуждать аварии: 
насколько быструю реакцию хотим, сколько ресурсов оправдано привлекать к решению проблемы и т.п.

У нас есть договоренности:

* по каким признакам относим аварии к sev1, sev2 и т.д.
* какой "уровень сервиса" получает авария в зависимости от sev-level
* Во время аварии задаемся вопросом "это sev1, sev2, или sev3?" и далее обрабатываем аварию соответственно. 

Об этом см. инструкцию: (TODO ссылка)

## Severity vs. Priority { #severity-vs-priority }
Severity — это масштаб/тяжесть проблемы; мера того, насколько нарушена нормальная работа сервиса.

Priority — это приоритет проблемы; скорость, с которой хотим чтобы она была пофикшена.

Есть корреляции: тяжелые проблемы обычно приоритетные.
Но есть и особенности (примеры из статьи Atlassian):

* Косметический баг "орфографическая ошибка в заголовке" может стать высокоприоритетным, если предстоит публичный запуск с демонстрацией.
* sev2 в норме хотим решать немедленно, но если одновременно разворачивается sev1, то sev2 встанет в очередь. 


## Источники вдохновения { #sources }

### dlutzy
<https://dlutzy.wordpress.com/2013/10/13/incident-severity-sev1-sev2-sev3-sev4-sev5/>

* Sev1 Complete outage
* Sev2 Major functionality broken and revenue affected
* Sev3 Minor problem, bug
* Sev4 Redundant component failure
* Sev5 False alarm or alert for something you can’t fix


### cyara

<https://cyara.com/incident-severity-levels/>

#### SEV1: Critical Impact/System Down

A SEV1 defect is a production outage. This is where the production system has ceased to operate, and there is no workaround. There are several different ways that a contact center can experience a SEV1 outage. An example is an error in the IVR, such as a prompt not loading, that prevents callers from being able to complete tasks within the IVR, resulting in a significant number of additional calls getting through to the agents. The errors can also involve agent systems, such as the CRM system failing, making it impossible for agents to access customer records and serve customers effectively.

#### SEV2: Significant Impact

A SEV2 defect refers to defects that affect production, but workarounds are possible. A SEV2 disaster, compared to a SEV1, is not a production outage but still affects the customer experience. For example, the CTI might misroute calls, resulting in agents having to manually transfer calls. Ultimately the customer is served, but there’s a not insignificant negative impact to the customer experience.
 
#### SEV3: Minor Impact

A SEV3 defect also impacts production systems. Customers and agents are able to accomplish tasks, but experience nuisances and inconveniences. An example of a SEV3 in a contact center is when audio quality is poor, requiring the customer and agent to repeat themselves, but ultimately, they are able to accomplish their tasks. In terms of your CX, these aren’t critical, but are the CX equivalent of death by a thousand paper cuts.


### vmware

<https://www.vmware.com/support/policies/severity.html>

#### Critical (On Premise Severity 1)
Production server or other mission critical system(s) are down and no workaround is immediately available.

- All or a substantial portion of your mission critical data is at a significant risk of loss or corruption.
- You have had a substantial loss of service.
- Your business operations have been severely disrupted.

Severity 1 support requires you to have dedicated resources available to work on the issue on an ongoing basis during your contractual hours.

#### Major (On Premise Severity 2)
Major functionality is severely impaired.

- Operations can continue in a restricted fashion, although long-term productivity might be adversely affected.
- A major milestone is at risk. Ongoing and incremental installations are affected.
- A temporary workaround is available.

#### Minor (On Premise Severity 3)
Partial, non-critical loss of functionality of the software.

- Impaired operations of some components, but allows the user to continue using the software.
- Initial installation milestones are at minimal risk.

#### Cosmetic (On Premise Severity 4)
General usage questions.

- Cosmetic issues, including errors in the documentation.


#### Critical (SaaS Severity 1)
Critical production issue that severely impacts your use of the service.The situation halts your business operations and no procedural workaround exists.

- Service is down or unavailable.
- Data corrupted or lost and must restore from backup.
- A critical documented feature / function is not available.

Severity 1 issues require the customer to have dedicated resources available to work on the issue on an ongoing basis with VMware.

#### Major (SaaS Severity 2)
Major functionality is impacted or significant performance degradation is experienced. The situation is causing a high impact to portions of your business operations and no reasonable workaround exists.

- Service is operational but highly degraded performance to the point of major impact on usage.
- Important features of the Software as a Service offering are unavailable with no acceptable workaround; however, operations can continue in a restricted fashion.

#### Minor (SaaS Severity 3)
There is a partial, non-critical loss of use of the service with a medium-to-low impact on your business, but your business continues to function.  Short-term workaround is available, but not scalable.

#### Cosmetic (SaaS Severity 4)
Inquiry regarding a routine technical issue; information requested on application capabilities, navigation, installation or configuration; bug affecting a small number of users. Acceptable workaround available.



### atlassian

<https://www.atlassian.com/incident-management/kpis/severity-levels>

At Atlassian, we define a SEV (severity) 1 incident as __“a critical incident with very high impact.”__ This could include a customer data loss, a security breach, or when a client-facing service is down for all customers.  

A SEV 2 incident is a __“major incident with significant impact,”__ including when a client-facing service is down for a sub-set of customers or a critical function within a system is not functioning.

And a SEV 3 incident is __“a minor incident with low impact,”__ such as a system glitch that is causing customers slight inconvenience. 

At Atlassian, SEV 3 incidents can be handled during daytime/working hours, while SEV 1 and SEV 2 incidents generate an alert for on-call professionals for an immediate fix no matter the time of day.


### pagerduty

<https://response.pagerduty.com/before/severity_levels/>

#### SEV-1
__Critical issue that warrants public notification and liaison with executive teams.__

 * The system is in a critical state and is actively impacting a large number of customers.
 * Functionality has been severely impaired for a long time, breaking SLA.
 * Customer-data-exposing security vulnerability has come to our attention.

__Response: Major incident response.__

 * Page an IC in Slack !ic page.
 * See During an Incident. (<https://response.pagerduty.com/during/during_an_incident/>)
 * Notify internal stakeholders.
 * Public notification.

#### SEV-2
__Critical system issue actively impacting many customers' ability to use the product.__

 * Notification pipeline is severely impaired.
 * Incident response functionality (ack, resolve, etc) is severely impaired.
 * Web app is unavailable or experiencing severe performance degradation for most/all users.
 * Monitoring of PagerDuty systems for major incident conditions is impaired.
 * Any other event to which a PagerDuty employee deems necessary of incident response.

__Response: Major incident response.__
 
 * Page an IC in Slack !ic page.
 * See During an Incident. (<https://response.pagerduty.com/during/during_an_incident/>)

#### SEV-3
__Stability or minor customer-impacting issues that require immediate attention from service owners.__

 * Partial loss of functionality, not affecting majority of customers.
 * Something that has the likelihood of becoming a SEV-2 if nothing is done.
 * No redundancy in a service (failure of 1 more node will cause outage).

__Response: High-Urgency page to service team.__

 * Work on issue as your top priority.
 * Liaise with engineers of affected systems to identify cause.
 * If related to recent deployment, rollback.
 * Monitor status and notice if/when it escalates.
 * Mention on Slack if you think it has the potential to escalate.
 * Trigger incident response if necessary (!ic page).

#### SEV-4
__Minor issues requiring action, but not affecting customer ability to use the product.__

* Performance issues (delays, etc).
* Individual host failure (i.e. one node out of a cluster).
* Delayed job failure (not impacting event & notification pipeline).
* Cron failure (not impacting event & notification pipeline).

__Response: Low-Urgency page to service team.__

* Work on the issue as your first priority (above "normal" tasks).
* Monitor status and notice if/when it escalates.

#### SEV-5
__Cosmetic issues or bugs, not affecting customer ability to use the product.__

* Bugs not impacting the immediate ability to use the system.

__Response: JIRA ticket.__

* Create a JIRA ticket and assign to owner of affected system.

