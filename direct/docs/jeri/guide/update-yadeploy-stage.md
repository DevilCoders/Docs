# Обновление Я.Деплойного сервиса (без direct-release)

Задача: обновить сервис в Я.Деплое

## Теория { #theory }

Если сервис живет по полному релизному воркфлоу (у него есть релизные тикеты),
то эту инструкцию использовать не надо. Надо собирать релизы через direct-release.
См. например [инструкцию по сборке релизов Logviewer](../../guide/releases/logviewer#sborka).

Эта инструкция -- для тестовых сервисов без релизного воркфлоу либо для случаев, когда direct-release почему-то использовать невозможно.

## 1. Собери тарник. Это аналог сборки пакетов

**1.1.** Создай задачу в https://sandbox.yandex-team.ru

Пример: 
```
  svn info svn+ssh://arcadia.yandex.ru/arc/trunk/arcadia/direct
  sandbox-ya-package.pl --package direct/packages/deploy/logviewer/package-logviewer.json --revision <подставить ревизию из svn info> --yadeploy --yadeploy-resourse-type DIRECT_LOGVIEWER_DEPLOY_PACKAGE --no-wait
  sandbox-ya-package.pl --package direct/packages/deploy/chassis/package-chassis.json --revision <подставить ревизию из svn info> --yadeploy --yadeploy-resource-type=DIRECT_CHASSIS_DEPLOY_PACKAGE --no-wait
```

Важно: скрипт не проверяет соответствие json с описанием пакета и типа ресурса, будьте внимательны

Если делать вручную, то параметры такие:
тип 
`DIRECT_YA_PACKAGE`

Package paths, related to arcadia ';'-separated   
для logviewer -- `direct/packages/deploy/logviewer/package-logviewer.json`  
для chassis -- `direct/packages/deploy/chassis/package-chassis.json`

Package type: debian or tarball  
`tarball`

Created package resource type  
для logviewer -- `DIRECT_LOGVIEWER_DEPLOY_PACKAGE`  
для chassis -- `DIRECT_CHASSIS_DEPLOY_PACKAGE`

Enable release to Yandex.Deploy  
`Включить галочку`

Может быть, стоит менять сборочную и/или целевую платформы. По умолчанию будет  precise. Непонятно.

Пример таски: <https://sandbox.yandex-team.ru/task/687456505/view>

**1.2.** запусти задачу (run)

**1.3.** дождись завершения задачи (полчаса). Если задача зафейлилась -- стоп, надо разбираться.

## **2.** Зарелизь ресурс из Sandbox. Это аналог dupload + dmove

**2.1.** В шапке задачи из п.1 нажми Release и выбери стейдж: Testing для непродакшенов, Production для продакшена  
Если нет прав релизить таску из интерфейса, запускай с `ppcdev`:  
`SANDBOX_TOKEN_FILE=/etc/direct-tokens/sandbox_oauth_token_ppc dt-sandbox-resource-release.py -t <id таски> -s <testing|stable>`

**2.2.** Дождись, что в шапке задаче появится бирка "Released" с нужным стейджем

## 3. Примени спеку с новой версией в Деплое. Это аналог direct-java-deploy { #apply-new-spec }

**3.1.** Заходи в интерфейс Деплоя <https://deploy.yandex-team.ru/>

**3.2.** Находи сервис (стейдж), который обновляешь. Например для chassis на devtest <https://deploy.yandex-team.ru/stages/direct-chassis-devtest>

**3.3.** Переходи во вкладку Deploy tickets. Там должна быть новособранная версия (отыскать нужную таску из нескольких можно по дате + внутри sandbox task в Description есть номер релиза).

**3.4.** Нажимай Commit

## 4. Смотри, что получилось

**4.1.** Смотри вкладки Status и Monitoring в deploy.yandex-team.ru

**4.2.** Смотри графики и мониторинги, какие есть по приложению

**4.3.** На ppcdev можно проверить версию командой (на примере api5)
```sh
dt-get-yadeploy-app-versions java-api5 2>/dev/null
```

## Ссылки { #links }

- прыдыдущая версия в wiki была здесь: <https://wiki.yandex-team.ru/jeri/ya-deploy/>
- [про dctl](../howto-dctl.md)
- [сборка и тестирование релизов Logviewer](../../guide/releases/logviewer).
- [выкладка релизов Logviewer](./deploy.md)

