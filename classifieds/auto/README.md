<img align="right" width="120" height="120" src="https://lh3.googleusercontent.com/_etTrpSQWtrdcNvq3-1rUbodPc4wVwNNIOOrkBJ3o5U7vePX91Fp_1IH6rNUoiBSqQ=s180">

# [auto.ru](https://auto.ru) searcher backend


## Service list

This repo hosts a source code of following services:

<details><summary>searcher</summary>
<p>

* [TeamCity job](https://t.vertis.yandex-team.ru/viewType.html?buildTypeId=bt2265)
* [Shiva](https://admin.vertis.yandex-team.ru/services/auto2-searcher)
* [Logs](https://grafana.vertis.yandex-team.ru/explore?orgId=1&left=%5B%22now-1h%22,%22now%22,%22vertis-logs%22,%7B%22expr%22:%22service%3Dauto2-searcher%20layer%3Dprod%20%22,%22fields%22:%5B%22thread%22,%22context%22,%22message%22,%22rest%22%5D,%22limit%22:100%7D%5D)
* __test request /apiCars__ http://auto2-searcher-api.vrts-slb.test.vertis.yandex.net/apiCars
* Remote debug port: 9999

</p>
</details>

<details><summary>shard</summary>
<p>

* [TeamCity job](https://t.vertis.yandex-team.ru/viewType.html?buildTypeId=bt2264)
* [Shiva](https://admin.vertis.yandex-team.ru/services/auto2-shard)
* [Logs](https://grafana.vertis.yandex-team.ru/explore?orgId=1&left=%5B%22now-1h%22,%22now%22,%22vertis-logs%22,%7B%22expr%22:%22service%3Dauto2-shard%20layer%3Dprod%20%22,%22fields%22:%5B%22thread%22,%22context%22,%22message%22,%22rest%22%5D,%22limit%22:100%7D%5D)
* Remote debug port: 9997

</p>
</details>

<details><summary>ext-data-service</summary>
<p>

Деплой отдельных джоб в шиву:  https://wiki.yandex-team.ru/vertis/search/auto/spisok-periodicheskix-dzhob/

</p>
</details>

<details><summary>wizard</summary>
<p>

* [TeamCity job](https://t.vertis.yandex-team.ru/viewType.html?buildTypeId=bt2284)
* [conductor](https://c.yandex-team.ru/packages/yandex-auto2-wizard)
* __logs.testing__ wizard-01-sas.test.vertis.yandex.net:/var/log/auto2/ru/auto2-wizard.log
* __logs.prod__ l.vertis.yandex.net:/var/remote-log/wizard-01-sas.prod.vertis.yandex.net/auto2/ru/auto2-wizard.log
* [wizard readme](auto-wizard/README.md)

</p>
</details>

## Requirements

- Java 8 
  - make sure Maven runs from terminal with this version
  - in case of `jenv` install maven plugin
- Apache Maven 2.2.1+

## Getting started Common part

Make sure two-factor authentication is activated in your ```Github``` account.

Add an ssh-key to your GitHub account, and then ```git clone git@github.com:YandexClassifieds/auto.git```

Copy `settings.xml` to `~/.m2/`, merge with existing or override with `Settings > Build, Execution, Deployment > Build Tools > Maven > User settings file > override = true`

Open a `pom.xml` file as a project in your favorite IDE(A)

If IDE can't link generated files
see [IDE Settings](https://github.com/YandexClassifieds/auto#ide-settings)

## Setup deployment configuration for your Dev host

Read more about dev-environment here https://wiki.yandex-team.ru/vertis-admin/dev-containers/

Set up a deploy with an assembly POMs inside components and put an
`upload.properties` file inside root folder with the following content:

    ssh.host=YOUR_DEV_HOST_NAME
    
Run this commands on `YOUR_DEV_HOST_NAME`:
```
mkdir -p ~/dist
sudo mkdir -p /var/run/auto2/ru
sudo mkdir -p /var/log/auto2/ru
sudo useradd auto2
sudo chown -R auto2:nogroup /var/run/auto2/ /var/log/auto2/
sudo touch /var/log/auto2/ru/auto2-searcher.log

sudo apt-get install yandex-auto2-config-ru-testing
sudo apt-get install yandex-auto2-ext-data
```

and create a symbolic link:
```
whereis java
sudo ln -s YOUR_PATH/java /usr/local/java8/bin/java
```

## Getting started for Searcher

Do [Common part](https://github.com/YandexClassifieds/auto#getting-started) first

For searcher open pom.xml in Maven, if you didn't do that in common part:

`Maven > Add Maven Projects > select auto-searcher/src/assembly/pom.xml`

Run this on localhost — to deploy on host that you point in `upload.properties`:
```
make searcher clean
make searcher compile
make searcher deploy
```

Or just

```
make searcher clean compile deploy run
```

For more details — see `Makefile`.

Call your host with Searcher: `http://YOUR_DEV_HOST_NAME:34389`

For check that your host with Searcher is up do simple query:
`http://YOUR_HOST_NAME:34389/apiCars`

### Searcher load testing recommendations
We use [Lunapark](https://lunapark.yandex-team.ru/) – Yandex' own platform to orchestrate load testing (that runs [this beast](https://github.com/yandex/yandex-tank) under the cover).
You can look for more detailed notes and howtos [here](https://wiki.yandex-team.ru/users/aafa/Nagruzochnye-strelby-po-sercheru/).   

## Debug configuration for Intellij Idea
Open [the dialog](https://www.jetbrains.com/help/idea/creating-and-editing-run-debug-configurations.html) 
to create run/debug configuration. Add new "Remote" configuration. 
Set the required port (e.g., ```9999``` for Searcher) and save the configuration.

## Remote debugging Searcher
Connect to your vm with debugging port forwarded. 
You will be able to debug remotely while this connection is active. 
```
ssh -L9999:localhost:9999 YOUR_DEV_HOST_NAME
```

## Remote debugging EDS
To be able running some tasks add file `/conf/auto2-ext-data-service.local.conf` at EDS resources
with text:
```
auto.extdata.service {
  extdata-server {
    curator {
      namespace = "auto2/$YOUR_NAME/ru"
    }
  }
}
```

Connect to your vm with debugging port forwarded. 
You will be able to debug remotely while this connection is active. 
```
ssh -L9989:localhost:9989 YOUR_DEV_HOST_NAME
```

## Run Searcher with prod indexes
Add line `auto.s3edr.s3.bucket = auto` to `auto-searcher/src/main/resources/auto-searcher-local.properties`.

Do clean, compile and deploy

## Development flow

This repository sticks to the following development cycle (for each service):

1. Address a task - create a branch with ticket ID in its name. Suggested branch naming format is:
    ```
    feature/QUEUE-1234_one_more_thing
    bug/QUEUE-2345_endless_loop
    hotfix/QUEUE-3456_massive_fckp
    ```

2. Implement your solution. \
Make sure the code is well-formatted:
    ```
    make format 
    make format-java
    ``` 
3. Create pull request for your branch.
4. Merge your branch into ```origin/testing``` branch.
5. Run [TeamCity](https://t.vertis.yandex-team.ru/project.html?projectId=Auto20&tab=projectOverview) 
job on ```testing``` (```default```) branch to deploy your changes into testing environment.\
When build is finished a link to the ```conductor ticket``` will occur in the ```Build log```.\
If ```conductor ticket``` has not been created you can do it manually.\
When ```conductor ticket``` is in ```done``` status you can proceed.
6. Make sure your solution works on testing environment.
7. Set ```tested``` / ```ready to deploy``` status for your ticket in task tracker.\
This could be important for services under the SOX regulation.
8. Merge pull request into ```origin/master``` (It must be approved).
9. Run [Make Release job](https://t.vertis.yandex-team.ru/viewType.html?buildTypeId=Auto20_MakeRelease) \
9.1. Choose your service in ```Parameters``` tab.\
9.2. Choose branch ```master``` in ```Changes``` tab.\
It will generate and commit ```changelog``` file and than ```TeamCity``` will trigger a job to build your service.\
When build is finished a link to the ```conductor ticket``` will occur in the ```Build log```.\
When ```conductor ticket``` is in ```done``` status you can proceed.
10. Promote ticket to ```prestable``` (if service has this kind of environment).\
10.1. Make sure that everything works fine in ```prestable``` environment (logs and monitoring are at your disposal).
11. Promote ticket to ```stable``` (this action usually requires an approve by one of a team members).\
11.1. Make sure that everything works fine in ```stable``` environment.
12. Surprisingly enough that's not it yet.\
    At this moment ```testing environment``` is occupied by build from ```master branch```.
13. Merge ```origin/master``` into ```origin/testing```.
14. Run ```TeacmCity``` job on ```testing``` (```default```) branch to deploy your changes into testing environment.\
    When build is finished a link to the ```conductor ticket``` will occur in the ```Build log```.\
    When ```conductor ticket``` is in ```done``` status you can proceed.
15. That's it, you can close your task.

## Publish micro-core

Bump `yandex.auto-micro-core.version` and then do
```
make publish-micro-core
``` 

## Health Check
https://md.vertis.yandex.net/auto/web/index.html

## IDE Settings

#### Max file size (for IntelliJ IDEA)

Help -> edit custom properties

add this line
```
idea.max.intellisense.filesize=9999
```

#### Scalafmt formatting 
Install [this](https://plugins.jetbrains.com/plugin/8236-scalafmt) plugin, IDEA will do the rest  
It is recommended to set "Format on save" flag as described [here](https://scalameta.org/scalafmt/docs/installation.html)
 
See full details [here](https://github.com/YandexClassifieds/auto/pull/852).

#### Java formatting

Use [this](https://github.com/google/google-java-format#intellij-android-studio-and-other-jetbrains-ides) manual to install and activate google-java-format IntelliJ plugin.

When enabled, it will replace the normal `Reformat Code` action, which can be triggered from the `Code` menu or with the `Ctrl-Alt-L` (by default) keyboard shortcut.

## Our team

Svyatoslav Demidov [:bust_in_silhouette:staff](https://nda.ya.ru/3TPHiM)
[:envelope: Telegram](https://t.me/demidov)

Andrey Korzinev [:bust_in_silhouette:staff](https://nda.ya.ru/3TPHqA)
[:envelope: Telegram](https://t.me/fellrond)

Makarchuk Azamat [:bust_in_silhouette:staff](https://nda.ya.ru/3UNt8v)
[:envelope: Telegram](https://t.me/azamat_makarchuk)

Artyom Pashinin [:bust_in_silhouette:staff](https://nda.ya.ru/3UZRUS)
[:envelope: Telegram](https://t.me/BMo6895)

Alexey Afanasev [:bust_in_silhouette:staff](https://nda.ya.ru/3VgLdZ)
[:envelope: Telegram](https://t.me/avafanasiev)
