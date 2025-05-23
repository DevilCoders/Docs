# Changelog 
## **[pod_agent 107-1 3006211268](https://sandbox.yandex-team.ru/resource/3006211268/view)**:

### **Обратно несовместимые изменения:**
* Нет

### **Известные проблемы:**
* Нет

### **Новая функциональность :**
* Нет

### **Исправления :**
* Пофикшена проблема с провалами readiness/liveness хуков из-за incomplete http response в neh библиотеке, проявлялось на стейджах телефонии

## **[pod_agent 106-1 2936629847](https://sandbox.yandex-team.ru/resource/2936629847/view)**:

### **Обратно несовместимые изменения:**
* Нет

### **Известные проблемы:**
* Нет

### **Новая функциональность :**
* Нет

### **Исправления :**
* Пофикшена проблема с неработоспособностью GC в случае удаления/переименования вольюма

## **[pod_agent 104-1 2882369236](https://sandbox.yandex-team.ru/resource/2882369236/view)**:

### **Обратно несовместимые изменения:**
* Нет

### **Известные проблемы:**
* Нет

### **Новая функциональность :**
* Добавлена возможность отгружать системные логи подового агента с событиями пользовательских хуков
* Метрики на отгрузку системных логов

### **Исправления :**
* Нет

## **[pod_agent 103-1 2859670568](https://sandbox.yandex-team.ru/resource/2859670568/view)**:

### **Обратно несовместимые изменения:**
* Нет

### **Известные проблемы:**
* Нет

### **Новая функциональность :**
* В ручку /pod_attributes пробрасывается информация про subnet allocations
* Логи не отсылаются в случае если под агент в not active состоянии
* Логи под агента теперь хранятся намного дольше за счет отселения логов деревьев в отдельный логгер 


### **Исправления :**
* При построении дифа спеки теперь учитывается порядок секретов
* Добавлена валидация точки монтирования вольюма
* Пофикшена проблема с хранением длинных лейблов в human readable spec



## **[pod_agent 101-1 2621390537](https://sandbox.yandex-team.ru/resource/2621390537/view)**:

### **Обратно несовместимые изменения:**
* Нет

### **Известные проблемы:**
* Нет

### **Новая функциональность :**
* Добавили возможность приносить статические ресурсы в вольюм
* Может создавать неперсистентные вольюмы 
* Может [не удалять лейры после скачивания для увеличения количества пиров torrent](https://a.yandex-team.ru/arc_vcs/yp/yp_proto/yp/client/api/proto/pod_agent.proto?rev=3dfecb0aec4317cfd1b615cfd19c9d30ed85137d#L66) 
* Появилась возможность явно [отключать checksum проверку ресурсов](https://a.yandex-team.ru/arc_vcs/yp/yp_proto/yp/client/api/proto/pod_agent.proto?rev=3dfecb0aec4317cfd1b615cfd19c9d30ed85137d#L280)
* Реализована периодическая сериализация оффсетов на диск по отправке логов


### **Исправления :**
* В случае пустой readiness пробы workload - workload не влияет на интегральный статус пода
* Пофикшена склейка строк логов в случае если строка больше чем 1024 байта.




## **[pod_agent 98-1 2460258894](https://sandbox.yandex-team.ru/resource/2460258894/view)**:

{% note alert %}

вызывает рестарт контейнеров в случае использования статических ресурсов и перехода с версии релиза 96-1 или 97-1

{% endnote %}

### **Обратно несовместимые изменения:**
* Нет

### **Известные проблемы:**
* Нет

### **Новая функциональность :**
* Нет 

### **Исправления :**
* Пофикшена логика расчета хеша для статического ресурса в случае использования group id


## **[pod_agent 97-1 2460258894](https://sandbox.yandex-team.ru/resource/2460258894/view)**:

{% note alert %}

вызывает рестарт контейнеров в случае использования статических ресурсов и перехода с версий релиза ниже 96-1

{% endnote %}

### **Обратно несовместимые изменения:**
* Нет

### **Известные проблемы:**
* Нет

### **Новая функциональность :**
* **Поддержка cgroupfs** 

### **Исправления :**
* Нет


## **[pod_agent 96-1 2362157802](https://sandbox.yandex-team.ru/resource/2362157802/view)**:

{% note alert %}

вызывает рестарт контейнеров в случае использования статических ресурсов и перехода с более ранних версий

{% endnote %}

### **Обратно несовместимые изменения:**
* Нет

### **Известные проблемы:**
* Нет

### **Новая функциональность :**
* **Поддержка read only fs для боксов**
* **Возможность выставления access  permissions на файлы статических ресурсов**
* **Возможность выставления group id на файлы статических ресурсов**
* **Поддержка child only изоляции для контейнеров боксов**
* **Поддержка secret env для секретов** 

### **Исправления :**
* Нет


## **[pod_agent 93-1 2243467644](https://sandbox.yandex-team.ru/resource/2243467644/view)**:

### **Обратно несовместимые изменения:**

{% note alert %}

Пользовательские сигналы будут только в /user_sensors

{% endnote %}

### **Известные проблемы:**
* Нет

### **Новая функциональность :**
* **оторвали /sensores для пользовательских метрик.**
	* В подовом агенте пользовательские сигналы льются в ручку только в /user_sensors. 

### **Исправления :**
* **Улучшили описание ошибок для readiness и liveness probes**
    * Было: ``` fail_reason: Connection refused ```, например, при неудачной проверке с http/tcp. 
    При варианте с command fail_reason вообще не отображался, а показывался только stderr_tail, который заполнялся после падения команды.
    * Стало:
    Теперь можно увидеть какая именно команда вызвала ошибку, описание ошибки в случае http/tcp, а в случае command - exit code.
        
        **http request fail reason:**
        ```readiness probe failed: HTTP request to http2://localhost:111/yandex.ru: Connection refused```
        **tcp check fail reason:**
        ```readiness probe failed: TCP request to [::1]:111: Connection refused```
        **command fail reason:**
        ```liveness probe failed: command 'cat /unknown/file': exit_code = '1'```




## **[pod_agent 92-1 2196557167](https://sandbox.yandex-team.ru/resource/2196557167/view)**:

### **Обратно несовместимые изменения:**
* Нет

### **Известные проблемы:**
* Нет

### **Новая функциональность :**
* Нет

### **Исправления :**
* **Спрятали секреты из публичного описания пода**
* **Исправили пересечение портов с TVM**
* **Исправили метрику ротации логов**
* **Исправили обновление json спецификации**


## **[pod_agent 89-1 2051752541](https://sandbox.yandex-team.ru/resource/2051752541/view)**:

### **Обратно несовместимые изменения:**
* Нет

### **Известные проблемы:**
* Нет

### **Новая функциональность :**
* **Унесли логирование важной деятельности подагента в отдельный лог**
* **Alive service самого pod-agent**

### **Исправления :**
* Нет
