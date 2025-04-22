# D'Arc
## Что это?
Утилита для дозаписывания debian changelog-a и инкремента версий на основе коммитов в Arc
## Зачем?
Чтобы дозаписывать debian changelog и инкрементить версии на основе коммитов в Arc
## Так, ладно, а какие пререквизиты?
Последней строкой в блоке changelog-а (перед автором блока) должна быть строка вида

`last commit: хэш коммита`

хэш можно получить запустив

```bash
arc log .
```

Весь блок будет выглядеть примерно так
```
yb-dwh (5.0.16) precise; urgency=low
  [ ecialo ]
      DWH-585
  [ estarchak ]
      DWH-579: switched to videodict by kochurovvs
      5.0.15
  last commit: cd38d204474d35084f88e4215d73b1c68ec4b188

 -- Integrat Dostavlyaev <robot-billing-ci@yandex-team.ru>  Mon, 28 Oct 2019 13:38:08 -0000
```

## Как пользоваться?
### Базовый сценарий
Выполните
```bash
$ARCADIA_HOME/billing/library/tools/d_arc/d_arc
```
из корня проекта. Он найдёт changelog в поддиректории debian/changelog и туда же дозапишет новый. Вы восхитительны.
### Небазовый сценарий
`d_arc --help` содержит подробное описание того какие параметры принимает и на что они влияют. Всякие пути до лога, как растить версию и прочее.
