# gpu_app_runner

Скрипт для `job-command` JOB кубика с torch.
Torch устанавливается в `layer` и недоступен в окружении приложения собранного `ya make`

Этот скрипт тоже не нужно собирать в бинарник и передавать через Sandbox ресурс в ресурсы Nirvana кубика,
нужно его передавать как `text` файл, что бы этот скрипт имел доступ к окружению в момент исполнения `Sandbox Task`


## job-command

    bash -c 'python3.8 ${resource["gpu_app_runner.py"]} ${input["script"]} ${output["result"]} ${input["params"]}'
