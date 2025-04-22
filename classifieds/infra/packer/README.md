xenial-common-cloud.json - конфиг для базового образа, включая common пакеты

Как использовать:
1. Устанавливаем packer ( https://cloud.yandex.ru/docs/solutions/infrastructure-management/packer-quickstart#install-packer )
2. Получаем ключ от service account из [yav](https://yav.yandex-team.ru/secret/sec-01edxy4am1ke19n2k3tt6dcbxs/explore/versions).
Путь до ключа нужно положить в env YC_SERVICE_ACCOUNT_KEY_FILE. Например, YC_SERVICE_ACCOUNT_KEY_FILE=/Users/spooner/key.json
3. Запускаем сборку нового образа:``packer build xenial-common-cloud.json`` (для образа на ubuntu 16.04), либо ``packer build focal-common-cloud.json`` ( для образа на ubuntu 20.04).
