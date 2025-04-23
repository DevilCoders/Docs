# How to run agent not in container
1. Install Docker
2. Install Redis: ``` sudo -y apt install redis-server ```
3. Install Debby, IVRE, nmap:
```
git clone https://github.yandex-team.ru/procenkoeg/debby debby-agent
wget https://github.com/cea-sec/ivre/archive/v0.9.11.tar.gz
tar -xf v0.9.11.tar.gz
cd ivre-0.9.11
patch -p1 < ../debby-agent/patches/ivre-0.9.11-ipv6.patch
pip install -r requirements-postgres.txt
cd ..

wget https://nmap.org/dist/nmap-7.70.tgz -O nmap.tar.gz
tar zxf nmap.tar.gz
mv nmap-* nmap
cd nmap
patch -p1 < ../debby-agent/patches/nmap_7_70_port_timestamp.patch
sudo -y apt install libssl-dev
./configure --without-ndiff --without-zenmap --without-nping \
                --without-ncat --without-nmap-update \
                --with-libpcap=included
make
sudo make install

cd ivre-0.9.11
./setup.py build
sudo ./setup.py install
cd ..

cd debby-agent/src
pip install -r requirements.txt

```
4. Run postgres container
```
cd ../docker/ivre_db_postgres
sudo make
```
5. Gen token: ``` python manage.py gen token ```
6. **OPTION** Run redis if it didnt automatically ``` redis-server ```
7. Run celery: ``` python manage.py run celery ```
8. Run debby agent: ``` python manage.py run debby ```