Ресурс с тестами надо собрать руками
```shell
ya upload data
```
и обновлять id руками в `__init__.py` или в `a.yaml` нужного CI .

`create_lxc_container_with_docker.sh` нужен чтобы собрать lxc образ
на котором будет запускаться sandbox задача.
Содержимое этого файла надо скормить задаче `BUILD_LXC_IMAGE`. 
Выхлоп `BUILD_LXC_IMAGE` надо прописать в `Task.Parameters.container.default_value` .