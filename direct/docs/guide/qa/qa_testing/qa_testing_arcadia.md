# Повседневная работа с Arcadia

## Arc
[Официальные инструкции](https://docs.yandex-team.ru/devtools/src/arc/workflow)

<br>

В начале в скобках бранч, в котором находимся

***На Windows mount и unmount*** <br><br>
Обновить arc <br>
```bash
arc --update
```

Mount и unmount<br>

```bash
arc mount -m arcadia
```

```bash
arc unmount arcadia
```

***Если на Windows не работают заглавные буквы***

```bash
remove-module psreadline
```

**Отвести новый бранч** <br>

```bash
(trunk) $ arc checkout -b my-feature
```

**Посмотреть список измененных файлов** <br>

```bash
(my-feature) $ arc status
```

**Добавить файлы в коммит** <br>

```bash
(my-feature) $ arc add code.cpp project/myfile2.txt
```

**Закоммитить изменения** <br>

```bash
(my-feature) $ arc commit -m "my commit message"
```

**Подтянуть свежий trunk** <br>

```bash
(my-feature) $ arc pull trunk
(my-feature) $ arc rebase trunk
```

**Создать пулл реквест** <br>

```bash
(my-feature) $ arc pr create --push -m "my first pull request"
```

**Удалить ветку с сервера** <br>

```bash
$ arc push -d users/username/my-feature
```

**Подтянуть изменения из транка в свою ветку** <br>

```bash
(my-feature) $ arc pull trunk
(my-feature) $ arc rebase trunk
```

**Запушить свежие изменения в свой существующий pr** <br>

```bash
(my-feature) $ arc push
```

**Подтянуть свежую версию ветки** <br>

```bash
(my-feature) $ arc pull
```





--
<br>
В случае неактуальности информации на данной странице можно обращаться к [Олегу Судареву](https://staff.yandex-team.ru/sudar)
