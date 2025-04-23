Тестирование
===

Локально:
- Положить [ARC_TOKEN](https://yav.yandex-team.ru/secret/sec-01fnxm4hd8nhr2f3583sz0tpde/explore/version/ver-01g16d84s91q430jb8htsgxjc6) в local.env
- Создать PR и к имени добавить префикс `skip_shiva-gh-app`, тогда продовый и тестовый боты не будут валидировать такой PR
- Запустить `main.go`
- Выполнить `grpcurl --plaintext -d '{"prId": id, "version": 1}' localhost:99 shiva.api.validator.ValidationService.Run`

В тестинге:
- Создать PR и к имени добавить префикс `test_shiva-gh-app`
- Добавить PR_ID к `envs.test_ids` в [teamcity](https://t.vertis.yandex-team.ru/admin/editBuildParams.html?id=buildType:VertisAdmin_ArcadiaPr_Validate)
