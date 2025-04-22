### Собрать stubimage

```
ya package --docker --docker-network=host --docker-repository=maps docker/pkg.json
```
В ответе будет фраза `Successfully built <image hash>`

### Сменить тег образа

```
docker tag <image hash> registry.yandex.net/maps/core-stubimage:<target stubimage tag>
```

### Запушить образ в репозиторий

```
docker push registry.yandex.net/maps/core-stubimage:<target stubimage tag>
```

### Обновить используемый stubimage в Sedem

Поменять [хардкод](https://a.yandex-team.ru/arc_vcs/maps/infra/sedem/cli/modules/rtc.py?rev=23cff17c033f603e1097de8d887e26c7dd9a18ee#L26), закоммитить и зарелизить cli.
