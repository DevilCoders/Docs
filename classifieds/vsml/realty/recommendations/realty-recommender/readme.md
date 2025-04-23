## Used instruments & libraries
To run / develop / deploy service locally, you have to install the following:  
1. Docker: use `Docker for Mac`
2. yav cli:  https://vault-api.passport.yandex.net/docs/#cli
   ```bash
    sudo apt-get install yandex-passport-vault-client
    ```

#### Deploy in testing/production
1. update version in push_to_registry.sh, build docker image and push it to registry:
    ```bash
    ./push_to_registry.sh
    ```
2. Deploy with telegram shiva-bot: https://wiki.yandex-team.ru/vertis-admin/deploy/bot/ 
   1. test deploy: 
    ```telegram
    /run -l test -v %YOUR_APP_VERSION_HERE% realty-recommender
    ```
   2. promote to prod, if you need:
   (use button  `Promote`)
   or
   ```
   /run -l prod -v %YOUR_APP_VERSION_HERE% realty-recommender
   ``` 

#### Launch in docker on local machine
1. Install docker on Mac OS and update Mac OS (otherwise "docker is staring" error can occur)
 yav-deploy --configs-path . --deploy-root . --file yav.conf
2. Build docker image:
docker build -t realty-recommender .
3. Run docker image to test:
docker run --env-file local_config_env.lst --rm -t -p 8897:8897 -i realty-recommender
4. to check REST API call find offerId from moscow rent and try:
curl -v http://localhost:8897/api/v1/get_recommendations/uid/23455?rgid=34543454