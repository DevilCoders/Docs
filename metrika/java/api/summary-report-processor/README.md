# summary-report-processor
Процессинг еженедельных отчетов.

Флоу работы:

![summaryreport](summary-report-processor.svg)

# Краткое описание основных компонент:
## SummaryReportTelegramLinkController/Service
Про авторизацию пользователя в telegram: https://core.telegram.org/widgets/login

У себя проверяем AuthHash на подлинность и привязываем telegram_uid и uid пользователя. Храним эти провязки в pg `subscriptions.telegram_user_links`
Помимо самой провязки telegram, эта компонента изменяет список счетчиков, на которые подписан пользователь. Пользователь может выбрать
один из типов [подписки](../management-common/src/java/ru/yandex/metrika/api/management/client/subscriptions/SubscriptionListType.java) (Доступны все кроме `ALL`).
В случае с `LIST` пользователь явно выбирает список счетчиков, после чего этот список счетчиков сохраняется в `summary_report_subscriptions_counters`
## SummaryReportsSettingsController/Service
Компонента отвечает за настройки отчетов каждого счетчика и за настройки по умолчанию. Для каждой фичи счетчика храним в `summary_report_metrics_by_feature`
список метрик, которые будут включены в отчет по умолчанию(если пользователи не выберут никаких настроек в интерфейсе)
и доступны для выбора в интерфейсе. Также по умолчанию в отчет включены все автоцели на счетчики. В интерфейсе счетчика пользователь
выбирает доступные для отчета в телеграмме метрики и цели счетчика. Все настройки сохраняются в таблице `summary_report_settings`
## SummaryReportEnqueueTask
Таска создает задачи на формирование и отправку отчета, складывая эти задачи в таблицы `summary_report_jobs` и
`summary_report_send_jobs`. В `summary_report_jobs` хранятся задачи на формирование отчета на счетчик, за неделю может быть
сформирован только один отчет. В `summary_report_send_jobs` хранятся задачи на отправку сформированных отчетов в телеграм.
Задача просматривает текущие подписки в `summary_report_subscriptions`, создает (если еще не создана в текущей неделе) задачи на формирование отчета на счетчике и
добавляет задачи на отправку сообщений в telegram.

В процессе создания `summary_report_jobs` задачи имеют статус `ENQUEUING`, после создания - `ENQUEUED`.
## SummaryReportFormTask
Onetime-таска, которая шедулится таской SummaryReportFormRunnerTask, одновременно может работать несколько таких тасок,
обрабатывая разные батчи задач из `summary_report_jobs`. Таска берет задачи в статусе `ENQUEUED`, после шедулинга проставляется статус `FORMING`.
Таска запрашивает нужные метрики из кликхауса и кладет результаты
в S3(бакет `metrika-summary-reports`). После завершения работы задаче проставляется статус `FORMED`
## SummaryReportMessageGenerateTask
Onetime-таска, которая шедулится таской SummaryReportMessageGenerateRunnerTask, одновременно может работать несколько таких тасок,
обрабатывая разные батчи задач из `summary_report_jobs`. Таска берет задачи в статусе `FORMED`, после шедулинга проставляется статус `SENDING`.
Таска читает результаты из S3 и формирует сообщения(для каждого нужного языка) в телеграмме. После этого кладет сообщения для каждого
пользователя в очередь SQS и проставляет статус задачам `SENT`. Однако из-за того что нужно одновременно записать сообщение в очередь
и проставить статус, возможны дубликаты в очереди, так как таска ретраится.
##TelegramMessageSender
Читает сообщения из очереди и рассылает их в телеграмме от имени бота `@YaMetricaBot`. Очередь SQS была введена для
ограничения RPS, посылаемого в Telegram (он имеет ограничение в ~30rps).

##Мониторинги
[Дашбоард](https://monitoring.yandex-team.ru/projects/metrika/dashboards/monbfvk2cgj577fj0m59?from=now-30m&to=now&refresh=60000&p.environment=production&p.=production)
