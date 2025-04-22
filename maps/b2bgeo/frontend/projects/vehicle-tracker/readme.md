# Vehicle Tracker Frontend [![Build Status](https://drone.yandex-team.ru/api/badges/B2BGeo/vehicle-tracker-frontend/status.svg)](https://drone.yandex-team.ru/B2BGeo/vehicle-tracker-frontend)

## Run

    npm install
    NODE_ENV=development npm start

    //windows
    set NODE_ENV=development
    npm start

## Options

##### Proxy track requests to tracker backend

Specify `apiProxyTo` in [configs/development](configs/development.js#L13)

## Testing

Deployed to [qloud](https://qloud-ext.yandex-team.ru/projects/b2bgeo/ya-courier/vehicle-tracker-frontend-test)

Available at https://courier-dev.common.yandex.ru/courier/tracking/{track_id}

## Production

Deployed to [qloud](https://qloud-ext.yandex-team.ru/projects/b2bgeo/ya-courier/vehicle-tracker-frontend-prod)

Available at https://yandex.ru/courier/tracking/{track_id}


