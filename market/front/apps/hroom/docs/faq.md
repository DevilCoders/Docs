## FAQ
1. Как открыть консоль postgres на локальной машине внутри docker:
```bash
docker exec -ti `docker ps | grep postgre | awk '{print $1}'` bash
su root
psql -U hroom
```