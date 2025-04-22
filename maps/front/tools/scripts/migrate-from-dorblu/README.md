# Install

**Warning**
  * If your Nginx logs are used for reports in Analytics or Statistics, make sure they support working with new paths before migrate


## Execution steps

### Preparation

1. Install dorblu migrator package **globaly**:

   ```
   $ npm install -g --registry=https://npm.yandex-team.ru/ @yandex-int/ymaps-dorblu-migrator
   ```

2. Update qtools:

   ```
   $ npm i @yandex-int/qtools@latest --save-dev --registry=https://npm.yandex-team.ru/
   ```

3. Update permissions for qtools token. Just click [link](https://oauth.yandex-team.ru/authorize?response_type=token&client_id=ff00df99f57b435e952e51156743200a) and press **Agree**. Token will be the same, only permissions will be changed.

   ```sh
   export QTOOLS_TOKEN=${value}
   ```

4. Generate config for alerts based on [arcadia configs](https://a.yandex-team.ru/arc/trunk/arcadia/maps/config/dorblu/maps) and add it to `qtools.json`.

   **Important:** Script works only with `JSON`.
   If you have Qtools config in `yaml` format, update qtools version and [convert](https://github.yandex-team.ru/maps/qtools/releases/tag/v0.1.0) config

   Run command in directory with your qtools config.

   ```
   $ ymaps-dorblu-migrator pull-config
   ```

5. Open `qtools.json` and check **geoSpecific.monitorings** section. Take your attention for:

   * Limits of every check (All values are absolute, not in percentage).
   * For correct order of maintainers list.

6. Update base image version to the [latest enforced version](https://github.yandex-team.ru/maps/docker-baseimages/blob/master/ubuntu-node/versions.json#L19) in your Dockerfile.

   ```Dockerfile
   FROM registry.yandex.net/maps/${IMAGE_NAME}:${VERSION}
   ```

7. Make sure your copy `qtools.json` to **WORKDIR**. It will be used to generate roquefort configs:

   ```Dockerfile
   WORKDIR /usr/local/app # WORKDIR variable must be set
   COPY .qtools.json .
   ```

8. Add command to Dockerfile to generate roquefort config on build stage:

   ```Dockerfile
   RUN maps_init
   ```

9. Bump the version of your project, build new image and deploy it to testing.
   **IMPORTANT:** make sure that Docker image was successfully build.

   ```
   $ bump version
   $ node_modules/.bin/qtools release testing
   ```

10. Make sure that Qloud app work well in testing.

### Migration

1. Set downtime for dorblu alerts.

   ```
   $ ymaps-dorblu-migrator set-downtime
   ```

2. Remove your service in Juggler.
Edit [maps_front.yml](https://a.yandex-team.ru/arc/trunk/arcadia/maps/config/juggler/geo_juggler/maps_front.yml?edit=true) and add anybody from devops as a reviewer.

3. Wait 5-10 mins for e-mail with subject `[Sandbox] ANSIBLE_JUGGLER_RUNNER`.

4. Deploy your production.

   ```
   $ node_modules/.bin/qtools release production
   ```

5. Add golovan alerts instead of dorblu ones.

   ```
   $ node_modules/.bin/qtools alerts push --force
   ```

   **NOTE**: The `--force` flag is used here only for initializaion purposes. Afterwards, you should first use the command without it, and only if you're sure that you want to apply your changes, add the `--force` option.

6. Remove downtime for dorblu alerts.

   ```
   $ ymaps-dorblu-migrator remove-downtime
   ```

7. Remove geo_juggler config of your project from [arcadia](https://a.yandex-team.ru/arc/trunk/arcadia/maps/config/juggler/geo_juggler/maps_front) and dorblu config from [here](https://a.yandex-team.ru/arc/trunk/arcadia/maps/config/dorblu/maps)

8. Update documentation in `README.md` and `ABC service`:

   * YASM dashboard instead of Grafana (see below).
   * New juggler links (see below).
   * Nginx logs for YQL stat moved to `//home/logfeller/logs/maps-front-production-log/1d` (YT path: https://yt.yandex-team.ru/hahn/navigation?path=//home/logfeller/logs/maps-front-production-log).
   * `Dorblu Agent` from logs:

     ```diff
     - | Nginx, DoBlu Agent, Juggler Client, Push client | `/var/log/supervisor/` |
     + | Nginx, Juggler Client, Push client | `/var/log/supervisor/` |
     ```

   To get new links execute:

   ```
   $ ymaps-dorblu-migrator get-links
   ```
