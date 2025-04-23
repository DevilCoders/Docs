Создание образа для тестирования: https://sandbox.yandex-team.ru/task/1352267814/view
```
apt-get --yes update
apt-get --yes install build-essential

echo "install nodejs 12"
KEYRING=/usr/share/keyrings/nodesource.gpg
curl -fsSL https://deb.nodesource.com/gpgkey/nodesource.gpg.key | apt-key add -
VERSION=node_12.x
DISTRO="$(lsb_release -s -c)"
echo "deb [signed-by=$KEYRING] https://deb.nodesource.com/$VERSION $DISTRO main" | tee /etc/apt/sources.list.d/nodesource.list
echo "deb-src [signed-by=$KEYRING] https://deb.nodesource.com/$VERSION $DISTRO main" | tee -a /etc/apt/sources.list.d/nodesource.list
apt-get --yes update
apt-get --force-yes install nodejs

echo "install and run clickhouse"
apt-key adv --keyserver keyserver.ubuntu.com --recv E0C56BD4
echo "deb http://repo.yandex.ru/clickhouse/deb/stable/ main/" | tee /etc/apt/sources.list.d/clickhouse.list
apt-get --yes update
apt-get --yes install clickhouse-server clickhouse-client

echo "install and run postgresql"
apt-get --yes install postgresql postgresql-contrib

echo "sandbox ALL=(postgres) NOPASSWD: ALL" | (EDITOR="tee -a" visudo)
echo "sandbox ALL=(ALL:ALL) NOPASSWD: /usr/bin/service" | (EDITOR="tee -a" visudo)

echo "local all all trust" > /etc/postgresql/9.3/main/pg_hba.conf
echo "host all all localhost trust" >> /etc/postgresql/9.3/main/pg_hba.conf
echo "host all all 127.0.0.1/32 trust" >> /etc/postgresql/9.3/main/pg_hba.conf
echo "host all all ::1/128 trust" >> /etc/postgresql/9.3/main/pg_hba.conf

cat /etc/postgresql/9.3/main/postgresql.conf
echo "hot_standby = on" >> /etc/postgresql/9.3/main/postgresql.conf

mkdir /var/lib/pgsql
mkdir /var/lib/pgsql/data
chown -R postgres /var/lib/pgsql
```