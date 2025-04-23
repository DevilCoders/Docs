# Собираем базовый образ
docker build -f Dockerfile.base-bionic -t paysys_base .

# Выбираем среду (testing/production), версию balance-common-config и yandex-trust
emacs tools/ansible-docker/roles/trust-lpm/defaults/main.yml

# Собираем образ lpm
docker build --build-arg APP_NAME=trust-lpm --build-arg BASE_IMAGE=paysys_base -t registry.yandex.net/paysys/deploy:trust-lpm_3.190.2_test_4.0.489_v1 .

# Пушим в репозиторий
docker push registry.yandex.net/paysys/deploy:trust-lpm_3.190.2_test_4.0.489_v1
