To create an atlas anomalies YT table:

1. Get your yt token from https://oauth.yt.yandex.net/

2. Get your OAuth token from https://oauth.yandex-team.ru/authorize?response_type=token&client_id=5f671d781aca402ab7460fde4050267b

3. Choose yt_table_path, for example in your home directory //home/taxi/home/<your_user_name>/atlas_anomalies

4. Get anomalies.json file from https://atlas.yandex-team.ru/api/v1/anomalies/?from_ts=1577836800&to_ts=1672531199&status=confirmed&level=unknown%2Cminor%2Cmajor&source=all&limit=400&offset=0 choosing from_ts and to_ts to your desire.

Launch following script

```
python3 taxi_atlas-anomalies/upload_atlas_anomalies_to_yt.py --anomalies_path <your_full_anomalies_json_path> --yt_token <yt_token> --oauth_token <oauth_token> --yt_table <your_table_path>
```

In case of success the following script will be prompted:

```
Success! Check your table at https://yt.yandex-team.ru/hahn/navigation?path=//home/taxi/home/dias-sadykov/atlas_anomalies
```

Go to the following link and click "Datalens" icon to visualize your new data!
