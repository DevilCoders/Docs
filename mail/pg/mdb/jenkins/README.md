# DSL описание джоб в jenkins

## Инструменты

- Плагин [Job DSL Plugin](https://wiki.jenkins-ci.org/display/JENKINS/Job+DSL+Plugin) 
  Подробный гайд: https://github.com/jenkinsci/job-dsl-plugin/wiki
- Возможные расширения:
  - [AQuA Plugin](https://github.yandex-team.ru/qatools/jenkins-aqua-plugin#job-dsl-extension)
- Джоба для сборки на [jenkins.mail.yandex.net](http://jenkins.mail.yandex.net/job/internal_generate_mdb_jobs/) 
  Пересобирается по пушу.
  
## Структура

- Все dsl скрипты из которых генерируются джобы должны заканчиваться на `.job.groovy` и 
содержать в названии имя генерируюемой джобы или ее часть, если таких внутри скрипта несколько.
- Скрипты должны располагаться в папке, соответствующей jenkins-view. 
- Bash-скрипты (и подобное), содержащиеся в степах, должны находиться рядом с джобой или в специальной подпапке `files_{название джобы}`, 
если скриптов много.
