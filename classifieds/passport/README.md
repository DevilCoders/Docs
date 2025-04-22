# Vertical Passport

## Structure
- passport-core - base building blocks (models, utils)
- passport-dao - data access layer, services
- passport-server - common parts for deployable service
- passport-api - service to process user requests 
- passport-controller - service to run periodic tasks

## Wiki
https://wiki.yandex-team.ru/vertis/passport/

## Docker version
dev: http://dev-passport-api.vrts-slb.test.vertis.yandex.net  
testing: http://passport-api.vrts-slb.test.vertis.yandex.net
testing branch: http://pull-???.passport-api.vrts-slb.test.vertis.yandex.net
prod: http://passport-api.vrts-slb.prod.vertis.yandex.net

## Swagger
http://passport-api.vrts-slb.test.vertis.yandex.net/swagger/?url=/api/2.x/

## Development

### Make release
Run autorelease in teamcity:
https://t.vertis.yandex-team.ru/project.html?projectId=VertisPassport

### Deploy to dev host
Set your dev host address in upload.properties
To deploy run
~~~
make deploy-api
make deploy-controller
~~~

### Debug
DEBUG_PORT=6212 for passport-api and passport-controller.
Make a tunnel to debug them remotely
~~~
ssh -L 6212:localhost:6212 YOUR_HOST_NAME
~~~
#### Debug configuration for Intellij Idea
Open [the dialog](https://www.jetbrains.com/help/idea/creating-and-editing-run-debug-configurations.html)
to create run/debug configuration. Add new "Remote JVM Debug" configuration.
Set the required port (e.g., ```6212``` for passport) and save the configuration.
