
# Table of Contents

1.  [Слаг](#slug-uml)
    1. [Стоимость доставки и сурж в слаге](#slug-surge)


<a id="slug-uml"></a>

# Слаг

scale 800 width
title Слаг

@startuml
!pragma useVerticalIf on

:GET /eats-catalog/v1/slug/{slug};

if (В запросе содержится гео позиция?) then (да)
    :Пытаемая получить часовой пояс
    исходя из переданной позиции;
else
    :Используем в часовой пояс сервера
    в качестве пользовательского;
endif

:Определение стратегии доступности по заголовку user-agent;

partition "Поиск заведения" {
    #pink:запрос в <color:red>eats-catalog-storage</color>
        для поиска заведения по слагу;

    if (В запросе передана гео позиция?) then (да)
        :Фильтрация зон по вхождению гео позиции в
        полигон зоны доставки;
    endif

    :Резолв зоны доставки;

    if (В запросе передана гео позиция?) then (да)
        :Расчет времени доставки исходя из
        расстояния по прямой;
        note
        Для расчета времени доставки используются кеши
        двух ручек <color:red>eats-core</color>:
        - <color:red>/server/api/v1/export/settings/regions-settings</color>
            для получения настроек регионов, которые
            содержат offset времени доставки и фиксированные
            времена доставки Лавки.
        - <color:red>/server/api/v1/export/settings/couriers-stats</color>
            для получения скорости курьера.
        endnote
    endif

    :Расчет доступности заведения;
}

if (Заведение не найдено?) then(да)
    stop
endif


fork
    if (Есть x-yandex-uid?) then (да)
        #pink:Запрос данных Яндекс.Плюс из <color:red>eats-plus</color>;
    endif
fork again
    if (Пользователь авторизован) then (да)
        #pink:Запрос избранных брендов пользователя из
        <color:red>eats-user-reactions/eats-user-reactions/v1/favourites/find-by-eater</color>;
    endif
fork again
    if (Заведение недоступно и передана гео позиция?) then (да)
        partition "Поиск доступного заведения" {
            note
            Пытаемся найти другое заведение того же
            бренда, которое доступно в данной
            гео позиции и доставка, из которого
            доступна на выбранное время чтобы
            фронт мог средиректить на него.
            endnote

            #pink:запрос в <color:red>eats-catalog-storage</color>
                для поиска заведения по гео позиции и бренду;

            :Резолв зоны доставки;

            :Расчет времени доставки исходя
                из расстояния по прямой;

            :Расчет доступности заведения;
        }
    endif
fork again
    #pink:Запрос к <color:red>plotva-ml-eats</color> для расчета времени
    доставки заказа;

    :Применяем рассчитанное время доставки;

    #pink:Запрашиваем сурж и трешхолды с помощью сервиса <color:red>eda-delivery-price</color>;
end fork

:Получение промоакций заведения;
note right
Для получения промоакций используется
кеш ручки <color:red>eats-core</color>
<color:red>/server/api/v1/promo/active</color>
endnote

:Формирование представления
заведения для выдачи клиенту;


stop
@enduml

<a src="slug-surge"></a>

## Стоимость доставки и сурж в слаге

title Расчет условий доставки

@startuml
!pragma useVerticalIf on

start

#palegreen:eats-catalog-storage;

:Резолв зоны доставки;

#palegreen:Расчет условий доставки c помощью запроса
<color:red>eda-delivery-price/v1/calc-delivery-price-surge</color>;

if (place.business != store) then
    :Устанавливаем трешхолды (условия доставки);
endif

if (place.delivery_type == native) then (да)
   if (place.business == store) then (да)
       :Увеличиваем минимальную корзину в условиях;
   else (нет)
       :Устанавливаем минимальную стоимость доставки;
   endif
endif

:Ограничиваем цену доставки, используя настойки регионов;

stop

@enduml

