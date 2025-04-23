#       Hermes 

## Hermes - скрипт для мониторнига ugc трансляций,оценивает различные статусы и качество трансляции - из всех оценок отсылает наихудшую
## Граница качества до крита - 95%

> STREAM_TO_JUGGLER_STATUS = {
>    "STREAM_STATUS_UNSPECIFIED": "WARN",
>    "STREAM_STATUS_NEW": "OK",
>    "STREAM_STATUS_SCHEDULED": "OK",
>    "STREAM_STATUS_RUNNING": "OK",
>    "STREAM_STATUS_ERROR": "CRIT",
>    "STREAM_STATUS_WAIT_SRC": "WARN",
>    "STREAM_STATUS_FINISHED": "OK",
>    "NO DATA": "CRIT",
>    "NO CHANNELS": "OK",
>    "BROKEN RESPONSE": "WARN",
>    "BAD QUALITY": "CRIT",
>    "NORMAL QUALITY": "OK",
>    "HERMES ERROR": "CRIT",
>    "UNEXPECTED STATUS": "WARN",
>} 
- словарь внутренних статусов и их отображения в джагглер

Список трансляций берет по ссылке 
>TRANSLATIONS_URL: str = r"https://api.vh.yandex.net/v1/admin/live/upcoming?right_offset=1800"
где right_offset=1800 - трансляции,которые наступят через 1800 секунд 

# Описание функций

## check_response
    на вход принимает информацию о трансляции в формате >JSON
    На выход - bool - нужная ли нам ( технология ugc и важное событие) трансляция(True) или нет (False)
    обязателные ключи - ['state'],['channel'][service] - в случае отсутствия одного из них - возвращает False

## get_ugc_info
    дергает GET'ом TRANSLATIONS_URL,если status_code != OK,то возвращает пустой список
    иначе фильтрует данные(отбирает только нужные нам трансляции) с помощью check_response
    
