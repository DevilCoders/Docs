# Как пользоваться

При добавлении новой версии нужно, чтобы было две версии ресурсов постгреса для каждой платформы:
1. jar файл с архивом (пример: https://sandbox.yandex-team.ru/resource/1251335516/view)
1. папка pgsql (имя важно!) с содержимым внутреннего архива (пример https://sandbox.yandex-team.ru/resource/1490193510/view)

Эти ресурсы должны включаться в разные файлы:
1. этот ресурс нужно включать в `ya.make` как `EXTERNAL_JAR`, чтобы система сборки генерировала проект с нужным постгресом в classpath
1. этот ресурс нужно включать в файл `recipe.inc` (e.g. ./11.6/recipe.inc), в котором описан рецепт и ресурсы постгреса для этого рецепта. Этот рецепт нужно включать в те модули, где постгрес нужен

# Сборка ресурсов с postgres-ом нужной версии

Собранный postgresql нужной версии можно взять по ссылке https://search.maven.org/search?q=io.zonky . Нужно скачать
бинарники нужной версии. перепаковать и залить в sandbox.

## Сборка ресурса sandbox

### Сборка и загрузка jar файла
```shell script
cd $HOME/pginstall # для Mac переходим в директорию, куда распаковали архив
tar -czf postgres.tgz bin lib share
zip -r postgres-13.2-linux-x64.jar postgres.tgz
ya upload postgres-13.2-linux-x64.jar --ttl=inf
```

### Сборка и загрузка директории
```shell script
cd $HOME/pginstall # для Mac переходим в директорию, куда распаковали архив
# заменяем симлинки настоящими файлами, т.к. sandbox не загружает симлинки
for link in $(find . -type l)
do
  loc="$(dirname "$link")"
  dir="$(readlink "$link")"
  rm "$link"
  cp "$loc/$dir" "$link"
done
cd $HONE
mv pginstall pgsql
ya upload pgsql --ttl=inf
```
