# ess-moderation-apply-*
Вместо * указывается название конкретного процесса обработки вердиктов:
- [ess-moderation-apply-general-results-lag](https://juggler.yandex-team.ru/project/direct.prod/aggregate?service=ess-moderation-apply-general-results-lag&host=direct-lb-moderation&project=direct.prod) - общий процесс обработки вердиктов (попадают все вердикты, не попавшие в отдельные топики)
- [ess-moderation-apply-image-ad-results-lag](https://juggler.yandex-team.ru/project/direct.prod/aggregate?service=ess-moderation-apply-image-ad-results-lag&host=direct-lb-moderation&project=direct.prod) - обработка вердиктов на картиночные баннера
- [ess-moderation-apply-smart-banner-results-lag](https://juggler.yandex-team.ru/project/direct.prod/aggregate?service=ess-moderation-apply-smart-banner-results-lag&host=direct-lb-moderation&project=direct.prod) - обработка вердиктов на smart-баннера
- [ess-moderation-apply-text-banner-results-lag](https://juggler.yandex-team.ru/project/direct.prod/aggregate?service=ess-moderation-apply-text-banner-results-lag&host=direct-lb-moderation&project=direct.prod) - обработка вердиктов на текстовые баннера

## Описание { #description }
Проверяется лаг обработки вердиктов модерации из соответствующих топиков.

## Диагностика { #diagnostics }
На [графике лага](https://solomon.yandex-team.ru/?l.Account=direct&l.ConsumerPath=direct%2Fmodadvert%2Fgeneral%2Frequests-consumer&l.OriginDC=*&l.TopicPath=*&cluster=lbkx&l.host=cluster&l.partition=-&project=kikimr&l.sensor=CreateTimeLagMsByCommitted&service=pqtabletAggregatedCounters&l.user_counters=PersQueue&graph=auto&b=1h&e=) должен быть виден существенный рост.
Надо посмотреть на:
- [График количества обработанных вердиктов](https://solomon.yandex-team.ru/?project=direct&cluster=app_java-jobs&service=java-monitoring&l.env=production&l.jobs=moderation_reader&l.host=CLUSTER&l.sensor=*moderation_response&graph=auto&checks=-display_href_sm_moderation_response%3Bsitelinks_set_sm_moderation_response%3Bturbolink_moderation_response&transform=differentiate&b=1d&e=). Если на нем не видно резкого падения, значит пришло очень много вердиктов и мы не успеваем их обрабатывать. В этом случае надо пробовать масштабировать обработку (см. далее). Если принятых вердиктов мало или их нет, нужно смотреть ошибки в работе.
- [Логи джобы](https://direct.yandex.ru/logviewer/#~(logType~'messages~form~(fields~(~'log_time~'host~'service~'method~'trace_id~'span_id~'prefix~'log_level~'class_name~'message)~conditions~(service~'direct.jobs~method~'moderation.ReceiveModerationResponseJob~log_level~'ERROR)~limit~100~offset~0~reverseOrder~false~showTraceIdRelated~false))$). Нужно посмотреть на конкретные ошибки и разбираться по факту.

## Решение { #solution }
- Если не успеваем обрабатывать вердикты, то нужно пробовать распараллелить обработку. На момент написания документации (2022-06-14) проблем со скоростью обработки нет. Распараллеливание обработки вердиктов настраивается [тут](https://a.yandex-team.ru/arc/trunk/arcadia/direct/libs-internal/config/src/main/resources/common-production.conf?rev=r9584794#L1605).
- Из известных ошибок при обработке вердиктов может быть "Lock wait timeout exceeded; try restarting transaction". В этом случае должна страдать ещё какая-то джоба (например, отправка на модерацию). Нужно остановить конкурирующую джобу и дать очереди вердиктов обработаться.
