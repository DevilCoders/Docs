Capa Partnerdata Feedloader
===


###Wiki

https://wiki.yandex-team.ru/vertis/feedloader




###Assembly

Project assembly is based on Maven.
Each command must be executed from project root directory.

#### partnerdata-feedloader
  * Clean 
    
    `mvn clean --partnerdata-feedloader --also-make`
  * Compile
    
    `mvn compile --partnerdata-feedloader --also-make`
  * Test
    
    `mvn test --partnerdata-feedloader --also-make`
  * Deploy to development
    
    `mvn install --projects partnerdata-feedloader --also-make -P development-deploy`
        
    There is `upload.properties` file must be placed in `partnerdata-feedloader/assembly` directory.
    It must contain `ssh.username` and `ssh.host` properties. Example of `upload.properties`:
    
    ```
    ssh.username=dimas
    ssh.host=dev23i.vs.os.yandex.net
    ```
         
#### partnerdata-feedloader-scheduler
  * Clean 
    
    `mvn clean --partnerdata-feedloader-scheduler --also-make`
  * Compile
    
    `mvn compile --partnerdata-feedloader-scheduler --also-make`
  * Test
    
    `mvn test --partnerdata-feedloader-scheduler --also-make`
  * Deploy to development
    
    `mvn install --projects partnerdata-feedloader-scheduler --also-make -P development-deploy`
        
    There is `upload.properties` file must be placed in `partnerdata-feedloader-scheduler/assembly` directory.
    It must contain `ssh.username` and `ssh.host` properties. Example of `upload.properties`:
    
    ```
    ssh.username=dimas
    ssh.host=dev23i.vs.os.yandex.net
    ```
    
#### partnerdata-feedloader-transport
  * Clean 
    
    `mvn clean --partnerdata-feedloader-transport --also-make`
  * Compile
    
    `mvn compile --partnerdata-feedloader-transport --also-make`
  * Test
    
    `mvn test --partnerdata-feedloader-transport --also-make`
  * Deploy to development
    
    `mvn install --projects partnerdata-feedloader-transport --also-make -P development-deploy`
        
    There is `upload.properties` file must be placed in `partnerdata-feedloader-transport/assembly` directory.
    It must contain `ssh.username` and `ssh.host` properties. Example of `upload.properties`:
    
    ```
    ssh.username=dimas
    ssh.host=dev23i.vs.os.yandex.net
    ```


###Integration with IntelliJ IDEA
For run builds from IntelliJ IDEA should one should:
  * have `.idea` (directory) based IDEA project
  * copy run configurations from `idea_run_configurations` directory to `.idea/runConfigurations`:
  ```
  cp idea_run_configurations/* .idea/runConfigurations/
  ```

These run configurations will be available 
  - via `Run Configurations` panel and 
  - via `Maven Projects` tab: `feedloader` -> `Run Configurations`
  

###TeamCity Builds

Build configurations are placed here - http://teamcity.yandex-team.ru/project.html?projectId=feedloader.

####Debian Builds

One can easily perform component release by commit `debian/changelog` file with urgency `autodeploy` and branch `testing`.

Example of `debian/changelog` record for trigger autorelease build:

```
yandex-partnerdata-feedloader (1.0-000) testing; urgency=autodeploy

  * Integration CAPA-000 - Some comment 

 -- Dmitry Schitinin <dimas@yandex-team.ru>  Wed, 22 Apr 2015 18:18:09 +0300
```
