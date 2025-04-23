# Deployment
### for development
1. build: `make build`
2. run compose: `docker compose up -d`
3. attach to container `docker exec -t agent-debby-agent-1 bash1` and gen new token: `cd /usr/lib/debby/ && python manage.py new token`
### on external cloud
1. Deliver files on remote. For example using scp:
```
ubuntu@remote:~$ mkdir debby-agent

user@local:~$ scp -i cert.pem debby/Dockerfile ubuntu@remote:~/debby-agent
user@local:~$ scp -i cert.pem debby/Makefile ubuntu@remote:~/debby-agent
user@local:~$ scp -i cert.pem debby/run.sh ubuntu@remote:~/debby-agent
user@local:~$ scp -i cert.pem -r debby/patches ubuntu@remote:~/debby-agent
user@local:~$ scp -i cert.pem -r debby/src ubuntu@remote:~/debby-agent
user@local:~$ scp -i cert.pem -r debby/config ubuntu@remote:~/debby-agent
```
or
```
user@local:~$ REMOTE_AGENT=agent@remote

user@local:~$ tar cvf debby-agent.tar debby/config/ debby/patches/ debby/src/ debby/Dockerfile debby/Makefile debby/run.sh
user@local:~$ scp debby-agent.tar $REMOTE_AGENT:~/debby-agent.tar
user@local:~$ ssh $REMOTE_AGENT
agent@remote:~$ tar xvf debby-agent.tar
agent@remote:~$ rm debby-agent.tar
agent@remote:~$ mv debby debby-agent
```
2. Install on remote docker and make tools
3. Build, run deamonized, attach if needed:
```
ubuntu@remote:~/debby-agent$ sudo make build
ubuntu@remote:~/debby-agent$ sudo make run
ubuntu@remote:~/debby-agent$ sudo make attach
```
4. Generate token inside container:
```
$ cd usr/lib/debby
$ python manage.py new token
```
5. Add auth header for requests: `X_AUTH_TOKEN: <TOKEN>`

### on nessus
```
make attach
cd /usr/lib/debby
python manage.py get token
<save token>
exit
docker kill debby-agent-qloud
make run
make attach
cd /usr/lib/debby
python manage.py set token <put token>
```

# Run container
## Using pregenerated certificates
To use pregenerated certificate pass it through volume `-v /path/to/your/cert:/cert_key`. It must contain files `private.key` and `cert.pem`. If entry script dont see /cer_key folder it generates selfsigned certificate.
## Port forward
Internal nginx server listen for connections on port 443. Use docker options to map host port to container's port (eg. `-p 10443:443`).
## Environment Variables
1. AGENT_CONCURRENCY - concurrent scans / amount of workers. [default=20]


# Add new engine
## example:
* zookeeper engine: https://github.yandex-team.ru/security/debby/pull/4 + https://github.yandex-team.ru/security/debby/pull/5 + https://github.yandex-team.ru/security/debby/commit/26a0ce0fb50fb259131db3346ae07f83b00d3e61

## API
##### POST 
```
curl -H "Content-Type: application/json" -X POST -d '{"engine":"nmap", "profile":{"args":"-sS -p 1-1024 127.0.0.1"}}' https://debby-agent:443/api/v1/scans
```
##### GET
```
curl -i -H "Accept: application/json" -X GET https://debby-agent:443/api/v1/scans/12345678-1234-1234-1234-1234567890ab
```
##### DELETE
```
curl -H "Content-Type: application/json" -X DELETE https://debby-agent:443/api/v1/scans/12345678-1234-1234-1234-1234567890ab
```
##### GET scans info count
```
curl -i -X GET https://debby-agent:443/api/v1/scans
{
  "results": {
    "canceled": 0, 
    "finished": 1, 
    "in progress": 1, 
    "pending": 0
  }, 
  "status": "ok"
}
```



# Old
## Troubleshooting
### IPv6 Network
1. Add the following json to file /etc/docker/daemon.json:
```
{
	“ipv6”: true,
	“fixed-cidr-v6”: “2001:db8:1::/64”
}
```
2. Restart daemon's config: `sudo systemctl restart docker`
3. Now can avoid using `--network host`
