# Как работать с гитом в паспорте

Мы работаем [по гитфлоу] [1]. Значительно упрощает процесс специальный [набор скриптов] [2].

[1]: https://www.atlassian.com/git/workflows#!workflow-gitflow
[2]: https://github.com/nvie/gitflow

## Ветки и naming convention

 * master — соответствует продакшену, все релизы отмечены тэгами
 * develop — ветка с активной разработкой
 * rc-<номер релиза> — релизные ветки
 * hotfix-<номер релиза> — хотфикс-ветки
 * feature/XXXXX-0000.slug — feature-ветки


## Таски
Фичи начинаются из девелопа и заканчиваются в девелопе

### Я начинаю делать таск
    git checkout develop
    git pull origin develop
    git checkout -b XXXXX-0000.slug
    
#### gitflow вариант
    git flow feature start XXXXX-0000.slug
    
    
### Я начинаю чинить баг в релизе
    git checkout rc-<version>
    git pull origin rc-<version>
    git checkout -b <taskID>

### Я закончил с фичей или багом
    см. Как завести пулл-реквест в Review.md 


## Релизы
Релизы начинаются из девелопа, а заканчиваются мерджем в мастер и девелоп.

### Я хочу сделать релиз
    git checkout develop
    git pull origin develop
    git checkout -b rc-<release>
    
#### gitflow вариант
    git flow release start <release>


### Я собираю пакет
Перед сборкой пакета нужно подмерджить мастер, чтобы не затереть своей выкаткой предыдущие изменения

    git checkout <release>
    git merge origin/master

### Я выкатил релиз
Выкаченный релиз нужно размерджить в мастер и девелоп и в девелопе поставить тэг

    git checkout master
    git pull origin master
    git merge --no-ff origin/rc-<release>
    git tag <released build number as tagname (0.1.75-15)>
    git push origin <tagname>
    git push origin master
    git checkout develop
    git pull origin develop
    git merge --no-ff origin/rc-<release>
    git push origin develop

#### gitflow вариант
    git flow release finish <release>


## Хотфиксы
Хотфиксы — это срочные релизы, которые нет времени долго тестировать.
Начинаются в мастере, вмердживаются в мастер и девелоп

### Я создаю хотфикс
    git checkout master
    git pull origin master
    git checkout -b hotfix-<release>

#### gitflow вариант
    git flow hotfix start <release>


### Я выкатил хотфикс
Смотри "Я выкатил релиз"


## Частные случаи
— Я сделал свою большую задачу в отдельной feature-ветке, как её выкатить?  
— Вмерджить в девелоп, создать релиз из девелопа, смотри "я закончил фичу" и "я хочу сделать релиз"
