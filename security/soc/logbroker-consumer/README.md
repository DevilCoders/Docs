# SOC Logbroker Consumer
Based on Python persqueue library.

Logbroker TVM Client ID can be found here:

https://abc.yandex-team.ru/services/Logbroker/resources/?tag=2&supplier=14&type=47&state=requested&state=approved&state=granted&view=consuming

## Qloud app: https://qloud.yandex-team.ru/projects/security/soc-logbroker-consumer

### How to deploy

#### Automatically
`make` OR `make Makefile`

For testing, pass topic name as argument to make (try to test one topic per try):
`make TESTING=mail--mail-nginx-access-log`
This will update topics.txt file content (use git checkout or git reset to drop temporary changes).

If you want to add custom string to result image tag:
`make CUSTOM_TAG=DEBUG_HOTFIX`


#### Manually
1. Clone repo
2. cd into it
3. `docker build -t soc-lb-consumer:<version> .`  Where version is incrementing number.
4. `docker tag soc-lb-consumer:<version> registry.yandex.net/soc/soc-lb-consumer:<version>`
5. `docker push registry.yandex.net/soc/soc-lb-consumer:<version>`
6. Update image for component in qloud app environment

If push failed, read this: https://wiki.yandex-team.ru/qloud/docker-registry/#docker18-on-mac


#### Packages

- tvm
- kikimrclient
- requests


#### Network access

Необходимые дырки для работы консюмера, запросить в Puncher-e:
- **\_\_C_LBK_MAN_CM\_\_** -- 2135, 8999, 9000
- **\_\_C_LBK_SAS2\_\_** -- 2135, 8999, 9000
- **\_\_C_LBK_SAS2\_\_** -- 2135, 8999, 9000
- **\_\_LBKNETS\_\_** -- 2135, 8999, 9000
- **man.logbroker.yandex.net** -- 2135, 8999, 9000
- **logbroker.yandex.net** -- 2135, 8999, 9000
- **tvm-api.yandex.net** -- 443


Optional:

- iva.logbroker.yandex.net
- man.logbroker.yandex.net
- myt.logbroker.yandex.net
- sas.logbroker.yandex.net
- vla.logbroker.yandex.net


### DEBUG

1. Check network access
2. Check instance of api / consumer / producer. For consumer or producer check: consumer.stop_future.result() for error message
3. Enable logging level debug for your program and for persqueue lib: [LBOPS-2746](https://st.yandex-team.ru/LBOPS-2746)
4. Ask for help in Logbroker support telegram group


### Links to Documentation

- https://wiki.yandex-team.ru/logbroker/docs/libs/python/?from=%252Flogbroker%252Fdocs%252Flib%252Fpython%252F
- https://wiki.yandex-team.ru/logbroker/docs/
- https://wiki.yandex-team.ru/logbroker/docs/network-access/
- https://github.yandex-team.ru/common-python/tvm2/#%D0%9F%D0%BE%D0%B4%D0%B3%D0%BE%D1%82%D0%BE%D0%B2%D0%BA%D0%B0-%D0%BA-%D0%B8%D1%81%D0%BF%D0%BE%D0%BB%D1%8C%D0%B7%D0%BE%D0%B2%D0%B0%D0%BD%D0%B8%D1%8E


## ToDo

1. Update docstrings in code, write documentation
2. Review ToDo's
