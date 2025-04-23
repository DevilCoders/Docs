1. Просмотр текущих конфигов push-client в сервисе:
```
./pushconf-updater show --services discord_test_service 
2022-04-05T13:02:28.806+0300	INFO	cmd/main.go:61	[init] enable info mode
2022-04-05T13:02:28.806+0300	INFO	cmd/main.go:65	[init] running dry run mode
2022-04-05T13:02:28.806+0300	INFO	pushlib/nanny.go:90	[GetMDBTokenOverSSH] run oauth.GetTokenBySSH for user 
2022-04-05T13:02:29.813+0300	INFO	cmd/main.go:94	[updateInstanceSpec] check tvm token for service discord_test_service
2022-04-05T13:02:29.813+0300	INFO	cmd/main.go:98	[updateInstanceSpec] founded tvm token, service discord_test_service, volume: push-client-tvm-secret-health, skip delegated
2022-04-05T13:02:29.848+0300	INFO	cmd/main.go:112	[nannyShowConfigs] service: discord_test_service, topic: topic1, logfile: test6, tvm_client: 824636955160
2022-04-05T13:02:29.848+0300	INFO	cmd/main.go:112	[nannyShowConfigs] service: discord_test_service, topic: topic1, logfile: topic7, tvm_client: 824636955160
2022-04-05T13:02:29.848+0300	INFO	cmd/main.go:112	[nannyShowConfigs] service: discord_test_service, topic: topic1, logfile: test9, tvm_client: 824636955160
2022-04-05T13:02:29.849+0300	INFO	cmd/main.go:112	[nannyShowConfigs] service: discord_test_service, topic: topic1, logfile: test3, tvm_client: 824636955160
2022-04-05T13:02:29.849+0300	INFO	cmd/main.go:112	[nannyShowConfigs] service: discord_test_service, topic: topic4, logfile: test4, tvm_client: 824636955160
2022-04-05T13:02:29.849+0300	INFO	cmd/main.go:112	[nannyShowConfigs] service: discord_test_service, topic: topic3, logfile: test5, tvm_client: 824636955160
2022-04-05T13:02:29.849+0300	INFO	cmd/main.go:112	[nannyShowConfigs] service: discord_test_service, topic: topic1, logfile: test10, tvm_client: 824636955160
```

2. Добавление в конфиг новых логов и топиков:
```
./pushconf-updater update --services discord_test_service --logs log1@topic1,log2@topic2,log3,log4 --main-topic topic3 --doit
2022-04-05T13:41:34.151+0300	INFO	cmd/main.go:61	[init] enable info mode
2022-04-05T13:41:34.151+0300	INFO	cmd/main.go:122	[nannyUpdateConfigs] start search services, user: dspushkin, services_patterns: discord_test_service
2022-04-05T13:41:34.151+0300	INFO	pushlib/nanny.go:90	[GetMDBTokenOverSSH] run oauth.GetTokenBySSH for user 
2022-04-05T13:41:34.627+0300	INFO	cmd/main.go:433	[updateInstanceSpec] check tvm token for service discord_test_service
2022-04-05T13:41:34.627+0300	INFO	cmd/main.go:437	[updateInstanceSpec] founded tvm token, service discord_test_service, volume: push-client-tvm-secret-health, skip delegated
2022-04-05T13:41:34.689+0300	INFO	cmd/main.go:159	[nannyUpdateConfigs] found different configs for discord_test_service
+3
+- name: log1
+  send_delay: 5
+  chunk:
+    send-server: 1
+    send-file: 1
+  topic: topic1
+- name: log2
+  send_delay: 5
+  chunk:
+    send-server: 1
+    send-file: 1
+  topic: topic2
+- name: log3
+  send_delay: 5
+  chunk:
+    send-server: 1
+    send-file: 1
+- name: log4
+  send_delay: 5
+  chunk:
+    send-server: 1
+    send-file: 1
+

2022-04-05T13:41:34.951+0300	INFO	cmd/main.go:177	[nannyUpdateConfigs] saved to Nanny success
2022-04-05T13:41:34.952+0300	INFO	pushlib/template.go:186	[BackupNewConfig] saved discord_test_service.push.new.1649155294 success
2022-04-05T13:41:34.953+0300	INFO	pushlib/template.go:175	[BackupOldConfig] saved discord_test_service.push.old.1649155294 success
```
Результат:
```
2022-04-05T13:42:55.699+0300	INFO	cmd/main.go:112	[nannyShowConfigs] service: discord_test_service, topic: topic3, logfile: test8, tvm_client: 824635424728
2022-04-05T13:42:55.699+0300	INFO	cmd/main.go:112	[nannyShowConfigs] service: discord_test_service, topic: topic1, logfile: log1, tvm_client: 824635424728
2022-04-05T13:42:55.699+0300	INFO	cmd/main.go:112	[nannyShowConfigs] service: discord_test_service, topic: topic2, logfile: log2, tvm_client: 824635424728
2022-04-05T13:42:55.699+0300	INFO	cmd/main.go:112	[nannyShowConfigs] service: discord_test_service, topic: topic3, logfile: log3, tvm_client: 824635424728
2022-04-05T13:42:55.699+0300	INFO	cmd/main.go:112	[nannyShowConfigs] service: discord_test_service, topic: topic3, logfile: log4, tvm_client: 824635424728
```
3. Удаление из конфига логов:
```
./pushconf-updater remove --services discord_test_service --logs log1@topic1,log2@topic2,log3,log4 --doit
2022-04-05T13:44:18.771+0300	INFO	cmd/main.go:61	[init] enable info mode
2022-04-05T13:44:18.771+0300	INFO	cmd/main.go:196	[nannyUpdateConfigs] start search services, user: dspushkin, services_patterns: discord_test_service
2022-04-05T13:44:18.771+0300	INFO	pushlib/nanny.go:90	[GetMDBTokenOverSSH] run oauth.GetTokenBySSH for user 
2022-04-05T13:44:19.120+0300	INFO	cmd/main.go:224	[nannyRemoveConfigs] found different configs for discord_test_service
-  send_delay: 5
-  chunk:
-    send-server: 1
-    send-file: 1
-  topic: topic1
-- name: log2
-  send_delay: 5
-  chunk:
-    send-server: 1
-    send-file: 1
-  topic: topic2
-- name: log3
-  send_delay: 5
-  chunk:
-    send-server: 1
-    send-file: 1
-- name: log4
-  send_delay: 5
-  chunk:
-    send-server: 1
-    send-file: 1
-

2022-04-05T13:44:19.406+0300	INFO	cmd/main.go:249	[nannyRemoveConfigs] saved to Nanny success
2022-04-05T13:44:19.407+0300	INFO	pushlib/template.go:186	[BackupNewConfig] saved discord_test_service.push.new.1649155459 success
2022-04-05T13:44:19.409+0300	INFO	pushlib/template.go:175	[BackupOldConfig] saved discord_test_service.push.old.1649155459 success
```
4. Загрузка готового лога push-client:
```
./pushconf-updater upload --services discord_test_service --file ./discord_test_service.push.old.1649155459  --doit
2022-04-05T13:49:49.550+0300	INFO	cmd/main.go:61	[init] enable info mode
2022-04-05T13:49:49.550+0300	INFO	pushlib/nanny.go:90	[GetMDBTokenOverSSH] run oauth.GetTokenBySSH for user 
2022-04-05T13:49:52.407+0300    INFO    cmd/main.go:433 [updateInstanceSpec] check tvm token for service discord_test_service
2022-04-05T13:49:52.407+0300    INFO    cmd/main.go:437 [updateInstanceSpec] founded tvm token, service discord_test_service, volume: push-client-tvm-secret-health, skip delegated
2022-04-05T13:49:50.161+0300	INFO	cmd/main.go:299	[nannyLoadConfigs] found different configs for discord_test_service
+- name: log1
+  send_delay: 5
+  chunk:
+    send-server: 1
+    send-file: 1
+  topic: topic1
+- name: log2
+  send_delay: 5
+  chunk:
+    send-server: 1
+    send-file: 1
+  topic: topic2
+- name: log3
+  send_delay: 5
+  chunk:
+    send-server: 1
+    send-file: 1
+- name: log4
+  send_delay: 5
+  chunk:
+    send-server: 1
+    send-file: 1
+

2022-04-05T13:49:50.380+0300	INFO	cmd/main.go:318	[nannyUpdateConfigs] saved to Nanny success
2022-04-05T13:49:50.381+0300	INFO	pushlib/template.go:175	[BackupOldConfig] saved discord_test_service.push.old.1649155790 success
```
5. Дамп текущего конфига в локальный файл:
```
./pushconf-updater dump --services discord_test_service --backup-dir /tmp/
2022-04-05T13:57:33.584+0300	INFO	cmd/main.go:61	[init] enable info mode
2022-04-05T13:57:33.584+0300	INFO	cmd/main.go:65	[init] running dry run mode
2022-04-05T13:57:33.584+0300	INFO	pushlib/nanny.go:90	[GetMDBTokenOverSSH] run oauth.GetTokenBySSH for user 
2022-04-05T13:57:33.957+0300	INFO	pushlib/template.go:186	[BackupNewConfig] saved /tmp/discord_test_service.push.new.1649156253 success
```
6. Добавление топиков и выставление нужного TVM ключа в Nanny(имя ключа в Nanny берётся из конфига push-client, строка tvm-secret-file)
```
./pushconf-updater update --services discord_test_service --logs log1@topic1,log2@topic2,log3,log4 --main-topic topic3 --tvm-secret-file push-client-tvm-secret-health2/client_secret --tvm-secret-name  market.discord --doit
2022-04-05T14:29:29.937+0300	INFO	cmd/main.go:61	[init] enable info mode
2022-04-05T14:29:29.937+0300	INFO	cmd/main.go:127	[nannyUpdateConfigs] start search services, user: dspushkin, services_patterns: discord_test_service
2022-04-05T14:29:29.937+0300	INFO	pushlib/nanny.go:90	[GetMDBTokenOverSSH] run oauth.GetTokenBySSH for user 
2022-04-05T14:29:30.407+0300	INFO	cmd/main.go:437	[updateInstanceSpec] check tvm token for service discord_test_service
2022-04-05T14:29:30.407+0300	INFO	cmd/main.go:444	[updateInstanceSpec] not founded tvm token, service discord_test_service, volume: push-client-tvm-secret-health2, need delegated
2022-04-05T14:29:30.407+0300	INFO	cmd/main.go:449	[updateInstanceSpec] start delegated tvm token, service: discord_test_service, new_volume: push-client-tvm-secret-health2
2022-04-05T14:29:30.705+0300	INFO	cmd/main.go:482	[updateInstanceSpec] start updating instance spec, service: discord_test_service
2022-04-05T14:29:30.805+0300	INFO	cmd/main.go:486	[updateInstanceSpec] success  updating instance spec, service: discord_test_service
2022-04-05T14:29:30.827+0300	INFO	cmd/main.go:161	[nannyUpdateConfigs] not found different configs for discord_test_service, skip update
```

