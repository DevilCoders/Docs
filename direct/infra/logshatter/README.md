Здоровье маркета 
https://wiki.yandex-team.ru/Market/Development/Health/

Собрать всё, запустить юнит-тесты:
```bash
./gradlew build
```

Запустить интеграционные тесты:
```bash
sudo docker-compose -f health-integration-tests/docker/docker-compose.yml up -d
./gradlew :health-integration-tests:integrationTest
```

###Для локального запуска в Idea:
1. Установить JDK 1.8, если ее еще нет

```bash
brew install openjdk@8
```

2. Добавить ее в Libraries:
```bash
sudo ln -sfn /usr/local/opt/openjdk@8/libexec/openjdk.jdk /Library/Java/JavaVirtualMachines/openjdk-8.jdk
```
3. Добавить JDK в проект (&lt;command&gt; + ;)

![Добавить JDK в проект](add_jdk.png)


4. Вписать строчки в файл ~/.gradle/gradle.properties, чтобы не было таймаутов на чтение во время сборки проекта.
```bash
systemProp.org.gradle.internal.http.connectionTimeout=180000
systemProp.org.gradle.internal.http.socketTimeout=180000
```
Если такого файла еще пока нет, создать его с указанными строчками внутри.
6. Указать в настройках Gradle скачанную JDK 
> IDE and Project Settings (&lt;command&gt; + ,) ) > Build, Execution, Deployment > Build Tools > Gradle - Gradle JVM

![установить JDK для Gradle](set_gradle_jdk.png)
7. Закоментить в build.gradle строку         
```java
  || !vendor.equals("Oracle Corporation")
```

8. Нажать на кнопку Reload All Gradle Projects в закладке Gradle

![Reload All Gradle Projects](reload_all_gradle_projects.png)

После всего этого проект соберется в Idea

