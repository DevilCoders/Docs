# Про LXC контейнер для задачи
Эта задача запускает приложение на 80 порту, из чего следует, что во время запуска он должен быть свободен. 
К сожалению, в стандартных браузерных контейнерах 80-й порт бывает занят другими сервисами, поэтому для задачи приходится собирать свой, практически пустой контейнер.
 
# Про параметры контейнера
Для сборки надо запустить задачу `SANDBOX_LXC_IMAGE`. 

Собирать можно под 16.04 и 18.04. Разница лишь в том, что в 16.04 нет antlr4 версии 4.7.2, а в pip нет рантайма (antlr4-python2-runtime) версии 4.5.1, поэтому при их использовании появляется предупреждение о несоответствии версий бинарника antlr4 и antlr4-python2-runtime. 
Но это довольно минормая проблема. 
## 16.04:
* **Container resource type**: LXC_CONTAINER
* **Ubuntu release**: xenial
* **Attributes to add to resulting resource**:  `platform: linux_ubuntu_16.04_bionic, ttl: 365`
* **Create custom LXC image**: True (поставить галочку)
* **Install all common packages**: True (поставить галочку)
* **List of packages to install during final stage, space-separated**: `antlr4=4.5.1-2`


## 18.04:
* **Container resource type**: LXC_CONTAINER
* **Ubuntu release**: bionic
* **Attributes to add to resulting resource**:  `platform: linux_ubuntu_18.04_bionic, ttl: 365`
* **Create custom LXC image**: True (поставить галочку)
* **Install all common packages**: True (поставить галочку)
* **List of packages to install during final stage, space-separated**: `antlr4=4.7.2-1~18.04 python-dev=2.7.15~rc1-1 libssl-dev=1.1.1-1ubuntu2.1~18.04.5 build-essential=12.4ubuntu1`
Все остальные поля сделать пустыми, **удалить значения по умолчанию**.
